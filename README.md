# SEO Labs - Cyber Range Environment

## 📋 프로젝트 개요

이 프로젝트는 **교육 및 보안 연구 목적**을 위한 사이버 레인지(Cyber Range) 환경입니다. 실제로 발생했던 주요 보안 취약점들을 Docker 환경에서 안전하게 시뮬레이션하고, 각 취약점의 공격 메커니즘과 방어 방법을 학습할 수 있도록 구성되었습니다.

각 취약점은 **Victim(피해자)** 서비스와 **Attacker(공격자)** 서비스로 구성되어 있으며, Docker Compose를 통해 자동화된 공격 시나리오를 제공합니다.

---

## 🎯 포함된 취약점 목록

### 1. **CVE-2014-6271 (Shellshock)**
- **심각도**: Critical
- **유형**: Bash 환경 변수 명령 주입
- **대상**: Apache HTTP Server + Bash 4.3
- **공격 방식**: HTTP 헤더를 통한 환경 변수 주입
- **상세**: [`CVE-2014-6271/README.md`](CVE-2014-6271/README.md)

### 2. **CVE-2017-5638 (Apache Struts 2 S2-045)**
- **심각도**: Critical
- **유형**: OGNL 표현식 주입을 통한 원격 코드 실행
- **대상**: Apache Struts 2.3.31
- **공격 방식**: Content-Type 헤더에 악성 OGNL 페이로드 삽입
- **상세**: [`CVE-2017-5638/README.md`](CVE-2017-5638/README.md)

### 3. **CVE-2021-44228 (Log4Shell)**
- **심각도**: Critical
- **유형**: Log4j JNDI 조회를 통한 원격 코드 실행
- **대상**: Log4j 2.14.1
- **공격 방식**: JNDI LDAP 참조를 통한 악성 클래스 로드
- **상세**: [`CVE-2021-44228/README.md`](CVE-2021-44228/README.md)

### 4. **CVE-2022-22965 (Spring4Shell)**
- **심각도**: Critical
- **유형**: Spring Framework 데이터 바인딩 취약점
- **대상**: Spring Framework + Apache Tomcat
- **공격 방식**: ClassLoader 조작을 통한 웹쉘 업로드
- **상세**: [`CVE-2022-22965/README.md`](CVE-2022-22965/README.md)

### 5. **CVE-2025-55182 (React2Shell)**
- **심각도**: High
- **유형**: React Server Components 역직렬화 취약점
- **대상**: Next.js (React Server Components)
- **공격 방식**: 서버 액션을 통한 명령 실행
- **상세**: [`CVE-2025-55182/Readme.md`](CVE-2025-55182/Readme.md)

---

## 🏗 프로젝트 구조

```
seo-labs/
├── README.md                    # 이 파일 (전체 프로젝트 개요)
├── CVE-2014-6271/               # Shellshock
│   ├── README.md
│   ├── docker-compose.yml
│   ├── attacker/
│   │   ├── Dockerfile
│   │   └── exploit.py
│   └── victim/
│       ├── Dockerfile
│       └── test.cgi
├── CVE-2017-5638/               # Apache Struts 2
│   ├── README.md
│   ├── docker-compose.yml
│   ├── attacker/
│   │   ├── Dockerfile
│   │   └── exploit.py
│   └── victim/
│       └── Dockerfile
├── CVE-2021-44228/              # Log4Shell
│   ├── README.md
│   ├── docker-compose.yml
│   ├── attacker/
│   │   ├── Dockerfile
│   │   ├── exploit.py
│   │   └── Exploit.java
│   └── victim/
│       ├── Dockerfile
│       └── src/
├── CVE-2022-22965/              # Spring4Shell
│   ├── README.md
│   ├── docker-compose.yml
│   ├── attacker/
│   │   ├── Dockerfile
│   │   └── exploit.py
│   └── victim/
│       ├── Dockerfile
│       └── src/
└── CVE-2025-55182/              # React2Shell
    ├── Readme.md
    ├── docker-compose.yml
    ├── attacker/
    │   ├── Dockerfile
    │   └── exploit.py
    └── victim/
        ├── Dockerfile
        └── app/
```

---

## 🚀 빠른 시작

### 사전 요구사항

- **Docker Desktop** (Windows/Mac) 또는 **Docker Engine** (Linux)
- **Docker Compose** (일반적으로 Docker와 함께 설치됨)
- 최소 **4GB RAM** (각 환경마다 약 1-2GB 필요)

### 기본 사용법

1. **특정 취약점 환경 실행**:
   ```bash
   cd CVE-2014-6271
   docker-compose up -d --build
   ```

2. **공격 로그 확인**:
   ```bash
   docker-compose logs -f attacker
   ```

3. **환경 정리**:
   ```bash
   docker-compose down
   ```

### 각 취약점별 상세 가이드

