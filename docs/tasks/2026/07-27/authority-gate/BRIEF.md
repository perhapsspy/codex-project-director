# 디렉터 권한 관문 보강

## Goal

- 디렉터의 구현 권한을 사용자 승인 경계에 고정하고, 승인된 작업은 과잉 감시 없이 사건 기반으로 끝까지 감독하도록 낮은 자유도의 계약을 둔다.

## Scope

- 한영 스킬의 권한 우선순위, 실행 전 사전 확인, 사건 기반 대기, 실행 유지·복구·분리·독립 이관 규칙을 함께 정리한다.
- 다른 제품 구현, push·release·설치·외부 배포는 제외한다.

## Current Facts

- `codex-project-director` 저장소가 스킬 내용의 정본이고 Project Legibility의 skill tree는 push된 정본 commit에서 생성되는 snapshot이다.
- 기존 `split an independent dependency`, Goal continuation과 idle recovery는 새 의존성을 승인된 변경 작업으로 오독할 여지가 있었다.
- 감독·계획·조사 승인과 mutation 권한을 분리하고, mutation에는 대상·영역·효과·담당자 네 필드가 모두 필요하다.
- 기존 감독 계약은 `RUNNING`의 만료 근거, 비종료 보고의 다음 사건, 반복 재개 지시 제한과 미완료 작업 중 감독 지속 여부가 모호했다.

## Current State

- 간결한 authorization record 중심 Authority Gate와 checkpoint 기반 사건 감독이 한영 정본과 설계 방향에 반영됐다.
- 권한·감독 대표 시나리오의 정적 계약 검사, skill 형식, diff 공백, task runtime shape, ChatGPT Pro 적대 리뷰와 후속 독립 리뷰가 통과했다.
- 변경은 로컬 정본에만 있으며 push·Project Legibility snapshot·version·publisher pin·설치본은 승인 범위 밖이라 갱신하지 않았다.

## Next Step

- 게시 승인을 받으면 정본을 검토·commit·push한 뒤 Project Legibility lock과 생성 snapshot을 정식 sync 절차로 갱신한다.

## Working Boundary

- `skills/codex-project-director/`
- `docs/tasks/2026/07-27/authority-gate/`
