# 3. Oracle 19c 설치

---

## 1. 설치 파일 압축 해제

Oracle 19c는 ORACLE_HOME 경로에서 직접 압축을 풀면 설치가 된다.

```bash
su - oracle

mv /home/oracle/LINUX.X64_193000_db_home.zip $ORACLE_HOME
cd $ORACLE_HOME

unzip LINUX.X64_193000_db_home.zip
```

압축 해제 후 확인:

```bash
ls $ORACLE_HOME
# bin, lib, network 등 디렉토리 확인
```

---

## 2. runInstaller 실행

```bash
cd $ORACLE_HOME
./runInstaller
```

> ⚠️ DISPLAY 환경변수가 설정되어 있어야 GUI가 실행된다.
> MobaXterm은 자동으로 DISPLAY가 설정된다.

---

## 3. 설치 진행 (GUI)

#### 1. 구성 옵션 선택
- **소프트웨어만 설정** 선택 (DB는 DBCA로 별도 생성)

#### 2. 데이터베이스 설치 옵션
- **단일 인스턴스 데이터베이스 설치** 선택

#### 3. 데이터베이스 에디션
- **Enterprise Edition** 선택

#### 4. Oracle 베이스 경로 확인
- `/u01/app/oracle` 확인

#### 5. 인벤토리 경로 확인
- `/u01/app/oraInventory` 확인

#### 6. 운영 체제 그룹
- Database Administrator (OSDBA): `dba`
- Database Operator (OSOPER): `oper`

#### 7. root 스크립트 자동 실행
- **자동으로 구성 스크립트 실행** 체크
- root 비밀번호: `oracle`

#### 8. 필요 조건 검사
- 해결되지 않는 항목은 **모두 무시** 선택

#### 9. 설치 완료 확인

```
설치 성공: Oracle Database 19c
```

---

## 4. 설치 확인

```bash
# oracle 유저에서
source ~/.bash_profile

which sqlplus
# /u01/app/oracle/product/19.0.0/db_1/bin/sqlplus

sqlplus -version
# SQL*Plus: Release 19.0.0.0.0
```
