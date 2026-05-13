---
cve: CVE-____-____
title: "취약점 시나리오 제목"
summary: "취약점 원인, 영향, 실습 목표 요약"
scenario_goal: "attacker/victim 환경에서 학습자가 확인하고 조치해야 하는 목표"
alias: "통칭 또는 별명"
vulnerability_type: "예: 원격 코드 실행, 명령 주입, 역직렬화 취약점"
cwe: "예: CWE-78"
severity: "Critical | High | Medium | Low"
affected_product: "영향 제품과 취약 버전"
difficulty: "easy | medium | hard"
category: "rce | command-injection | deserialization | web"
attacker_service: "attacker"
victim_service: "victim"
victim_port: 8080
victim_internal_url: "http://victim:8080/취약경로"
target_url_env: "TARGET_URL=http://victim:8080/취약경로"
attacker_workdir: "/app"
attacker_entrypoint: "cd /app && python3 exploit.py"
fix_summary: "victim 컨테이너 또는 이미지에 적용해야 하는 수정/완화 요약"
verification_signal: "취약점 검증 성공 신호"
remediation_signal: "조치 후 성공 신호"
requires_rebuild: true
patch_mode: "container_runtime | image_rebuild"
readiness_check: "attacker/victim 컨테이너 내부 기준 준비 상태 확인 방법"
k8s_notes: "Kubernetes 변환 시 attacker/victim 역할, readiness, 포트, env, 볼륨 관련 참고"
references:
  - "https://example.com/reference"
evaluation_items:
  - "취약점 재현 성공 여부"
  - "attacker/victim 컨테이너 실행 맥락의 정확성"
  - "victim 조치 근거와 재검증 결과"
expected_actions:
  - "attacker 컨테이너에서 공격 명령 실행"
  - "victim 컨테이너에서 취약 상태 확인"
  - "victim 컨테이너에서 조치 또는 조치 가능성 확인 후 재검증"
---

# CVE-____-____ (취약점 이름)

> 이 README는 ScoreX가 시나리오 카드, 관리자 QA, 학습자 가이드를 자동 생성하기 위한 파싱 계약입니다.
> 모든 시나리오는 `attacker`와 `victim` 두 역할 컨테이너를 반드시 포함해야 합니다.

## 작성 규칙

- 상단 YAML front matter의 필수 값은 모두 실제 값으로 채웁니다.
- 실제 CVE README에는 `CVE-____-____`, `________`, `<...>` 같은 placeholder를 남기지 않습니다.
- `attacker_service`, `victim_service`는 `docker-compose.yml`의 서비스명과 정확히 일치해야 합니다.
- `scorex:*` 마커 안의 명령 블록에는 해당 컨테이너 내부에서 실행 가능한 명령만 작성합니다.
- `docker compose`, `docker exec`, `kubectl`, `helm`, `kompose` 같은 컨테이너 외부 명령은 ScoreX 명령 블록에 넣지 않습니다.
- 실제 영구 조치가 이미지 재빌드가 필요한 경우에도 `victim_fix_commands`에는 현재 victim 컨테이너 안에서 가능한 확인/정리 명령만 넣고, 재빌드 필요성은 `requires_rebuild`, `patch_mode`, `k8s_notes`에 명시합니다.

## 1. 취약점 개요

| 항목 | 내용 |
|------|------|
| CVE 번호 | CVE-____-____ |
| 통칭/별명 | 취약점 별명 |
| 취약점 유형 | 예: 원격 코드 실행 |
| CWE | 예: CWE-78 |
| 심각도 | Critical |
| 영향 제품/버전 | 영향 제품과 취약 버전 |
| 요약 | 취약점 원인과 영향 요약 |
| Cyber Range 목표 | attacker/victim 환경에서 확인해야 하는 목표 |

<!-- scorex:attacker_commands:start -->
```sh
cd /app
python3 exploit.py
```
<!-- scorex:attacker_commands:end -->

<!-- scorex:victim_verify_commands:start -->
```sh
cat /app/version.txt 2>/dev/null || echo "버전 파일 없음"
```
<!-- scorex:victim_verify_commands:end -->

<!-- scorex:victim_fix_commands:start -->
```sh
echo "현재 컨테이너에서 가능한 조치 또는 확인 명령을 작성합니다."
```
<!-- scorex:victim_fix_commands:end -->

<!-- scorex:post_fix_validation_commands:start -->
```sh
echo "조치 후 재검증 명령을 작성합니다."
```
<!-- scorex:post_fix_validation_commands:end -->

## Kubernetes 변환 힌트

- attacker 서비스: attacker
- victim 서비스: victim
- victim 포트: 8080
- attacker 유지 방식: exploit 실행 후 `tail -f /dev/null` 또는 대기형 entrypoint
- 패치 반영 방식: container_runtime 또는 image_rebuild

## 로컬 개발자 참고

```sh
docker compose up -d --build
docker compose logs -f attacker victim
docker compose down
```
