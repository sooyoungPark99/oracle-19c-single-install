# 2. Oracle 설치 사전 준비

---

## 1. SELinux / 방화벽 해제

```bash
# SELinux 비활성화
vi /etc/selinux/config
# SELINUX=enforcing → SELINUX=disabled 로 변경

# 방화벽 중지
systemctl stop firewalld
systemctl disable firewalld

reboot
```

---

## 2. /etc/hosts 설정

```bash
vi /etc/hosts
```

아래 내용 추가:

```
192.168.xx.xx  ora19c
```

---

## 3. 호스트명 변경

```bash
hostnamectl set-hostname ora19c
hostnamectl status
```

---

## 4. preinstall 패키지 설치

Oracle 19c 설치에 필요한 패키지와 커널 파라미터, 유저/그룹을 자동으로 설정해준다.

```bash
# 인터넷 연결 확인
ping -c 4 8.8.8.8

# preinstall 패키지 설치
yum -y install oracle-database-preinstall-19c
```

설치 완료 후 oracle 유저와 그룹이 자동 생성된다.

```bash
# 확인
id oracle
# uid=54321(oracle) gid=54321(oinstall) groups=54321(oinstall),54322(dba),...
```

---

## 5. oracle 유저 비밀번호 설정

```bash
passwd oracle
# oracle 입력
```

---

## 6. 디렉토리 생성 및 권한 설정

```bash
mkdir -p /u01/app/oracle/product/19.0.0/db_1
mkdir -p /u01/app/oraInventory

chown -R oracle:oinstall /u01
chmod -R 775 /u01
```

---

## 7. .bash_profile 설정 (oracle 유저)

```bash
su - oracle
vi ~/.bash_profile
```

아래 내용을 추가한다:

```bash
export ORACLE_BASE=/u01/app/oracle
export ORACLE_HOME=$ORACLE_BASE/product/19.0.0/db_1
export ORACLE_SID=orcl
export ORA_INVENTORY=/u01/app/oraInventory

export PATH=/usr/sbin:/usr/local/bin:$PATH
export PATH=$ORACLE_HOME/bin:$PATH

export LD_LIBRARY_PATH=$ORACLE_HOME/lib:/lib:/usr/lib
export CLASSPATH=$ORACLE_HOME/jlib:$ORACLE_HOME/rdbms/jlib

export NLS_DATE_FORMAT="RR/MM/DD"
export LANG=C
export LC_ALL=C

alias ss='sqlplus / as sysdba'
alias oh='cd $ORACLE_HOME'
```

```bash
source ~/.bash_profile

# 확인
echo $ORACLE_HOME
# /u01/app/oracle/product/19.0.0/db_1
```

---

## 8. 설치 파일 업로드

MobaXterm 또는 scp로 서버에 전송한다.

```bash
# Windows → Linux 서버로 전송
scp V1039330-01.zip oracle@192.168.xx.xx:/home/oracle/
```

전송 후 확인:

```bash
ls -lh /home/oracle/
# V1039330-01.zip 확인
```
