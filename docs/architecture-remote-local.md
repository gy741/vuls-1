---
id: architecture-remote-local
title: Remote, Local, One-liner scan
sidebar_label: Remote, Local, One-liner scan
---

Vuls는 3가지 모드를 지원한다.: [원격 스캔 모드](architecture-remote-scan.md) and [로컬 스캔 모드](architecture-local-scan.md) and [서버 모드](usage-server.md).

## [원격 스캔 모드](architecture-remote-scan.md)

원격 스캔 모드는 SSH를 통해 스캔 대상 서버에 연결하고 일부 명령을 실행하여 스캔한다.

## [로컬 스캔 모드](architecture-local-scan.md)

로컬 스캔 모드에서는 SSH가 필요하지 않으며 로컬 호스트에서 직접 명령을 실행하여 스캔한다.

## [서버 모드](https://vuls.io/docs/en/usage-server.html)

- SSH를 사용하지 않으며, 또한 스캐너가 필요 없다. 검색 대상 서버에서 직접 리눅스 명령만 실행하여 스캔한다..
- 먼저 서버 모드에서 Vuls를 시작하고 HTTP 서버로 수신한다.
- 그 다음, 검색 대상 서버에서 명령을 실행하여 소프트웨어 정보를 수집한다. 그런 다음 HTTP를 통해 결과를 Vuls Server로 전송한다. 스캔 결과는 JSON 형식으로 수신한다.
