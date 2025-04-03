---
title: Projects - Steven Chen
display: Projects
description: List of projects that I am proud of
wrapperClass: 'text-center'
art: dots
projects:
  Current Focus:
    - name: 'Thrust Vectoring Rocket'
      link: 'https://github.com/UBC-Rocket/Thrust-Vectoring-II'
      desc: 'PID-Controlled Thrust Vectoring'
      icon: 'i-material-symbols:rocket-launch-outline'

  Embedded Systems:
      - name: 'Thrust Vectoring Drone'
        link: 'https://github.com/UBC-Rocket/Thrust-Vectoring'
        desc: '2nd Place @ Launch Canada 2024'
        icon: 'i-material-symbols:rocket-outline'
      - name: 'Metal Detector Robot'
        link: 'https://github.com/Shengw3n/Remote-Controlled-Metal-Detector-Robot'
        desc: 'Dual MCU Remote Controlled Robot in C'
        icon: 'i-material-symbols:toys-outline'
      - name: 'Reflow Oven Controller'
        link: 'https://github.com/Shengw3n/Reflow-Oven-Controller'
        desc: 'Reflow Oven Controller in Assembly'
        icon: 'i-material-symbols:oven-outline'

  FPGA:
      - name: 'FPGA RISC Machine'
        link: 'https://github.com/Shengw3n/FPGA-Reduced-Instruction-Set-Computer'
        desc: '16-bit RISC Machine in System Verilog'
        icon: 'i-material-symbols:memory-rounded'
---

<!-- @layout-full-width -->
<ListProjects :projects="frontmatter.projects" />