각 취약점 폴더의 `README.md` 파일을 참조하세요:
- [`CVE-2014-6271/README.md`](CVE-2014-6271/README.md) - Shellshock
- [`CVE-2017-5638/README.md`](CVE-2017-5638/README.md) - Apache Struts 2
- [`CVE-2021-44228/README.md`](CVE-2021-44228/README.md) - Log4Shell
- [`CVE-2022-22965/README.md`](CVE-2022-22965/README.md) - Spring4Shell
- [`CVE-2025-55182/Readme.md`](CVE-2025-55182/Readme.md) - React2Shell

---

## 🔍 공통 아키텍처 패턴

모든 취약점 환경은 다음과 같은 공통 구조를 따릅니다:

### 1. **Victim 서비스**
- 취약한 애플리케이션을 실행하는 컨테이너
- 실제 취약점이 존재하는 소프트웨어 버전 사용
- 내부 네트워크(`cyber_range`)에서만 접근 가능

### 2. **Attacker 서비스**
- 자동화된 공격 스크립트를 실행하는 컨테이너
- 컨테이너 시작 시 자동으로 공격 시도
- Victim 서비스가 준비될 때까지 대기 후 공격 실행

### 3. **네트워크 격리**
- 모든 컨테이너는 `cyber_range` 브리지 네트워크에 연결
- 호스트 시스템과 격리되어 안전하게 실행
- 컨테이너 간 통신은 서비스 이름으로 수행

---

## 📚 학습 목표

이 프로젝트를 통해 다음을 학습할 수 있습니다:

1. **취약점 이해**
   - 각 CVE의 기술적 배경과 공격 메커니즘
   - 실제 공격 시나리오 시뮬레이션

2. **공격 기법**
   - 환경 변수 주입 (Shellshock)
   - OGNL 표현식 주입 (Struts 2)
   - JNDI 조회 공격 (Log4Shell)
   - 데이터 바인딩 조작 (Spring4Shell)
   - 역직렬화 공격 (React2Shell)

3. **방어 방법**
   - 각 취약점의 패치 방법
   - 보안 모범 사례

4. **실전 경험**
   - Docker 기반 환경 구성
   - 자동화된 공격 스크립트 작성
   - 로그 분석 및 디버깅

---

## ⚠️ 주의사항 및 면책 조항

### ⚠️ **중요 경고**

1. **교육 목적 전용**: 이 프로젝트는 **교육 및 보안 연구 목적**으로만 사용되어야 합니다.

2. **무단 사용 금지**: 
   - 프로덕션 시스템이나 승인되지 않은 시스템에서 사용 금지
   - 실제 서비스에 대한 공격 시도는 불법입니다

3. **격리된 환경에서만 실행**:
   - 모든 컨테이너는 격리된 네트워크에서 실행됩니다
   - 호스트 시스템에 직접적인 위험은 없지만, 주의 깊게 사용하세요

4. **책임 면제**:
   - 이 프로젝트의 오용으로 인한 모든 책임은 사용자에게 있습니다
   - 개발자는 어떠한 손해에 대해서도 책임을 지지 않습니다

### 🔒 보안 권장사항

- 프로덕션 환경에 배포하지 마세요
- 공용 네트워크에 노출하지 마세요
- 사용 후 반드시 `docker-compose down`으로 정리하세요
- 민감한 정보가 포함된 환경에서는 사용하지 마세요

---

## 🛠 문제 해결

### 일반적인 문제

1. **포트 충돌**:
   - `docker-compose.yml`에서 포트 매핑을 변경하세요
   - 다른 Docker 컨테이너가 같은 포트를 사용 중인지 확인하세요

2. **빌드 실패**:
   - Docker 이미지 캐시를 정리: `docker system prune -a`
   - 네트워크 연결 확인 (일부 이미지는 외부에서 다운로드)

3. **공격 실패**:
   - Victim 서비스가 완전히 시작될 때까지 충분히 대기했는지 확인
   - 각 폴더의 README에서 특정 문제 해결 방법 확인

4. **리소스 부족**:
   - Docker Desktop의 리소스 할당량 증가
   - 한 번에 하나의 환경만 실행

---

## 📖 추가 자료

### 공식 CVE 정보
- [CVE-2014-6271](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2014-6271)
- [CVE-2017-5638](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-5638)
- [CVE-2021-44228](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-44228)
- [CVE-2022-22965](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-22965)

### 관련 문서
- 각 취약점 폴더의 `README.md` 파일
- Docker 공식 문서: https://docs.docker.com/
- Docker Compose 문서: https://docs.docker.com/compose/

---

## 📝 기여

이 프로젝트는 교육 목적으로 개발되었습니다. 개선 사항이나 버그 리포트는 환영합니다.

---

## 📄 라이선스

이 프로젝트는 교육 목적으로 제공되며, 각 취약점의 원본 소프트웨어는 해당 라이선스를 따릅니다.

---

**⚠️ 다시 한 번 강조합니다: 이 프로젝트는 교육 및 보안 연구 목적으로만 사용하세요. 무단 사용은 불법이며 심각한 법적 문제를 야기할 수 있습니다.**

