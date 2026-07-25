# 사용자 가시 작업자 우선 경계

## Goal

- 디렉터가 내부 보조 에이전트로 사용자 가시 작업 세션을 대체하지 않도록 실행 담당 경계를 명확히 한다.

## Scope

- 정본 스킬의 한영 실행 계약과 설계 방향을 최소 범위로 맞춘다.
- 디렉터가 사용하는 내부 에이전트만 제한하고 다른 작업 세션의 자체 위임은 제한하지 않는다.

## Current Facts

- 현재 정본은 작업자의 책임을 정의하지만 사용자 가시 세션과 디렉터 내부 에이전트를 구분하지 않는다.
- 새 작업 세션은 사용자의 명시적 요청과 현재 도구 계약이 허용할 때만 시작할 수 있다.

## Current State

- 승인된 경계 문구를 정본에 반영했다. 형식 검사와 세 가지 독립 사전 검증이 통과했으며 Project Legibility 동기화는 정본 게시를 기다린다.

## Next Step

- 사용자 검토 후 정본을 게시하고 Project Legibility의 출처 잠금과 생성 묶음을 갱신한다.

## Working Boundary

- `skills/codex-project-director/`
- `docs/skill-direction.md`
- `docs/tasks/2026/07-26/visible-worker-ownership/`
