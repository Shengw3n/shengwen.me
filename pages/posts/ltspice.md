---
title: Installing LTspice Windows Edition on macOS (Tutorial)
date: 2025-04-21T12:00:00Z
desc: How to run LTSpice Windows Edition on macOS
duration: 10min
image: /images/LTspice.jpg
type: note
---

[[toc]]

![LT Spice](/images/LTspice.jpg)

## Prerequisites

- macOS (Intel or Apple Silicon)
- Homebrew package manager

## Installation Steps

### 1. Install Wine

```bash
brew install --cask --no-quarantine wine-stable
```

### 2. Download LTspice

Download the latest Windows version (`LTspice64.msi`) from the [ADI website](https://www.analog.com/en/design-center/design-tools-and-calculators/ltspice-simulator.html).

### 3. Install LTspice through Wine

```bash
cd ~/Downloads
wine msiexec /i LTspice64.msi
```

### 4. Create an Application Launcher

1. Open **Automator** and create a new **Application**
2. Add a **Run Shell Script** action
3. Paste this script:

```bash
cd "$HOME/.wine/drive_c/Program Files/ADI/LTspice/" || exit 1
WINEDEBUG=-all wine LTspice.exe > /dev/null 2>&1 &
```

4. Save as "LTspice (Wine)" to Applications folder

### 5. Launch

Double-click your new application to run LTspice.

LTspice on Wine provides all functionality of the Windows version, though complex simulations may run slightly slower. However, in my experience everything ran smoothly with no crashes.
