# DI-1850 권한 경계 회귀

## Goal

- cross-repo 설계 조언과 과거 배포 지시가 새 저장소 변경·PR 권한으로 승격되는 경로를 닫는다.

## Scope

- `codex-project-director`의 권한 preflight, source-owner 선행 조건, 병렬화와 사용자 교정 복구를 보강한다.
- 제품 저장소 구현은 제외한다.
- 사용자 승인에 따라 정본 push, Project Legibility patch release, publisher catalog와 설치본 동기화까지 수행한다.

## Source

- `skills/codex-project-director/SKILL.md`가 영문 runtime 정본이다.
- Project Legibility snapshot과 설치 cache는 생성·배포 사본이다.

## Done

- 한영 계약과 방향 문서가 일치하고 DI-1850 정적 회귀 시나리오와 skill validator를 통과한다.
- 배포 snapshot과 marketplace pin, 설치본이 같은 release를 가리킨다.
