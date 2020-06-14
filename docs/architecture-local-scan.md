---
id: architecture-local-scan
title: Local Scan Mode(Scan without SSH)
sidebar_label: Local Scan Mode
---

SSH를 통해 중앙 vuls 서버가 각 서버에 연결되지 않도록 하려면 로컬 스캔 모드에서 vuls를 사용할 수 있다. vuls를 스캔 대상 서버에 배포하고 대상서버에서 vuls를 실행한다. 스캔 결과를 세분화하려면 CVE 데이터베이스에 액세스해야 하므로 미리 서버 모드에서 Go-cve-dictionary를 실행한다.
집계 서버에서는 웹을 사용하여 각 검색 대상 서버의 검색 결과를 참조할 수 있다.UI 또는 TUI.

![Vuls-Architecture Local Scan Mode](/img/docs/vuls-architecture-localscan.png)

[Tutorial: local scan mode](tutorial-local-scan.md)

