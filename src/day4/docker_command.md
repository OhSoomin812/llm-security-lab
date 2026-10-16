# Docker 명령어 모음 — PostgreSQL 로컬 실행용

`simple_agent_postgre.ipynb`에서 쓰는 PostgreSQL을 로컬 설치 대신 Docker로 띄울 때 참고하는 명령어 모음입니다.
기존 로컬 PostgreSQL 설치에서 비밀번호를 분실했거나, 실습용으로 격리된 DB가 필요할 때 이쪽이 더 간단합니다.

## 0. 사전 준비

Docker Desktop이 설치되어 있고 실행 중이어야 합니다. 확인:

```powershell
docker --version
docker ps
```

## 1. 컨테이너 생성 및 실행

처음 한 번만 실행합니다. 이름·비밀번호·포트는 필요에 맞게 바꾸세요.

```powershell
docker run --name day4-postgres `
  -e POSTGRES_USER=postgres `
  -e POSTGRES_PASSWORD=postgres `
  -e POSTGRES_DB=postgres `
  -p 5432:5432 `
  -d postgres:17
```

| 옵션 | 의미 |
|---|---|
| `--name day4-postgres` | 컨테이너 이름 (다른 명령어에서 이 이름으로 지칭) |
| `-e POSTGRES_PASSWORD=...` | `postgres` 계정 비밀번호 — `.env`의 `POSTGRES_PASSWORD`와 맞춰야 함 |
| `-p 5432:5432` | `호스트포트:컨테이너포트`. 로컬에 이미 PostgreSQL이 떠 있어 5432가 쓰이는 중이면 `-p 5433:5432`처럼 호스트 쪽 포트를 바꾸세요 |
| `-d` | 백그라운드(detached)로 실행 |
| `postgres:17` | 이미지와 버전. 버전을 안 쓰면 `latest`가 받아집니다 |

포트를 바꿨다면 `.env`의 `POSTGRES_PORT`도 그 값으로 맞춰야 노트북에서 연결됩니다.

## 2. 상태 확인

```powershell
docker ps                      # 실행 중인 컨테이너 목록
docker ps -a                   # 멈춘 것까지 전부
docker logs day4-postgres      # 시작 로그 확인 (에러 났을 때 가장 먼저 볼 곳)
docker logs -f day4-postgres   # 실시간으로 로그 따라가기
```

## 3. 시작 / 중지 / 재시작

컨테이너를 한 번 만들고 나면, 다음부터는 삭제하지 말고 이 명령으로 켜고 끄면 됩니다 (데이터가 유지됩니다).

```powershell
docker stop day4-postgres
docker start day4-postgres
docker restart day4-postgres
```

## 4. 컨테이너 안에서 psql 직접 접속

로컬에 `psql`이 없어도, 컨테이너 안에 이미 들어있는 `psql`을 바로 쓸 수 있습니다.

```powershell
docker exec -it day4-postgres psql -U postgres
```

접속되면 평소처럼 SQL을 칠 수 있습니다.

```sql
\l              -- 데이터베이스 목록
\c postgres     -- 접속 DB 전환
\dt             -- 테이블 목록
SELECT * FROM personal_info;
\q              -- 종료
```

## 5. 비밀번호를 다시 바꾸고 싶을 때

로컬 설치와 달리 컨테이너는 환경변수로 비밀번호를 준 것이므로, 바꾸려면 컨테이너 안에서 직접 `ALTER USER`를 실행하면 됩니다.

```powershell
docker exec -it day4-postgres psql -U postgres -c "ALTER USER postgres PASSWORD '새비밀번호';"
```

## 6. 완전히 지우고 새로 시작하고 싶을 때

**데이터가 전부 사라집니다.** 실습용 더미 데이터가 아니라면 신중하게 실행하세요.

```powershell
docker stop day4-postgres
docker rm day4-postgres
# 이후 1번 명령으로 다시 생성
```

## 7. `.env` 설정값과의 연결

`simple_agent_postgre.ipynb`는 아래 환경변수를 읽습니다. 위 1번에서 만든 컨테이너 설정과 값이 일치해야 합니다.

```
POSTGRES_HOST=localhost
POSTGRES_PORT=5432
POSTGRES_DB=postgres
POSTGRES_USER=postgres
POSTGRES_PASSWORD=postgres
```

## 8. 자주 만나는 문제

| 증상 | 원인 | 해결 |
|---|---|---|
| `port is already allocated` | 로컬 PostgreSQL 서비스나 다른 컨테이너가 5432를 이미 씀 | `-p 5433:5432`처럼 호스트 포트를 바꾸고 `.env`의 `POSTGRES_PORT`도 맞추기 |
| `password authentication failed` | `.env`의 비밀번호와 컨테이너 생성 시 준 비밀번호가 다름 | 5번처럼 컨테이너 안에서 비밀번호를 다시 맞추거나, `.env`를 컨테이너 생성 당시 값으로 수정 |
| `connection refused` | 컨테이너가 꺼져 있음 | `docker ps -a`로 상태 확인 후 `docker start day4-postgres` |
| Windows에서 `docker` 명령을 못 찾음 | Docker Desktop이 꺼져 있거나 설치 안 됨 | Docker Desktop 실행 후 재시도 |
