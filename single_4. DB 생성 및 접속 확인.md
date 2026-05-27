# 4. DB 생성 및 접속 확인

---

## 1. orcl DB 생성 (DBCA)

```bash
dbca
```

#### 1. Create a database 선택

<img width="1197" height="948" alt="image" src="https://github.com/user-attachments/assets/0d02d7d6-a36f-4584-b623-6a9f6f312684" />

#### 2. Advanced configuration 선택

<img width="1197" height="948" alt="image" src="https://github.com/user-attachments/assets/ec7eccf2-e112-4fcf-a02d-507c1a0ef497" />

#### 3. Oracle Single Instance database 선택
#### 4. General Purpose 템플릿 선택

<img width="1197" height="948" alt="image" src="https://github.com/user-attachments/assets/a956e9de-2c33-4a45-a4ec-a4fbe56434aa" />

#### 5. 데이터베이스 정보 입력
- Global database name: `orcl`
- SID: `orcl`
- **컨테이너 DB(CDB) 체크 해제**

<img width="1197" height="948" alt="image" src="https://github.com/user-attachments/assets/a6f04ac7-1c49-419b-9b88-0b959c9da7af" />

#### 6. 스토리지 설정
- Storage type: **File System** 선택
- Database files location: `/u01/app/oracle/oradata`

<img width="1197" height="948" alt="image" src="https://github.com/user-attachments/assets/f2345198-c74e-4146-b376-44c861c2c68e" />

#### 7. Fast Recovery Area
- Recovery files location: `/u01/app/oracle/fast_recovery_area`
- Recovery area size: `10GB`

<img width="1197" height="948" alt="image" src="https://github.com/user-attachments/assets/541945f4-d235-402e-bdb0-29b03fba1098" />

#### 8. Network Configuration
- **Create a new listener 체크**
- Listener name: `LISTENER`
- Listener port: `1521`
> 리스너를 여기서 생성하지 않으면 DB 생성 후 외부 접속이 안 된다.

<img width="1197" height="948" alt="image" src="https://github.com/user-attachments/assets/9c9501e1-32b1-414e-84c3-e5ff9b5b8a7c" />

<img width="1196" height="941" alt="image" src="https://github.com/user-attachments/assets/064ad6c4-18e9-44d6-b3b3-5f5d43ec7e62" />

#### 9. 샘플 스키마 설치 체크 ← scott 유저 생성을 위해 반드시 체크

<img width="1196" height="941" alt="image" src="https://github.com/user-attachments/assets/1934c8e2-52c9-4280-81a3-bed620560325" />

#### 10. 메모리 설정
- Memory management: **Automatic**
- Total memory: `1500MB`

<img width="1196" height="941" alt="image" src="https://github.com/user-attachments/assets/776e2b41-f5e6-41e5-8a5d-18634d2a73b2" />

#### 11. Configure EM database express 체크 해제

<img width="599" height="473" alt="image" src="https://github.com/user-attachments/assets/521753a2-801e-4c52-b8b7-87118fc4439a" />

#### 12. 비밀번호
- 모든 계정: `oracle`

<img width="1195" height="947" alt="image" src="https://github.com/user-attachments/assets/7fda38f5-ee6c-4dc2-9507-e6be3915046a" />

#### 13. Finish 후 생성 완료 확인

<img width="1196" height="945" alt="image" src="https://github.com/user-attachments/assets/37a0c490-e830-455f-acb6-9e7c2a5494d1" />

<img width="1197" height="947" alt="image" src="https://github.com/user-attachments/assets/5f374790-0ce8-4472-becf-b22db90f7085" />

<img width="1197" height="945" alt="image" src="https://github.com/user-attachments/assets/d846130f-868b-4b81-9ca2-d61007654ec5" />

<img width="1195" height="943" alt="image" src="https://github.com/user-attachments/assets/bf3e35fe-7310-41c5-9a4f-5eef1c3e2e73" />

---
 
## 2. clonedb DB 생성 (DBCA)
 
orcl 생성과 동일하게 진행하되 아래 항목만 변경한다.
 
- Global database name: `clonedb`
- SID: `clonedb`

<img width="1199" height="947" alt="image" src="https://github.com/user-attachments/assets/0f9f533e-420f-40c5-abe5-aff019583d2f" />

#### Network Configuration
- 기존 LISTENER(1521) 가 목록에 표시되면 그대로 체크 후 Next
- 새로 생성할 필요 없음

<img width="1197" height="943" alt="image" src="https://github.com/user-attachments/assets/7debd05d-9ec6-49bb-890f-2c4a8e622ff5" />

