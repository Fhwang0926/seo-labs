---
cve: CVE-____-____
title: "취약점 한글 제목"
summary: "취약점 원인과 실습 목표 요약"
scenario_goal: "attacker/victim 환경에서 학습자가 확인하고 조치해야 하는 목표"
alias: "통칭 또는 별명"
vulnerability_type: "예: 원격 코드 실행"
cwe: "예: CWE-78"
severity: "예: Critical"
affected_product: "영향 제품과 취약 버전"
difficulty: "easy | medium | hard"
category: "예: rce"
attacker_service: "attacker"
victim_service: "victim"
victim_port: 8080
victim_internal_url: "http://victim:8080/health 또는 취약 엔드포인트"
target_url_env: "TARGET_URL=http://victim:8080/취약경로"
attacker_workdir: "/app"
attacker_entrypoint: "attacker 컨테이너 내부에서 실행할 대표 공격 명령"
fix_summary: "피해자 컨테이너에서 적용할 수정/완화 요약"
verification_signal: "취약점 검증 성공 신호"
remediation_signal: "조치 후 성공 신호"
requires_rebuild: true
patch_mode: "container_runtime | image_rebuild"
readiness_check: "attacker 또는 victim 컨테이너 내부에서 확인 가능한 준비 상태 확인 방법"
k8s_notes: "Kubernetes 변환 시 attacker/victim 유지, readiness, 포트, 볼륨 관련 힌트"
references:
  - "https://example.com/reference"
evaluation_items:
  - "취약점 재현 성공 여부"
  - "공격자/피해자 컨테이너 실행 맥락의 정확성"
  - "조치 후 재검증 결과"
expected_actions:
  - "attacker 컨테이너에서 공격 명령 실행"
  - "victim 컨테이너에서 취약 상태 확인"
  - "victim 컨테이너에서 조치 후 재검증"
---

# CVE-____-____ (취약점 이름)

> 이 README는 ScoreX가 시나리오 카드를 자동 생성하기 위한 파싱 계약입니다.
> 모든 시나리오는 `attacker`와 `victim` 두 역할 컨테이너가 반드시 존재해야 합니다.

## 작성 규칙

- 상단 YAML front matter의 필수 값을 모두 실제 값으로 채웁니다.
- `CVE-____-____`, `________`, `〔...〕`, `<...>` 같은 placeholder를 남기지 않습니다.
- `attacker_service`, `victim_service` 값은 `docker-compose.yml`의 서비스명과 정확히 일치해야 합니다.
- ScoreX 마커가 붙은 명령 블록에는 **컨테이너 내부에서 실행 가능한 명령만** 넣습니다.
- ScoreX 마커 명령 블록은 POSIX `sh` 기준 셸 시퀀스를 그대로 보존합니다. `cd`, 변수 대입, 파이프라인, command substitution, `env`, `test`, `/bin/sh`, `/bin/bash` 같은 컨테이너 내부 명령을 사용할 수 있습니다.
- `docker compose`, `docker exec`, `kubectl`, `helm`, `kompose`, host shell 명령은 “로컬 개발자 참고” 섹션에만 둡니다.

## 1. 취약점 개요

| 항목 | 내용 |
|------|------|
| **CVE 번호** | CVE-____-____ |
| **통칭·별명** | 취약점 별명 |
| **취약점 유형** | 예: 원격 코드 실행 |
| **CWE** | 예: CWE-78 |
| **심각도** | 예: Critical |
| **영향 제품·버전** | 영향 제품과 취약 버전 |
| **요약** | 취약점 원인과 영향 요약 |
| **Cyber Range 목표** | attacker/victim 환경에서 학습자가 확인해야 하는 목표 |

### 영향 및 파급력

- **기밀성**:
- **무결성**:
- **가용성**:
- **네트워크 조건**:

### 참고 링크

- MITRE CVE:
- Vendor advisory:

