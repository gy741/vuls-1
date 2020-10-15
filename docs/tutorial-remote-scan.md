---
id: tutorial-remote-scan
title: Tutorial - Remote Scan Mode
sidebar_label: Remote Scan Mode
---

이 튜토리얼을 통해 SSH를 통해 원격 호스트에서 uls를 사용하여 취약점을 스캔 할 수 있다.

1. 새로운 Ubuntu Linux 시작
1. localhost에서 SSH 활성화
1. 구성 확인
1. 스캔하기 전에 config.toml 및 서버의 설정 확인
1. 스캔 시작
1. 보고서 확인

이전 튜토리얼에서 생성된 Vuls 서버(localhost라고 함)를 사용할 것이다.

## Step1. 새로운 Ubuntu Linux 실행

다음 튜토리얼과 같다.  [Tutorial: Local Scan Mode#Step1. Launch CentOS7](tutorial-local-scan.md#step1-launch-centos7)  
터미널을 실행하고 원격 호스트에 연결한다.
원격 호스트 키를 `$HOME/.ssh/known_hosts`,에 추가하려면 검색하기 전에 SSH를 통해 원격 호스트에 로그인해야 한다.

## Step2. localhost에서 SSH 활성화

Vuls SSH 암호 인증을 지원하지 않으며 따라서 SSH 키 기반 인증을 사용해야 한다.
localhost에 키페어를 만든 다음 원격 호스트의 certified_keys에 공개 키를 추가한다.

### localhost

```bash
$ ssh-keygen -t rsa
```

Copy `~/.ssh/id_rsa.pub` to the clipboard.

### Remote Host

```bash
$ mkdir ~/.ssh
$ chmod 700 ~/.ssh
$ touch ~/.ssh/authorized_keys
$ chmod 600 ~/.ssh/authorized_keys
$ vim ~/.ssh/authorized_keys
```

클립보드에서 `~/.ssh/authorized_keys` 파일에 붙여넣는다.

또한 검색 대상 서버의 호스트 키가 localhosts의 known_hosts에 등록되었는지 확인한다.
원격 호스트의 호스트 키를 `$HOME/.ssh/known_hosts`에 추가하려면 검색하기 전에 SSH를 통해 원격 호스트에 로그인해야 한다.

### localhost

```bash
$ ssh ubuntu@172.31.4.82 -i ~/.ssh/id_rsa
```

## Step3. Configure (config.toml)

### localhost

```bash
$ cd $HOME
$ cat config.toml
[servers]

[servers.ubuntu]
host         = "172.31.4.82"
port        = "22"
user        = "ubuntu"
keyPath     = "/home/centos/.ssh/id_rsa"
```

## Step4. Check config.toml and settings on the server before scanning

```bash
$ vuls configtest ubuntu
```

see [Usage: configtest](#usage-configtest)

## Step5. Start Scanning

```bash
$ vuls scan ubuntu
... snip ...

One Line Summary
================
ubuntu  ubuntu16.04     30 updatable packages
```

## Step6. Reporting

- See [Tutorial: Local Scan#Step6. Reporting](tutorial-local-scan.md#step6-reporting)
- See [Tutorial: Local Scan#Step7. TUI](tutorial-local-scan.md#step7-tui)
- See [Tutorial: Local Scan#Step8. Web UI](tutorial-local-scan.md#step8-web-ui)

