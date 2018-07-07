---
layout: lost
title: "민트 19로 업그레이드"
categories: tools
date: 2018-07-07 13:00:00 +0900
---
나는 리눅스 민트를 사용한다. 19가 나왔다길래 업그레이드했다. [설명](https://community.linuxmint.com/tutorial/view/2416)을 읽고 그대로 하면 된다.

## 스냅샷 만들기
별로 만들고 싶지는 않았지만,

~~~bash
$ apt install timeshift
~~~

`timeshift` 스냅샷 만들기 완성

## LightDM

~~~bash
$ cat /etc/X11/default-display-manager
~~~

`lightdm`이 나오므로 패스

## 업그레이드

업그레이드 자체는 일련의 다운로드 명령이다. 모두 꽤 오래 걸린다.

~~~bash
$ sudo apt install mintupgrade
$ mintupgrade check
$ mintupgrade download
$ mintupgrade upgrade
$ sudo reboot
~~~

시간이 오래 걸려서 그렇지 문제 없이 깔끔하게 해결되었다.
