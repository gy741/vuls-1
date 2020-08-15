---
id: architecture-fast-root-scan
title: Fast-Root Scan
sidebar_label: Fast-Root Scan
---

![Vuls-Scan-Flow](/img/docs/vuls-scan-flow-fast-root.png)

| Distribution|                             Scan Speed | Need Root Privilege |       OVAL | Need Internet Access|
|:------------|:--------------------------------------:|:-------------------:|:----------:|:---------------------------------------:|
| Alpine      |                                   Fast |　                No |  Supported |                                    Need |
| CentOS      |                                   Fast |　              Need |  Supported |                                    Need |
| RHEL        |                                   Fast |　              Need |  Supported |                                    Need |
| Oracle      |                                   Fast |　              Need |  Supported |                                    Need |
| Ubuntu      |                                   Fast |　              Need |  Supported |                                    Need |
| Debian      |                                   Fast |　              Need |  Supported |                                    Need |
| Raspbian    |    1st time: Slow, From 2nd time: Fast |                Need |         No |                                    Need |
| FreeBSD     |                                   Fast |　                No |         No |                                    Need |
| Amazon      |                                   Fast |　              Need |  Supported |                                    Need |
| SUSE Enterprise |                               Fast |　                No |  Supported |                                    Need |

## With -offline option

-offline 옵션을 사용해서 vuls는 인터넷 액세스없이 스캔할 수 있다.

| Distribution|                             Scan Speed | Need Root Privilege |       OVAL | Need Internet Access|
|:------------|:--------------------------------------:|:-------------------:|:----------:|:---------------------------------------:|
| Alpine      |                                   Fast |　                No |  Supported |                                    No |
| CentOS      |                                   Fast |　              Need |  Supported |                                    No |
| RHEL        |                                   Fast |　              Need |  Supported |                                    No |
| Oracle      |                                   Fast |　              Need |  Supported |                                    No |
| Ubuntu      |                                   Fast |　              Need |  Supported |                                    No |
| Debian      |                                   Fast |　              Need |  Supported |                                    No |
| Amazon      |                                   Fast |　              Need |  Supported |                                    No |
| SUSE Enterprise |                               Fast |　                No |  Supported |                                    No |

오프라인 스캔 모드는 FreeBSD, Raspbian을 지원하지 않는다.

## Dependencies and /etc/sudoers

자세한 내용은 아래 문서 참조

- Dependencies: [usage-configtest](usage-configtest.md#fast-root-scan-mode)
- /etc/sudoers: [/etc/sudoers](usage-configtest.md#etc-sudoers)

## Runtime Inspection

### 다음 패키지 업데이트의 영향을받는 프로세스 감지

RedHat, CentOS, OracleLinux, Amazon Linux에서 yum-ps를 사용하여 소프트웨어 업데이트에 영향을 미치는 프로세스를 미리 알 수 있다.

### 다시 시작되지 않은 프로세스 탐지

Debian, Ubuntu에서 debian-goodies의 checkrestart를 사용하여 이전에 업데이트되었지만 아직 다시 시작되지 않은 프로세스 감지할 수 있다.
