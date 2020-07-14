---
id: install-manually
title: Install Manually
sidebar_label: Install Manually
---

## Install Requirements

### Linux Distributions
다음 예제는 CentOS, RedHat, Amazon Linux 등 (CentOS 및 Amazon Linux에서 테스트)을 포함한 Fedora 기반 Linux 배포에서 작동합니다.

### Packages
Vuls에는 다음 패키지가 필요하다.

- SQLite3, MySQL, PostgreSQL, Redis
- git
- gcc
- GNU Make
- Gi 버전은 v1.13 이상을 사용한다.(최신 버전 권장)
    - https://golang.org/doc/install

```bash
$ ssh <user>@<IP> -i ~/.ssh/private.pem
$ export latest_version=1.14.2 # Latest Go release as of writing
$ sudo yum -y install sqlite git gcc make wget
$ wget https://dl.google.com/go/go$latest_version.linux-amd64.tar.gz
$ sudo tar -C /usr/local -xzf go$latest_version.linux-amd64.tar.gz
$ mkdir $HOME/go
```

아래 내용을 `/etc/profile.d/goenv.sh`에 추가한다.(sudo 액세스 필요)

```bash
export GOROOT=/usr/local/go
export GOPATH=$HOME/go
export PATH=$PATH:$GOROOT/bin:$GOPATH/bin
```

OS 환경 변수를 현재 쉘로 설정한다.
```bash
$ source /etc/profile.d/goenv.sh
```
## Deploy go-cve-dictionary

