# 4. DB 생성 및 접속 확인

---

## 1. orcl DB 생성 (DBCA)

```bash
dbca
```

#### 1. Create a database 선택

#### 2. Advanced configuration 선택

#### 3. Oracle Single Instance database 선택

#### 4. General Purpose 템플릿 선택

#### 5. 데이터베이스 정보 입력
- Global database name: `orcl`
- SID: `orcl`
- **컨테이너 DB(CDB) 체크 해제**

#### 6. 스토리지 설정
- Storage type: **File System** 선택
- Database files location: `/u01/app/oracle/oradata`

#### 7. Fast Recovery Area
- Recovery files location: `/u01/app/oracle/fast_recovery_area`
- Recovery area size: `10GB`

#### 8. 샘플 스키마 설치 체크 ← scott 유저 생성을 위해 반드시 체크

#### 9. 메모리 설정
- Memory management: **Automatic**
- Total memory: `1500MB`

#### 10. 비밀번호
- 모든 계정: `oracle`

#### 11. Finish 후 생성 완료 확인

---

## 2. clonedb DB 생성 (DBCA)

orcl 생성과 동일하게 진행하되 아래 항목만 변경한다.

- Global database name: `clonedb`
- SID: `clonedb`
- Total memory: `1000MB`

> 두 DB가 동시에 떠야 하므로 메모리를 나눠서 설정한다.

---

## 3. 기동 확인

```bash
ps -ef | grep pmon
# ora_pmon_orcl
# ora_pmon_clonedb
# 두 개 모두 확인
```

---

## 4. tnsnames.ora 확인 및 수정

```bash
vi $ORACLE_HOME/network/admin/tnsnames.ora
```

아래 내용이 있는지 확인하고 없으면 추가한다.

```
ORCL =
  (DESCRIPTION =
    (ADDRESS = (PROTOCOL = TCP)(HOST = 192.168.xx.xx)(PORT = 1521))
    (CONNECT_DATA =
      (SERVER = DEDICATED)
      (SERVICE_NAME = orcl)
    )
  )

CLONEDB =
  (DESCRIPTION =
    (ADDRESS = (PROTOCOL = TCP)(HOST = 192.168.xx.xx)(PORT = 1521))
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
      (ADDRESS = (PROTOCOL = TCP)(HOST = 192.168.xx.xx)(PORT = 1521))
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

```bash
# clonedb 접속
sqlplus sys/oracle@clonedb as sysdba
```

```sql
select instance_name, status from v$instance;
-- clonedb OPEN

exit;
```

---

## 7. tnsping 확인

```bash
tnsping orcl
tnsping clonedb
# 양쪽 모두 OK 나와야 한다
```

---

## 8. 방화벽 1521 포트 오픈

```bash
su -

firewall-cmd --permanent --add-port=1521/tcp
firewall-cmd --reload

# 확인
netstat -tlnp | grep 1521
```
