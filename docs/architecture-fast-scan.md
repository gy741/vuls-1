---
id: architecture-fast-scan
title: Fast Scan
sidebar_label: Fast Scan
---

빠른 스캔 모드는 루트 권한과 종속성없이 스캔 대상 서버에 거의 부하가없는 스캔 모드이다.

![Vuls-Scan-Flow](/img/docs/vuls-scan-flow-fast.png)

| Distribution|                             Scan Speed | Need Root Privilege |       OVAL | Need Internet Access|
|:------------|:--------------------------------------:|:-------------------:|:----------:|:---------------------------------------:|
| Alpine      |                                   Fast |　                No |  Supported |                                     Need |
| CentOS      |                                   Fast |　                No |  Supported |                                     Need |
| RHEL        |                                   Fast |　                No |  Supported |                                     Need |
| Oracle      |                                   Fast |　                No |  Supported |                                     Need |
| Ubuntu      |                                   Fast |　                No |  Supported |                                     Need |
| Debian      |                                   Fast |　                No |  Supported |                                     Need |
| FreeBSD     |                                   Fast |　                No |         No |                                     Need |
| Amazon      |                                   Fast |　                No |  Supported |                                     Need |
| SUSE Enterprise |                               Fast |　                No |  Supported |                                       No |

빠른 스캔모드는 Raspbian를 지원하지 않는다.

## With -offline option

-offline 옵션을 사용해서 vuls는 인터넷 액세스없이 스캔할 수 있다.

| Distribution|                             Scan Speed | Need Root Privilege |       OVAL | Need Internet Access|
|:------------|:--------------------------------------:|:-------------------:|:----------:|:---------------------------------------:|
| Alpine      |                                   Fast |　                No |  Supported |                                    No |
| CentOS      |                                   Fast |　                No |  Supported |                                      No |
| RHEL        |                                   Fast |　                No |  Supported |                                      No |
| Oracle      |                                   Fast |　                No |  Supported |                                      No |
| Ubuntu      |                                   Fast |　                No |  Supported |                                      No |
| Debian      |                                   Fast |　                No |  Supported |                                      No |
| Amazo       |                                   Fast |　                No |  Supported |                                      No |
| SUSE Enterprise |                               Fast |　                No |  Supported |                                      No |

오프라인 모드는 FreeBSD, Raspbian를 지원하지 않는다.

## Dependencies and /etc/sudoers

자세한 설명 아래 문서 참조
- Dependencies: [usage-configtest](usage-configtest.md#fast-scan-mode)
- /etc/sudoers: [/etc/sudoers](usage-configtest.md#etc-sudoers)