[go-cve-dictionary](https://github.com/kotakanbe/go-cve-dictionary)

```bash
$ sudo mkdir /var/log/vuls
$ sudo chown <user> /var/log/vuls
$ sudo chmod 700 /var/log/vuls
$ mkdir -p $GOPATH/src/github.com/kotakanbe
$ cd $GOPATH/src/github.com/kotakanbe
$ git clone https://github.com/kotakanbe/go-cve-dictionary.git
$ cd go-cve-dictionary
$ make install
```
바이너리는 `$GOPATH/bin` 아래경로에 설치된다.

그런 다음 NVD에서 취약점 데이터를 가져온다.오십시오.
(AWS) 기준으로 10분 정도 소요된다.

```bash
$ cd $HOME
$ for i in `seq 2002 $(date +"%Y")`; do go-cve-dictionary fetchnvd -years $i; done
... snip ...
$ ls -alh cve.sqlite3
-rw-r--r--. 1 centos centos  51M Aug  6 08:10 cve.sqlite3
-rw-r--r--. 1 centos centos  32K Aug  6 08:10 cve.sqlite3-shm
-rw-r--r--. 1 centos centos 5.1M Aug  6 08:10 cve.sqlite3-wal
```


일본어로 결과를 얻으려면 JVN 취약점 데이터도 가져와야 한다.
(AWS) 기준으로 10분 정도 소요된다.

```bash
$ cd $HOME
$ for i in `seq 1998 $(date +"%Y")`; do go-cve-dictionary fetchjvn -years $i; done
... snip ...
$ ls -alh cve.sqlite3
-rw-r--r--. 1 centos centos  51M Aug  6 08:10 cve.sqlite3
-rw-r--r--. 1 centos centos  32K Aug  6 08:10 cve.sqlite3-shm
-rw-r--r--. 1 centos centos 5.1M Aug  6 08:10 cve.sqlite3-wal
```


## Deploy goval-dictionary

[goval-dictionary](https://github.com/kotakanbe/goval-dictionary)

```bash
$ mkdir -p $GOPATH/src/github.com/kotakanbe
$ cd $GOPATH/src/github.com/kotakanbe
$ git clone https://github.com/kotakanbe/goval-dictionary.git
$ cd goval-dictionary
$ make install
$ ln -s $GOPATH/src/github.com/kotakanbe/goval-dictionary/oval.sqlite3 $HOME/oval.sqlite3
```
바이너리는 `$GOPATH/bin` 아래경로에 설치된다.

그런 다음 검사 대상 서버가 CentOS이므로 Red Hat의 OVAL 데이터를 가져온다. [README](https://github.com/kotakanbe/goval-dictionary#usage-fetch-oval-data-from-redhat)

```bash
$ goval-dictionary fetch-redhat 7
```

다른 Linux 배포판을 검색하려면 OS 유형 및 검색 대상 서버 버전에 따라 OVAL 데이터를 미리 검색한다. 

- [Alpine](https://github.com/kotakanbe/goval-dictionary#usage-fetch-alpine-secdb-as-oval-data-type)
- [Red Hat, CentOS](https://github.com/kotakanbe/goval-dictionary#usage-fetch-oval-data-from-redhat)
- [Debian](https://github.com/kotakanbe/goval-dictionary#usage-fetch-oval-data-from-debian)
- [Ubuntu](https://github.com/kotakanbe/goval-dictionary#usage-fetch-oval-data-from-ubuntu)
- [Oracle Linux](https://github.com/kotakanbe/goval-dictionary#usage-fetch-oval-data-from-oracle)
- [SUSE](https://github.com/kotakanbe/goval-dictionary#usage-fetch-oval-data-from-suse)


## Deploy gost

[gost (go-security-tracker)](https://github.com/knqyf263/gost)
> Vuls 0.5.0 부터는 gost라는 새로운 데이터 소스를 사용하여 배포자가 패치를 게시하지 않은 취약점을 탐지 할 수 있다.


```bash
$ sudo mkdir /var/log/gost
$ sudo chown <user> /var/log/gost
$ sudo chmod 700 /var/log/gost
$ mkdir -p $GOPATH/src/github.com/knqyf263
$ cd $GOPATH/src/github.com/knqyf263
$ git clone https://github.com/knqyf263/gost.git
$ cd gost
$ make install
$ ln -s $GOPATH/src/github.com/knqyf263/gost/gost.sqlite3 $HOME/gost.sqlite3
```
바이너리는 `$GOPATH/bin` 아래경로에 설치된다.

 그런 다음 검색할 서버가 CentOS이므로 RedHat의 security tracker를 가져온다. [README](https://github.com/knqyf263/gost#fetch-redhat)

```bash
$ gost fetch redhat
```

Debian 보안 추적기를 가져오려면 다음을 참조하십시오. To fetch Debian security tracker, See [gost README](https://github.com/knqyf263/gost#fetch-debian)

## Deploy go-exploitdb

[go-exploitdb](https://github.com/mozqnet/go-exploitdb)
> Vuls 0.6.0 버전부터는 익스플로잇 코드를 표시 할 수있는 [Exploit DB.com] (https://www.exploit-db.com/) 데이터베이스가 추가되었다. 탐지 된 CVE의 익스플로잇 코드에 대해 알 필요가 없으면이 섹션을 건너 뛰세요.

```bash
$ sudo mkdir /var/log/go-exploitdb
$ sudo chown <user> /var/log/go-exploitdb
$ sudo chmod 700 /var/log/go-exploitdb
$ mkdir -p $GOPATH/src/github.com/mozqnet
$ cd $GOPATH/src/github.com/mozqnet
$ git clone https://github.com/mozqnet/go-exploitdb.git
$ cd go-exploitdb
$ make install
$ ln -s $GOPATH/src/github.com/mozqnet/go-exploitdb/go-exploitdb.sqlite3 $HOME/go-exploitdb.sqlite3
```
바이너리는 `$GOPATH/bin` 아래경로에 설치된다.

그런 다음 exploit-db 정보를 가져온다. [README](https://github.com/mozqnet/go-exploitdb#usage-fetch-and-insert-exploit)

```bash
$ go-exploitdb fetch exploitdb
```

`--deep` 옵션을 사용하면 많은 익스플로잇 정보를 얻을 수 있지만 오랜 시간이 걸린다.

## Deploy go-msfdb

[go-msfdb](https://github.com/takuzoo3868/go-msfdb)
>  Vuls 0.11.0 버전부터는 메타스플로이트 모듈을 표시할 수 있는 [Metasploit](https://github.com/rapid7/metasploit-framework) 데이터베이스가 추가되었다. 탐지된 CVE에 대한 메타스플로잇 모듈에 대해 알 필요가 없으면 이 섹션을 건너 뛰세요.

```bash
$ sudo mkdir /var/log/go-msfdb
$ sudo chown <user> /var/log/go-msfdb
$ sudo chmod 700 /var/log/go-msfdb
$ mkdir -p $GOPATH/src/github.com/takuzoo3868
$ cd $GOPATH/src/github.com/takuzoo3868
$ git clone https://github.com/takuzoo3868/go-msfdb.git
$ cd go-msfdb
$ make install
$ ln -s $GOPATH/src/github.com/takuzoo3868/go-msfdb/go-msfdb.sqlite3 $HOME/go-msfdb.sqlite3
```
바이너리는 `$GOPATH/bin` 아래경로에 설치된다.

그런 다음 msf-db 정보를 가져온다. [README](https://github.com/takuzoo3868/go-msfdb#usage-fetch-and-insert-modules-info)

```bash
$ go-msfdb fetch msfdb
```

## Deploy Vuls

```
$ mkdir -p $GOPATH/src/github.com/future-architect
$ cd $GOPATH/src/github.com/future-architect
$ git clone https://github.com/future-architect/vuls.git
$ cd vuls
$ make install
```
이전에 `vuls`를 설치했고 업데이트 하려는 경우 다음을 수행한다.
```
$ rm -rf $GOPATH/pkg/linux_amd64/github.com/future-architect/vuls/
$ rm -rf $GOPATH/src/github.com/future-architect/vuls/
$ cd $GOPATH/src/github.com/future-architect
$ git clone https://github.com/future-architect/vuls.git
$ cd vuls
$ make install
```

바이너리는 `$GOPATH/bin` 아래경로에 설치된다.

## Test Installation

[Local Scan Mode: From Configuration to Reporting](https://github.com/vulsdoc/vuls/blob/master/docs/tutorial-local-scan.md#step3-configuration)
