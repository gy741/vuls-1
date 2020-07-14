---
id: install-with-vulsctl
title: Install with vulsctl
sidebar_label: Vulsctl - Quickest Vuls setup
---

## Vulsctl

### 리눅스 배포판
다음 예제는 CentOS, RedHat, Amazon Linux 등을 포함한 Fedora 기반 Linux 배포판에서 동작한다.(CentOS 및 Red Hat 7에서 테스트).

[Vulsctl](https://github.com/vulsio/vulsctl)은 설정을 쉽게하기 위해 만들어졌으며 Docker 기반에서 실행된다. 

## 도커 설치

- [Docker 설치] (https://docs.docker.com/engine/install/)
- [root 사용자가 아닌 일반 사용자로 도커 관리](https://docs.docker.com/install/linux/linux-postinstall/)

```bash
$ sudo systemctl start docker
```

## Vulsctl 복사

```bash
$ git clone https://github.com/vulsio/vulsctl.git
$ cd vulsctl
```

## 취약점 데이터베이스 가져오기

이 작업은 시간이 걸릴 수 있다...

```
$ ./update-all.sh
```

## 설정, 스캔, 보고서

**vulsctl** 설치 디렉토리에서 아래 구성을 참고하여 **config.toml** 파일을 준비한다.

```
[servers]
[servers.hostos]
host        = "52.10.10.10"
port        = "22"
user        = "centos"
# if ssh config file exists in .ssh, path to ssh config file in docker
sshConfigPath   = "/root/.ssh/config" 
# keypath in the Vuls docker container
keyPath     = "/root/.ssh/id_rsa"
```
`.ssh`에 `config`파일이 있을 경우 SSH 연결할 떄 vuls는 도커 컨테이너에 있는 `/root/.ssh/config` 파일을 가리킨다.
그러나 로컬 사용자가 도커의 사용자와 일치하지 않기 때문에 오류가 발생한다.
이 문제를 해결하려면 `sshConfigPath` 옵션에 `/root/.ssh/config`  파일을 지정한다.

**scan.sh** 파일은 호스트 운영체제에서 **$HOME/.ssh**를 컨테이너에 탑재하지만,
미리 대상서버에 SSH를 설치해야 $HOME/.ssh/known_hosts 지문을 추가할 수 있다.

`
![](https://user-images.githubusercontent.com/534611/66093182-20535f00-e5ca-11e9-8060-8c9247abcefa.jpg)

```
$ ssh centos@52.100.100.100 -i ~/.ssh/id_rsa.pem
```

```
$ ./scan.sh
$ ./report.sh
$ ./tui.sh
```

자세한 설명은 아래 링크에 있다.
- [scan.sh](https://github.com/vulsio/vulsctl/blob/master/scan.sh)
- [report.sh](https://github.com/vulsio/vulsctl/blob/master/report.sh)
- [tui.sh](https://github.com/vulsio/vulsctl/blob/master/tui.sh)

## Deploy `vuls` on the host

[install-host.sh](https://github.com/vulsio/vulsctl/blob/5efed5284bf97e9915563644d90411490bcf47ce/install-host.sh) 스크립트를 사용하여 `vuls`을 쉽게 설치 할 수 있다.

```bash
$ sudo bash install-host.sh
```

> The support for RHEL and CentOS 6.x / 7.x is in [pull requests](https://github.com/vulsio/vulsctl/pulls).

## Vulsrepo

```
$ ./vulsrepo.sh
$ docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS                    NAMES
39c8830dbeac        ishidaco/vulsrepo   "vulsrepo-server"   3 seconds ago       Up 1 second         0.0.0.0:5111->5111/tcp   focused_wu
```

Vulsrepo는 http://host-ip:5111 기본 포트로 5111을 사용하여 실행된다.
