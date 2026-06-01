# Vulhub 기반 시나리오 출처

일부 Cyber Range 시나리오는 [Vulhub](https://github.com/vulhub/vulhub) 저장소의 환경 설명·Dockerfile·재현 절차를 참고하여 `seo-labs`의 **victim + attacker + `cyber_range`** 패턴에 맞게 이식했습니다.

**구조 규약**: 아래 각 디렉터리는 다른 CVE와 동일하게 **`victim/`**(취약 서비스 이미지 빌드) + **`attacker/`**(공격 자동화) + 루트 **`docker-compose.yml`**(서비스명 `victim`, `attacker`)로 구성됩니다. Compose의 `depends_on`으로 attacker가 victim 기동 후에 올라갑니다.

## 라이선스

Vulhub 소프트웨어는 **MIT License**입니다. 전문:

- 원본: [vulhub/LICENSE](https://github.com/vulhub/vulhub/blob/master/LICENSE)
- 저작권 표기: `Copyright (c) 2017-present phith0n, https://vulhub.org`

신규 이식 시 **행 추가 절차**는 [docs/VULHUB-PORTING-CHECKLIST.md](docs/VULHUB-PORTING-CHECKLIST.md)의 마스터 표와 동일하게 유지합니다(체크리스트 `이식완료` ↔ 아래 표 반영).

이 레포에서 Vulhub를 참고한 디렉터리와 대응 원본 경로는 다음과 같습니다.

| seo-labs (victim/ + attacker/) | Vulhub 원본 경로 |
|--------------------------------|------------------|
| [CVE-2017-12615](CVE-2017-12615/) | [tomcat/CVE-2017-12615](https://github.com/vulhub/vulhub/tree/master/tomcat/CVE-2017-12615) |
| [CVE-2022-22963](CVE-2022-22963/) | [spring/CVE-2022-22963](https://github.com/vulhub/vulhub/tree/master/spring/CVE-2022-22963) |
| [CVE-2018-20062](CVE-2018-20062/) | [thinkphp/5.0.23-rce](https://github.com/vulhub/vulhub/tree/master/thinkphp/5.0.23-rce) |
| [CVE-2017-18349](CVE-2017-18349/) | [fastjson/1.2.24-rce](https://github.com/vulhub/vulhub/tree/master/fastjson/1.2.24-rce) |
| [CVE-2018-7490](CVE-2018-7490/) | [uwsgi/CVE-2018-7490](https://github.com/vulhub/vulhub/tree/master/uwsgi/CVE-2018-7490) |

MIT 조건에 따라 위 저작권 및 허가 문구를 복제·이용 시 포함하는 것을 권장합니다.
