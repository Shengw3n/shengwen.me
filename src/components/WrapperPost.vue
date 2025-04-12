<script setup lang='ts'>
import { formatDate } from '~/logics'

const { frontmatter } = defineProps({
  frontmatter: {
    type: Object,
    required: true,
  },
})

const router = useRouter()
const route = useRoute()
const content = ref<HTMLDivElement>()

// MathJax support
const mathjaxLoaded = ref(false)

// Check if math is enabled in frontmatter
const mathjaxEnabled = computed(() => frontmatter?.math === true)

// Load MathJax when needed
onMounted(() => {
  if (mathjaxEnabled.value && !mathjaxLoaded.value) {
    loadMathJax()
  }

  // Rest of your existing onMounted code
  const navigate = () => {
    if (location.hash) {
      const el = document.querySelector(decodeURIComponent(location.hash))
      if (el) {
        const rect = el.getBoundingClientRect()
        const y = window.scrollY + rect.top - 40
        window.scrollTo({
          top: y,
          behavior: 'smooth',
        })
        return true
      }
    }
  }

  const handleAnchors = (
    event: MouseEvent & { target: HTMLElement },
  ) => {
    const link = event.target.closest('a')

    if (
      !event.defaultPrevented
      && link
      && event.button === 0
      && link.target !== '_blank'
      && link.rel !== 'external'
      && !link.download
      && !event.metaKey
      && !event.ctrlKey
      && !event.shiftKey
      && !event.altKey
    ) {
      const url = new URL(link.href)
      if (url.origin !== window.location.origin)
        return

      event.preventDefault()
      const { pathname, hash } = url
      if (hash && (!pathname || pathname === location.pathname)) {
        window.history.replaceState({}, '', hash)
        navigate()
      }
      else {
        router.push({ path: pathname, hash })
      }
    }
  }

  useEventListener(window, 'hashchange', navigate)
  useEventListener(content.value!, 'click', handleAnchors, { passive: false })

  setTimeout(() => {
    if (!navigate())
      setTimeout(navigate, 1000)
  }, 1)
})

// Watch for route changes to re-render MathJax when navigating
// between math-enabled pages
watch(() => route.path, () => {
  if (mathjaxEnabled.value && mathjaxLoaded.value && window.MathJax) {
    setTimeout(() => {
      window.MathJax.typeset()
    }, 100)
  }
})

function loadMathJax() {
  // Check if MathJax is already loaded
  if (document.getElementById('MathJax-script')) {
    // If already loaded, just typeset the current page
    if (window.MathJax) {
      setTimeout(() => {
        window.MathJax.typeset()
      }, 100)
    }
    return
  }

  // Set up global MathJax configuration
  window.MathJax = {
    tex: {
      inlineMath: [['$', '$'], ['\\(', '\\)']],
      displayMath: [['$$', '$$'], ['\\[', '\\]']],
    },
    options: {
      skipHtmlTags: ['script', 'noscript', 'style', 'textarea', 'pre', 'code'],
      processHtmlClass: 'tex2jax_process',
      ignoreHtmlClass: 'tex2jax_ignore',
    },
    startup: {
      pageReady() {
        mathjaxLoaded.value = true
        return window.MathJax.startup.defaultPageReady()
      },
    },
  }

  // Add MathJax script dynamically
  const script = document.createElement('script')
  script.id = 'MathJax-script'
  script.src = 'https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js'
  script.async = true
  document.head.appendChild(script)
}

// const base = 'https://antfu.me'
// const tweetUrl = computed(() => `https://twitter.com/intent/tweet?text=${encodeURIComponent(`Reading @antfu7\'s ${base}${route.path}\n\nI think...`)}`)
// const elkUrl = computed(() => `https://elk.zone/intent/post?text=${encodeURIComponent(`Reading @antfu@m.webtoo.ls\'s ${base}${route.path}\n\nI think...`)}`)
// const blueskyUrl = computed(() => `https://bsky.app/intent/compose?text=${encodeURIComponent(`Reading @antfu.me ${base}${route.path}\n\nI think...`)}`)

const ArtComponent = computed(() => {
  let art = frontmatter.art
  if (art === 'random')
    art = Math.random() > 0.5 ? 'plum' : 'dots'
  if (typeof window !== 'undefined') {
    if (art === 'plum')
      return defineAsyncComponent(() => import('./ArtPlum.vue'))
    else if (art === 'dots')
      return defineAsyncComponent(() => import('./ArtDots.vue'))
  }
  return undefined
})
</script>

<template>
  <ClientOnly v-if="ArtComponent">
    <component :is="ArtComponent" />
  </ClientOnly>
  <div
    v-if="frontmatter.display ?? frontmatter.title"
    class="prose m-auto mb-8"
    :class="[frontmatter.wrapperClass]"
  >
    <h1 class="mb-0 slide-enter-50">
      {{ frontmatter.display ?? frontmatter.title }}
    </h1>
    <p
      v-if="frontmatter.date"
      class="opacity-50 !-mt-6 slide-enter-50"
    >
      {{ formatDate(frontmatter.date, false) }} <span v-if="frontmatter.duration">· {{ frontmatter.duration }}</span>
    </p>
    <p v-if="frontmatter.place" class="mt--4!">
      <span op50>at </span>
      <a v-if="frontmatter.placeLink" :href="frontmatter.placeLink" target="_blank">
        {{ frontmatter.place }}
      </a>
      <span v-else font-bold>
        {{ frontmatter.place }}
      </span>
    </p>
    <p
      v-if="frontmatter.subtitle"
      class="opacity-50 !-mt-6 italic slide-enter"
    >
      {{ frontmatter.subtitle }}
    </p>
    <p
      v-if="frontmatter.draft"
      class="slide-enter" bg-orange-4:10 text-orange-4 border="l-3 orange-4" px4 py2
    >
      This is a draft post, the content may be incomplete. Please check back later.
    </p>
  </div>
  <article ref="content" :class="[frontmatter.tocAlwaysOn ? 'toc-always-on' : '', frontmatter.class]">
    <slot />
  </article>
  <div v-if="route.path !== '/'" class="prose m-auto mt-8 mb-8 slide-enter animate-delay-500 print:hidden">
    <!-- <template v-if="frontmatter.duration">
      <span font-mono op50>> </span>
      <span op50>comment on </span>
      <a :href="blueskyUrl" target="_blank" op50>bluesky</a>
      <span op25> / </span>
      <a :href="elkUrl" target="_blank" op50>mastodon</a>
      <span op25> / </span>
      <a :href="tweetUrl" target="_blank" op50>twitter</a>
    </template> -->
    <br>
    <span font-mono op50>> </span>
    <RouterLink
      :to="route.path.split('/').slice(0, -1).join('/') || '/'"
      class="font-mono op50 hover:op75"
      v-text="'cd ..'"
    />
  </div>
</template>

<style>
/* Optional: Some basic styling for math elements */
.mjx-chtml {
  display: inline-block;
  line-height: 0;
  text-indent: 0;
  text-align: left;
  text-transform: none;
  font-style: normal;
  font-weight: normal;
  font-size: 100%;
  font-size-adjust: none;
  letter-spacing: normal;
  word-wrap: normal;
  word-spacing: normal;
  white-space: nowrap;
  direction: ltr;
  padding: 1px 0;
}

.MJX-TEX {
  font-family: 'MJXc-TeX-math-I,MJXc-TeX-math-Ix,MJXc-TeX-math-Iw';
}

.mjx-block {
  display: block;
  margin: 1em 0;
}

.mjx-chtml[display='true'] {
  display: block;
  margin: 1em 0;
}
</style>