- Total memory: `1000MB`
> 두 DB가 동시에 떠야 하므로 메모리를 나눠서 설정한다.

<img width="1199" height="947" alt="image" src="https://github.com/user-attachments/assets/c77c8ab9-e32f-40ce-bc8c-9e619c85e1bc" />

>  **[DBT-11214]** 오류 발생 시 Automatic Memory Management 대신
> Use Automatic Shared Memory Management를 선택한다.
> - SGA size: 700MB
> - PGA size: 300MB

<img width="1198" height="946" alt="image" src="https://github.com/user-attachments/assets/45c850bb-91d9-4807-8190-ac0233e4da66" />

---
 
## 3. 기동 확인
 
```bash
ps -ef | grep pmon
# ora_pmon_orcl
# ora_pmon_clonedb
# 두 개 모두 확인
```
<img width="1102" height="168" alt="image" src="https://github.com/user-attachments/assets/16397242-74f3-4450-8299-24ed98f5c241" />

---
 
## 4. tnsnames.ora 확인 및 수정
 
```bash
vi $ORACLE_HOME/network/admin/tnsnames.ora
```
 
아래 내용이 있는지 확인하고 없으면 추가한다.
 
```
ORCL =
  (DESCRIPTION =
    (ADDRESS = (PROTOCOL = TCP)(HOST = 172.xx.xx.xx)(PORT = 1521))
    (CONNECT_DATA =
      (SERVER = DEDICATED)
      (SERVICE_NAME = orcl)
    )
  )
 
CLONEDB =
  (DESCRIPTION =
    (ADDRESS = (PROTOCOL = TCP)(HOST = 172.xx.xx.xx)(PORT = 1521))
    (CONNECT_DATA =
      (SERVER = DEDICATED)
      (SERVICE_NAME = clonedb)
    )
  )
```
 
> HOST는 실제 서버 IP로 입력한다.
 
---
 
## 5. listener.ora HOST 수정
 
```bash
vi $ORACLE_HOME/network/admin/listener.ora
```
 
HOST를 실제 IP로 수정한다.
 
```
LISTENER =
  (DESCRIPTION_LIST =
    (DESCRIPTION =
      (ADDRESS = (PROTOCOL = TCP)(HOST = 172.xx.xx.xx)(PORT = 1521))
      (ADDRESS = (PROTOCOL = IPC)(KEY = EXTPROC1521))
    )
  )
 
SID_LIST_LISTENER =
  (SID_LIST =
    (SID_DESC =
      (ORACLE_HOME = /u01/app/oracle/product/19.0.0/db_1)
      (SID_NAME = orcl)
    )
    (SID_DESC =
      (ORACLE_HOME = /u01/app/oracle/product/19.0.0/db_1)
      (SID_NAME = clonedb)
    )
  )
```
 
```bash
lsnrctl stop
lsnrctl start
lsnrctl status
# orcl, clonedb 서비스 모두 확인
```

 <img width="1094" height="196" alt="image" src="https://github.com/user-attachments/assets/2dfd4997-f1c7-404b-a3f2-048c4d3152ea" />

---
 
## 6. 접속 확인
 
```bash
# orcl 접속
sqlplus sys/oracle@orcl as sysdba
```
 
```sql
select instance_name, status from v$instance;
-- orcl OPEN
 
exit;
```
<img width="1255" height="481" alt="image" src="https://github.com/user-attachments/assets/4b19eb06-2a4a-4a09-aae1-63618eb5fdf0" />
 
```bash
# clonedb 접속
sqlplus sys/oracle@clonedb as sysdba
```
 
```sql
select instance_name, status from v$instance;
-- clonedb OPEN
 
exit;
```
<img width="1165" height="429" alt="image" src="https://github.com/user-attachments/assets/e95fac87-f3e4-4607-96d7-0e80d222a3f8" />
 
---
 
## 7. tnsping 확인
 
```bash
tnsping orcl
tnsping clonedb
# 양쪽 모두 OK 나와야 한다
```
 
---
 
## 8. 방화벽 설정

방화벽이 비활성화된 경우 별도 설정 없이 접속 가능하다.

```bash
# 방화벽 상태 확인
systemctl status firewalld

<img width="1209" height="159" alt="image" src="https://github.com/user-attachments/assets/4c0dcdec-22f0-40e2-8368-fde1799fbce1" />

# 방화벽이 실행 중인 경우에만 아래 명령어 실행
firewall-cmd --permanent --add-port=1521/tcp
firewall-cmd --reload
```

> 2번 단계에서 방화벽을 비활성화했다면 이 단계는 생략한다.
