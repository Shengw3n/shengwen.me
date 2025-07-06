---
title: 1. Stabilizing my Rhythm
duration: 5 min
date: 2025-06-30T12:00:00Z
image: /images/1.jpeg
math: true
---

> This post is a reflection on the month of June 2025.

![Outside UBC Rocket Building](/images/1.jpeg)

My friends repeatedly mentioned how my May review had a bit of a melancholic tone—I swear I'm joyful most of the time! Unlike the pressured atmosphere in May where I was adjusting to working life, catching product deadlines, and managing a 3-hour daily commute, June has been much kinder to me. I'm fully adjusted to the working rhythm and even slacked off a bit after work to watch some quality League of Legends esports.

## Last and Only Chance

There's a famous saying in League of Legends esports by 2020 World Champion ShowMaker before his final: "With the opportunity I have now, I need to go in thinking this could be my last and only chance." He has never won another world title since. This saying hit me as I watched my favorite player, Knight, showing deep remorse at the regular season playoffs, months after losing two World finals back-to-back. With his current team and skill level, he may never get as close to a World title again.

Now that I'm 21, in university, and surrounded by opportunities, I must also approach each moment thinking this could be my last and only chance.

## UBC Rocket

June has been strong for the Thrust Vectoring Team—our firmware is polished and, most importantly, our simulation is roughly complete. We made a major design decision for our MATLAB simulation: removing the aerodynamic components and focusing mainly on thrust-based calculations. There are two key reasons: first, none of us are mechanical engineering majors, so we don't fully understand aerodynamics; second, our rocket won't go particularly fast or high since we mainly want to demonstrate active stabilization abilities. It's actually harder to stabilize a slow-moving object than a fast one, so aerodynamic impact should be minimal—or at least that's what a couple of ELEC and Computer Science students think.

Moving to a thrust-based simulation and measuring actual dimensions like mass and inertia proved quite accurate. Below is our second hold-down test:

<div style="display: flex; justify-content: center;">
  <video width="400" height="300" controls loop>
    <source src="/vids/holddown2.mov" type="video/mp4">
  </video>
</div>

As you can see, the rocket is mostly stable with some oscillations at the end. This is mainly due to integral windup, where small steady-state errors accumulate in the integral term as our rocket flies. Simply reducing the integral gain should help stabilize it.

The second hold-down test validates our simulation—though as with all simulations, there are bound to be differences from the real world, and some manual tuning is always necessary.

Next month, we'll finish our parachute ejection design and firmware integration, then begin actual flight tests. Stay tuned 😋

## The Xiaomi Lesson on Fast Iterations

I'm currently halfway through Lei Jun's book on Xiaomi's success. One thing that really stood out was how he attributed Xiaomi's success to their incredibly fast iteration cycle. At peak, their insider version would get updated three or more times daily, with weekly stable releases. Lei Jun proudly mentioned their vibrant community of users who deeply loved Xiaomi phones and constantly provided feedback—essentially an army of free manual software testers who were also end users. This was possible because Lei Jun described himself as a huge Chinese forum moderator in the early days of the internet, with extensive experience managing active communities.

As I now lead the Thrust Vectoring Team at UBC Rocket, it feels like a startup environment where a few students try to build something cool—except we don't make money, we just burn it. Moving up the corporate ladder of university design teams, I'm gaining a systems overview of the entire project and slowly realizing the importance of fast iteration and user feedback.

During our 2024 competition cycle, I was the sole firmware and controls developer for our first Thrust Vectoring Demo Drone, which won second place at Launch Canada 2024. Our drone used an EDF (electric ducted fan), meaning I could test whenever I wanted—I just needed electricity and a kill switch ready in case anything went wrong. My iteration cycle was super fast, and I achieved a good demo in relatively short time.

For our 2025 competition cycle, despite having a dedicated team and more resources, our iteration cycle has actually become considerably slower. We're now using a solid motor that costs $25 to test each time and produces considerable thrust. Every test requires finding a safe location with no people or potential harm to surroundings, meaning driving far from UBC and Vancouver due to tight rocketry regulations. This limitation was completely unexpected and incredibly frustrating to deal with.

For next year, I'm planning to return to drone design since the Thrust Vectoring team is mainly interested in control algorithms, which can't be developed efficiently if we can only test our algorithms during biweekly trips to remote locations.

## Plan for Next Month

While I slacked off a bit this month, it's time to get back to the grind in July. I have an Electronic Materials makeup final in mid-July (I was sick during finals season) and need to start preparing for interviews as I look for January co-op placement. September will be busy restarting my research project and hopefully publishing it soon (more on that later 😉) while juggling my current internship and finding a new one. July and August will be my only opportunity to fine-tune my technical skills and get our rocket competition-ready.

Busy times, but I'm really enjoying it.

---

Thank you for reading my thoughts this far. Steven out :)
