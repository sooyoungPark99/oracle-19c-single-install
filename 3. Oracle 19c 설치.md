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
<img width="1368" height="196" alt="image" src="https://github.com/user-attachments/assets/8f786d96-c722-4a05-b80f-1f1a74cae3c4" />

---

## 2. runInstaller 실행

```bash
cd $ORACLE_HOME
./runInstaller
```

> DISPLAY 환경변수가 설정되어 있어야 GUI가 실행된다.
> (MobaXterm은 자동으로 DISPLAY가 설정됨)

---

## 3. 설치 진행 (GUI)

#### 1. 구성 옵션 선택
- **소프트웨어만 설정** 선택 (DB는 DBCA로 별도 생성)

<img width="1195" height="948" alt="image" src="https://github.com/user-attachments/assets/a9ce2dfc-3813-4e37-be55-73f7e5f723dc" />

#### 2. 데이터베이스 설치 옵션
- **단일 인스턴스 데이터베이스 설치** 선택

<img width="1200" height="945" alt="image" src="https://github.com/user-attachments/assets/c058d305-1345-433e-93b5-9624daedf096" />

#### 3. 데이터베이스 에디션
- **Enterprise Edition** 선택

<img width="1196" height="948" alt="image" src="https://github.com/user-attachments/assets/cd8c2656-afcd-4118-aea7-dabb30d28eca" />

#### 4. Oracle 베이스 경로 확인
- `/u01/app/oracle` 확인

<img width="1195" height="946" alt="image" src="https://github.com/user-attachments/assets/7d6eca5c-78e1-47a9-9242-a8e4c98e32d1" />

#### 5. 인벤토리 경로 확인
- `/u01/app/oraInventory` 확인

<img width="1195" height="946" alt="image" src="https://github.com/user-attachments/assets/879ad437-e727-43db-8356-aacde58db14c" />

#### 6. 운영 체제 그룹
- Database Administrator (OSDBA): `dba`
- Database Operator (OSOPER): `oper`

<img width="1200" height="943" alt="image" src="https://github.com/user-attachments/assets/4097aeb0-6783-496f-9d99-0552dcd0a34a" />

#### 7. root 스크립트 자동 실행
- **자동으로 구성 스크립트 실행** 체크
- root 비밀번호: `oracle`

<img width="1198" height="946" alt="image" src="https://github.com/user-attachments/assets/a9012289-e2d1-42e0-8866-f1f91c1ecba4" />

#### 8. 필요 조건 검사
- 해결되지 않는 항목은 **모두 무시** 선택

<img width="1195" height="946" alt="image" src="https://github.com/user-attachments/assets/50c37e85-9008-495d-82c9-8305a62bfa9b" />

#### 9. 설치 완료 확인

```
설치 성공: Oracle Database 19c
```

<img width="1195" height="947" alt="image" src="https://github.com/user-attachments/assets/f74f1316-85f0-4d9d-be62-89a27db73b96" />

---

## 4. 설치 확인

```bash
# oracle 유저에서
# runInstaller 실행 후 환경변수 재적용
source ~/.bash_profile

which sqlplus
# /u01/app/oracle/product/19.0.0/db_1/bin/sqlplus

sqlplus -version
# SQL*Plus: Release 19.0.0.0.0
```
<img width="1005" height="221" alt="image" src="https://github.com/user-attachments/assets/03c97861-7ee6-4c49-8541-cd4c5a4f6db1" />
