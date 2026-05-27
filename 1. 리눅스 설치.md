# 1. 리눅스 설치

---

## 1. VirtualBox VM 생성

#### 1. 새로 만들기 클릭

#### 2. 이름 / 폴더 / ISO 이미지 설정

- 이름: `ora19c_single`
- ISO 이미지: `OracleLinux-R7-U7-Server-x86_64-dvd.iso`
- **무인 설치 건너뛰기 체크**

<img width="865" height="488" alt="image" src="https://github.com/user-attachments/assets/cf9b422a-5d6d-4fab-a2db-646a1d677e17" />

#### 3. 하드웨어 설정

- 메모리: `4096MB`
- CPU: `2`

<img width="864" height="488" alt="image" src="https://github.com/user-attachments/assets/4bd8d4ed-50eb-4c17-b305-4cbf0986bd67" />

#### 4. 디스크 크기 설정

- 크기: `50GB`

<img width="863" height="487" alt="image" src="https://github.com/user-attachments/assets/a56c6e25-3da1-4417-813e-e09dba303f83" />

<img width="431" height="242" alt="image" src="https://github.com/user-attachments/assets/c3c8a6b0-40a3-4e0f-98c9-9f14053f9e2d" />

#### 5. 속성 설정

- 포인팅 장치: `USB 태블릿`으로 변경

<img width="381" height="288" alt="image" src="https://github.com/user-attachments/assets/f3942bc1-2849-4e15-bb73-ae6999c956e2" />

#### 6. 네트워크 설정

- 어댑터 1: `어댑터에 브리지`

<img width="383" height="289" alt="image" src="https://github.com/user-attachments/assets/4676a3d5-680a-4ede-9e11-fd320010f7c8" />

---

## 2. Oracle Linux 7.9 설치

#### 1. VM 시작 후 Install Oracle Linux 7.9 선택

<img width="415" height="388" alt="image" src="https://github.com/user-attachments/assets/cb1cf052-e439-4b78-8449-30e9760117e8" />

#### 2. 언어 설정

- 한국어 선택

<img width="798" height="714" alt="image" src="https://github.com/user-attachments/assets/14bfb226-e452-4b64-a791-0c87b9b94f0b" />

#### 3. 소프트웨어 선택

- **서버 - GUI 사용** 선택
- 추가 기능:
  - 자바 플랫폼
  - KDE
  - MariaDB 데이터베이스 서버

<img width="465" height="391" alt="image" src="https://github.com/user-attachments/assets/0dc7a9c7-400b-4f59-92b7-85637c99f595" />

#### 4. 설치 대상

- 로컬 디스크 선택 후 완료

<img width="467" height="388" alt="image" src="https://github.com/user-attachments/assets/6e19fc72-a87d-4740-a3ef-6ecb81710988" />

#### 5. 네트워크 & 호스트 이름 설정

```
호스트 이름: ora19c
```

| 항목 | 값 |
|------|-----|
| 주소 | 172.31.xx.xx (실제 환경에 맞게 설정) |
| 넷마스크 | 255.255.0.0 |
| 게이트웨이 | 172.31.0.1 |
| DNS 서버 | 8.8.8.8 |

<img width="466" height="388" alt="image" src="https://github.com/user-attachments/assets/ac00f7b1-3fae-4330-a34e-952ebd8e833b" />
<img width="467" height="387" alt="image" src="https://github.com/user-attachments/assets/7b95930f-6ba9-4f77-bc70-ad26d1f501de" />

#### 6. ROOT 암호 및 사용자 생성

- root 암호: `oracle`
- 사용자 이름: `oracle` / 암호: `oracle`

<img width="935" height="776" alt="image" src="https://github.com/user-attachments/assets/4bfe4a18-fec2-4bd6-9f3c-40ea6bc3073a" />

<img width="932" height="776" alt="image" src="https://github.com/user-attachments/assets/5c7b88c3-269e-41ec-8b81-628c908b0644" />

#### 7. 설치 완료 후 재부팅

<img width="803" height="713" alt="image" src="https://github.com/user-attachments/assets/e55ccbbe-1571-4aa0-bd1b-ca7c1efa6c24" />

<img width="799" height="713" alt="image" src="https://github.com/user-attachments/assets/b83bba99-0287-4eca-a7e6-682b7c69c079" />

<img width="400" height="359" alt="image" src="https://github.com/user-attachments/assets/31932cce-6c0b-4cb8-a7f1-c6370e83b346" />

---

## 3. MobaXterm SSH 접속

설치 완료 후 MobaXterm으로 SSH 접속한다.

- Host: 설정한 IP
- Username: `root`
- Port: `22`

<img width="489" height="277" alt="image" src="https://github.com/user-attachments/assets/dbcaa7c1-c25b-43c3-b9a6-8dc1c05f5d9a" />

```bash
# 접속 확인
hostname
# ora19c

ip addr
# 설정한 IP 확인
```
