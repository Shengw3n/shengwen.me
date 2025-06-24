---
title: Projects - Steven Chen
display: Projects
description: List of projects that I am proud of
wrapperClass: 'text-center'
art: dots
projects:
  Current Focus:
    - name: 'TIPSO Manager'
      link: 'https://www.nztech.ca/airpad/'
      desc: 'Qt Quick GUI for AirPad Configurations<br>Intern Project @ NZ Tech'
      icon: 'i-material-symbols:web-asset'
    - name: 'Thrust Vectoring Rocket'
      link: 'https://github.com/UBC-Rocket/Thrust-Vectoring-II'
      desc: 'PID-Controlled Thrust Vectoring<br>Competing @ Launch Canada 2025'
      icon: 'i-material-symbols:rocket-launch-outline'
    - name: 'da Vinci 3D Gaze Estimation'
      desc: 'Computer Vision + LSTM Model<br>Research Project @ RCL'
      icon: 'i-material-symbols:eye-tracking-outline'

  Embedded Systems:
      - name: 'TIPSO AirPad'
        link: 'https://www.nztech.ca/airpad/'
        desc: 'FDA-Approved HMI for Surgeons<br>Intern Project @ NZ Tech'
        icon: 'i-material-symbols:trackpad-input'
      - name: 'Thrust Vectoring Drone'
        link: 'https://github.com/UBC-Rocket/Thrust-Vectoring'
        desc: 'PID-Controlled Tethered Drone<br>2nd Place @ Launch Canada 2024'
        icon: 'i-material-symbols:rocket-outline'
      - name: 'Metal Detector Robot'
        link: 'https://github.com/Shengw3n/Remote-Controlled-Metal-Detector-Robot'
        desc: 'Dual MCU Remote Controlled Robot in C<br>Course Project for ELEC 291'
        icon: 'i-material-symbols:toys-outline'
      - name: 'Reflow Oven Controller'
        link: 'https://github.com/Shengw3n/Reflow-Oven-Controller'
        desc: 'Reflow Oven Controller in Assembly<br>Course Project for ELEC 291'
        icon: 'i-material-symbols:oven-outline'
      - name: "Beauty & the Beast"
        link: 'https://www.ubcrocket.com/past-projects.html'
        desc: '30k Two-Stage Solid Rocket<br> 1st Place @ Launch Canada 2023'
        icon: 'i-game-icons:rocket-flight'

  FPGA:
      - name: 'FPGA RISC Machine'
        link: 'https://github.com/Shengw3n/FPGA-Reduced-Instruction-Set-Computer'
        desc: '16-bit RISC Machine in System Verilog<br>Course Project for CPEN 211'
        icon: 'i-material-symbols:memory-rounded'

---

<!-- @layout-full-width -->
<ListProjects :projects="frontmatter.projects" />
