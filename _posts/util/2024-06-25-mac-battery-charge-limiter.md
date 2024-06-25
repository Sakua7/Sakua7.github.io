---
title: 'Macbook(Arm) 배터리 유틸 추천'
date: 2024-06-25 12:00:00 +0000
categories: [Mac, Utility]
tags: [Mac, Utility]
author: Sakua7
mermaid: true
---

배터리 차지 제한 유틸리티를 소개합니다.

사용해야하는 이유: 배터리 수명을 오래 사용하기 위해 풀 충전(100%)은 피해야 하지만 충전기를 꼽아놓고 쓸 경우 관리하기 어렵기에 충전을 제한하는 프로그램을 사용해야 합니다.

본 오프소스는 AI Delte 유료 버전처럼 다양한 기능은 없지만 메인 기능이라고 할 수 있는 일정 비율 이상 충전 제한을 충실하게 제공하며 CLI로 사용할 수 있는 게 매력입니다.

**단, M 칩(Arm) 버전 Macbook에서만 동작하므로 Intel Macbook 유저분들은 AI Delte를 사용하셔야 할 것 같습니다.**

깃허브 Repository
<div style="background-color: #007bff; padding: 10px; border-radius: 15px; text-align: center;">
    <a href="https://github.com/actuallymentor/battery" style="color: white;  font-size: 1.2em;">
        https://github.com/actuallymentor/battery
    </a>
</div>

---

```
// brew를 사용해 설치후 battery 입력하면 친절하게 command들을 알려줍니다.
// 메인기능은 battery maintain [1~100, stop]
// 80%로 제한을 걸려면 "battery maintain 80"으로 사용할 수 있습니다.

1. brew install battery
2. battery

Battery CLI utility v1.1.6

Usage:
  battery status
    output battery SMC status, % and time remaining

  battery logs LINES[integer, optional]
    output logs of the battery CLI and GUI
	eg: battery logs 100

  battery maintain LEVEL[1-100,stop]
    reboot-persistent battery level maintenance: turn off charging above, and on below a certain value
	it has the option of a --force-discharge flag that discharges even when plugged in (this does NOT work well with clamshell mode)
    eg: battery maintain 80
    eg: battery maintain stop

  battery charging SETTING[on/off]
    manually set the battery to (not) charge
    eg: battery charging on

  battery adapter SETTING[on/off]
    manually set the adapter to (not) charge even when plugged in
    eg: battery adapter off

  battery charge LEVEL[1-100]
    charge the battery to a certain percentage, and disable charging when that percentage is reached
    eg: battery charge 90

  battery discharge LEVEL[1-100]
    block power input from the adapter until battery falls to this level
    eg: battery discharge 90

  battery visudo
    ensure you don't need to call battery with sudo
    This is already used in the setup script, so you should't need it.

  battery update
    update the battery utility to the latest version

  battery reinstall
    reinstall the battery utility to the latest version (reruns the installation script)

  battery uninstall
    enable charging, remove the smc tool, and the battery script
```