## 2. 공격자(Attacker) 컨테이너 공격 절차

### 공격 전제

- attacker 서비스명:
- victim 서비스명:
- victim 내부 주소 또는 포트:
- 공격에 필요한 환경 변수:

### 공격 성공 신호

- 예: `/etc/passwd` 일부 출력, 특정 로그, 특정 HTTP 응답, 콜백 수신 등

<!-- scorex:attacker_commands:start -->
```sh
# attacker 컨테이너 내부에서 실행할 명령만 작성합니다.
# 예:
python3 exploit.py
```
<!-- scorex:attacker_commands:end -->

## 3. 피해자(Victim) 컨테이너 검증 및 조치

### 취약 상태 검증 신호

- 예: 취약 버전 출력, 취약 설정 확인, 공격 흔적 로그 확인 등

<!-- scorex:victim_verify_commands:start -->
```sh
# victim 컨테이너 내부에서 취약 상태를 확인하는 명령만 작성합니다.
# 예:
cat /app/version.txt
```
<!-- scorex:victim_verify_commands:end -->

### 수정/완화 방향

- 패키지 또는 프레임워크를 안전한 버전으로 업데이트합니다.
- 취약한 설정, 플러그인, 입력 처리 경로를 제거하거나 제한합니다.
- 컨테이너 내부 수정으로 끝나는지, 이미지 재빌드가 필요한지 명시합니다.

<!-- scorex:victim_fix_commands:start -->
```sh
# victim 컨테이너 내부에서 가능한 조치 명령만 작성합니다.
# 이미지 재빌드가 필요한 경우, 아래에는 현재 victim 컨테이너에서 가능한 확인/수정 명령만 쓰고
# 영구 반영 방식은 requires_rebuild/patch_mode/k8s_notes에 명시합니다.
sed -i 's/vulnerable/safe/g' /app/config.ini
```
<!-- scorex:victim_fix_commands:end -->

<!-- scorex:post_fix_validation_commands:start -->
```sh
# 조치 후 victim 컨테이너 내부에서 재검증하는 명령만 작성합니다.
grep safe /app/config.ini
```
<!-- scorex:post_fix_validation_commands:end -->

## 4. Kubernetes 변환 힌트

| 항목 | 값 |
|------|----|
| attacker 서비스 | attacker |
| victim 서비스 | victim |
| victim 포트 | 8080 |
| victim 내부 URL | http://victim:8080/취약경로 |
| attacker 작업 디렉터리 | /app |
| attacker 유지 방식 | 예: `sleep infinity` 또는 대기형 entrypoint |
| readiness 기준 | 예: victim HTTP 200 응답 |
| 필요한 env | 예: `TARGET_URL=http://victim:8080` |
| 필요한 volume | 없음 또는 경로 |
| 패치 반영 방식 | container_runtime 또는 image_rebuild |

변환 후 워크로드에는 다음 라벨이 붙어야 합니다.

```yaml
scorex.role: attacker
scorex.role: victim
```

## 5. 로컬 개발자 참고

이 섹션은 로컬 compose 재현용 참고입니다. ScoreX 관리자 QA와 웹 터미널 명령 파싱 대상이 아닙니다.

```sh
docker compose up -d --build
docker compose ps
docker compose logs -f attacker victim
docker compose down
```

## 6. 트러블슈팅

- attacker/victim 서비스명이 compose와 README에서 다르면 ScoreX는 보정 필요로 표시합니다.
- 필수 ScoreX 명령 블록이 비어 있으면 시나리오 카드는 보정 필요로 표시됩니다.
- 컨테이너 내부에 `bash`, `curl`, `ps` 같은 도구가 없을 수 있으므로 명령은 가능한 POSIX `sh` 기준으로 작성합니다.

## 7. 면책 조항

본 자료는 교육과 방어 역량 검증을 위한 격리된 Cyber Range 실습용입니다. 허가받지 않은 시스템에 사용하지 마십시오.
