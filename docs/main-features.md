---
id: main-features
title: Main Features
sidebar_label: Main Features
---

## Linux/FreeBSD Server의 취약점 스캔

[주요 지원 OS](supported-os.md)

- Alpine, Ubuntu, Debian, CentOS, Amazon Linux, RHEL, Oracle Linux, SUSE Enterprise Linux and Raspbian, FreeBSD
- Cloud, on-premise, Docker

## 고품질 스캔

Vuls는 다음과 같이 여러개의 취약점 데이터베이스를 사용한다.

- [NVD](https://nvd.nist.gov/)
- [JVN(Japanese)](http://jvndb.jvn.jp/apis/myjvn/)
- OVAL
  - [Red Hat](https://www.redhat.com/security/data/oval/)
  - [Debian](https://www.debian.org/security/oval/)
  - [Ubuntu](https://people.canonical.com/~ubuntu-security/oval/)
  - [SUSE](http://ftp.suse.com/pub/projects/security/oval/)
  - [Oracle Linux](https://linux.oracle.com/security/oval/)
- [Alpine-secdb](https://git.alpinelinux.org/cgit/alpine-secdb/)
- [Red Hat Security Advisories](https://access.redhat.com/security/security-updates/)
- [Debian Security Bug Tracker](https://security-tracker.debian.org/tracker/)
- Commands(yum, zypper, pkg-audit)
  - RHSA/ALAS/ELSA/FreeBSD-SA
- [Exploit Database](https://www.exploit-db.com/)
- [US-CERT](https://www.us-cert.gov/ncas/alerts)
- [JPCERT](http://www.jpcert.or.jp/at/2019.html)
- [WPVulnDB](https://wpvulndb.com/api)
- [Node.js Security Working Group](https://github.com/nodejs/security-wg)
- [Ruby Advisory Database](https://github.com/rubysec/ruby-advisory-db)
- [Safety DB(Python)](https://github.com/pyupio/safety-db)
- [PHP Security Advisories Database](https://github.com/FriendsOfPHP/security-advisories)
- [RustSec Advisory Database](https://github.com/RustSec/advisory-db)
- Changelog

## 빠른 스캔과 깊은 스캔

[빠른 스캔](architecture-fast-scan.md)

- 루트 권한 없이 스캔, 종속성 없음
- 스캔 대상 서버에 부하가 거의 없음
- 인터넷 접속이 없는 오프라인 모드 스캔 (Red Hat, CentOS, OracleLinux, Ubuntu, Devian)

[Root 권한이 필요한 빠른 스캔](architecture-fast-root-scan.md)

- 루트 권한으로 스캔
- 스캔 대상 서버에 부하가 거의 없음
- yum-ps(Red Hat, CentOS, Oracle Linux, Amazon Linux)를 사용하여 업데이트에 영향을 받는 프로세스 탐지
- debian-goodies의 checkrestart(Debian 및 Ubuntu)를 사용하여 이전에 업데이트 되었지만 아직 다시 시작하지 않은 프로세스 감지
- 인터넷 접속이 없는 오프라인 모드 스캔. (Red Hat, CentOS, OracleLinux, Ubuntu, Devian)

[상세 스캔](architecture-deep-scan.md)

- Root 권한이 필요한 빠른 스캔과 동일

## [원격 스캔모드, 로컬 스캔모드, 서버모드](architecture-remote-local.md)

[원격 스캔 모드](architecture-remote-scan.md)

- 사용자는 SSH를 통해 다른 대상 서버에 연결된 하나의 시스템만 설정해야 한다.

[로컬 스캔 모드](architecture-local-scan.md)

- SSH를 통해 Vuls 서버가 각 서버에 연결되지 않도록 하려면 로컬 검색 모드에서 Vuls를 사용한다.

[서버 모드](https://vuls.io/docs/en/usage-server.html)

- SSH도 필요 없고 스캐너도 필요 없다. 검색 태겟 서비스에서 Linux 명령 디렉토리만 실행.
- 먼저 서버 모드에서 Vuls를 시작하고 HTTP 서버로 데이터를 받는다.
- 서버 모드에서 취약점을 시작하고 HTTP 서버로 수신을 대기한다.
- 다음으로, 스캔 대상 서버에 명령을 내려 소프트웨어 정보를 수집한다. 그런 다음 HTTP를 통해 결과를 Vuls Server로 전송하고 검색 결과는 JSON 형식으로 수신한다.

## **상세** 분석

- SSH를 통해 접속하여 명령을 실행함으로써 서버 상태를 획득할 수 있다.
- Vuls는 다시 시작하지 않은 프로세스에 대해 경고하지만 아직 다시 시작하지는 않았으며 소프트웨어 업데이트에 영향을 미치는 프로세스를 미리 감지한다.

## **정적** 컨테이너 분석

- Vuls는 ECR, GCR 및 로컬의 Docker Image와 같은 컨테이너 이미지를 스캔 할 수 있다.
- TODO Link

## [OS 패키지 관리에 포함되지 않은 미들웨어 스캔](usage-scan-non-os-packages.md)

- 미들웨어, 프로그래밍 언어 라이브러리 및 프레임 워크의 취약점 스캔
- CPE에 등록된 지원 소프트웨어

## 통합

- [GitHub Security Alerts](usage-scan-non-os-packages.html#usage-integrate-with-github-security-alerts.md)
- [OWASP Dependency Check](usage-scan-non-os-packages.html#usage-integrate-with-owasp-dependency-check-to-automatic-update-when-the-libraries-are-updated-experimental.md)
- [WordPress](usage-scan-wordpress.md)

## 기타

- 비파괴 검사
- AWS에서 스캔하기 위해서 사전 승인이 필요하지 않습니다.
- Vuls는 매일 테스트를 실행할 수 있어 지속적인 통합과 잘 작동한다. 이를통해 취약점을 빠르게 찾을 수 있다.
- [구성 파일 템플릿 자동 생성](usage-automatic-discovery.md)
  - CIDR을 사용하여 설정된 서버의 자동 감지, 구성 파일 템플리트 생성
- 이메일 및 슬랙 알림 가능(일본어 지원)
- 스캔결과는 TUI, [TUI Viewer on terminal](usage-tui.md) 또는 Web UI를 지원한다. ([VulsRepo](https://github.com/ishiDACo/vulsrepo)).
