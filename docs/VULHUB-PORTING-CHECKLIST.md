# Vulhub 이식 마스터 체크리스트

Vulhub 시나리오를 `seo-labs`의 **Victim + Attacker + `cyber_range`** 패턴으로 옮길 때 사용하는 추적 표입니다. 한 행을 `이식완료`로 바꿀 때마다 아래 **이식 절차**를 한 세트 적용합니다.

## 골든 레퍼런스 (템플릿·문서 구조)

| 용도 | 경로 |
|------|------|
| YAML·ScoreX·작성 규칙 | [templates/README-CVE.ko.template.md](../templates/README-CVE.ko.template.md) |
| 본문 §1~§7 확장 예시 | [CVE-2014-6271/README.md](../CVE-2014-6271/README.md) |

## 중복·보류 규칙

- **중복-기존시나리오**: 동일 CVE·동일 공격 체인이 이미 `seo-labs`에 있으면 이식하지 않고 표에만 기록합니다. (예: Vulhub `struts2/s2-045` → [CVE-2017-5638](../CVE-2017-5638/).)
- **보류-리소스과다**: 다중 DB·클러스터 등 Compose가 과해 교육용 최소 구조로 줄이기 어려운 경우.
- **보류-법교육범위외**: 레포 교육 목적에 맞지 않거나 유지보수 리스크가 큰 경우.

## 이식 절차 (행을 `이식완료`로 올릴 때)

1. `CVE-xxxx-xxxxx/` 폴더 생성, **`victim/Dockerfile`** + **`attacker/{Dockerfile,exploit.py}`** + 루트 **`docker-compose.yml`** (`services`: `victim`, `attacker`; `depends_on: victim`; 네트워크 `cyber_range`).
2. 호스트 포트는 기존 시나리오와 겹치지 않게 **`28xxx`** 대역 사용 ([루트 README](../README.md) 문제 해결 절 참고).
3. **README**: 템플릿 YAML + ScoreX 네 블록 + CVE-2014-6271 스타일 §2~§7.
4. **[VULHUB-ATTRIBUTION.md](../VULHUB-ATTRIBUTION.md)** 표에 Vulhub 원본 경로 한 행 추가.
5. **[README.md](../README.md)** 취약점 목록·트리·MITRE(가능 시) 갱신.
6. **아래 마스터 표**에서 해당 행의 `seo-labs 상태`·`템플릿 점검` 열을 갱신.

## 템플릿 점검 열 (요약 기호)

각 이식 완료 행에 `템플릿 점검`에 다음을 한 줄로 적습니다.

`YAML | scorex×4 | v/a dirs | compose victim/attacker | ATTR행`

- **YAML**: front matter 필수 필드 채움
- **scorex×4**: attacker / victim_verify / victim_fix / post_fix_validation
- **v/a dirs**: `victim/`, `attacker/` 존재
- **compose**: 서비스명 `victim`·`attacker`
- **ATTR행**: VULHUB-ATTRIBUTION.md 반영

---

## 마스터 표

| Vulhub 경로 | 식별자 | seo-labs 상태 | seo-labs 디렉터리 | 템플릿 점검 | 비고 |
|-------------|--------|----------------|-------------------|-------------|------|
| tomcat/CVE-2017-12615 | CVE-2017-12615 | 이식완료 | CVE-2017-12615/ | YAML \| scorex×4 \| v/a \| compose \| ATTR | |
| spring/CVE-2022-22963 | CVE-2022-22963 | 이식완료 | CVE-2022-22963/ | 동일 | |
| thinkphp/5.0.23-rce | CVE-2018-20062 | 이식완료 | CVE-2018-20062/ | 동일 | |
| fastjson/1.2.24-rce | CVE-2017-18349 | 이식완료 | CVE-2017-18349/ | YAML \| scorex×4 \| v/a \| compose \| ATTR | JNDI+RMI |
| uwsgi/CVE-2018-7490 | CVE-2018-7490 | 이식완료 | CVE-2018-7490/ | YAML \| scorex×4 \| v/a \| compose \| ATTR | 경로 순회 |
| struts2/s2-045 | CVE-2017-5638 | 중복-기존시나리오 | CVE-2017-5638/ | — | OGNL S2-045 |
| spring/CVE-2022-22965 | CVE-2022-22965 | 중복-기존시나리오 | CVE-2022-22965/ | — | Spring4Shell |
| log4j/CVE-2021-44228 등 | CVE-2021-44228 | 중복-기존시나리오 | CVE-2021-44228/ | — | Log4Shell |
| tomcat/CVE-2020-1938 | CVE-2020-1938 | 미포함 | — | 미작성 | Ghostcat AJP |
| shiro/CVE-2016-4437 | CVE-2016-4437 | 미포함 | — | 미작성 | Remember Me |
| solr/CVE-2019-0193 | CVE-2019-0193 | 미포함 | — | 미작성 | 보류 후보 |
| redis/common | — | 미포함 | — | 미작성 | 무인증 등 |
| webmin/CVE-2019-15107 | CVE-2019-15107 | 미포함 | — | 미작성 | |
| activemq/CVE-2023-46604 | CVE-2023-46604 | 미포함 | — | 미작성 | |
| jenkins/CVE-2018-1000861 | CVE-2018-1000861 | 미포함 | — | 미작성 | |

> 표는 필요 시 행을 추가합니다. 로컬에 Vulhub 클론이 있으면 `**/docker-compose.yml` 목록을 뽑아 부록으로 확장할 수 있습니다.
