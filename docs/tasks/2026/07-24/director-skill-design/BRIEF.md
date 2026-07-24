# Goal

실제 Codex 디렉터 세션에서 확인된 장점과 실패를 바탕으로, 여러 작업을 프로젝트 완료까지 지휘하면서도 직접 구현·과잉 감시·과대 절차로 흐르지 않는 재사용 가능한 스킬을 만든다.

# Scope

- 디렉터, 작업자, 리뷰어의 입장과 책임을 분리한다.
- 상태 전이, 개입, 증거, 복구, handoff의 최소 운영 계약을 정한다.
- 독립 스킬로 시험한 뒤 Project Legibility 편입 여부를 판단한다.

# Current Understanding

- 디렉터의 효과는 상위 모델보다 목적 함수, 가시 범위, 행동 권한과 실패 비용이 다른 입장에서 나온다.
- 디렉터는 목표·우선순위·교차 계약·사용자 피드백·통합을 소유하고, 작업자는 국소 실행을, 리뷰어는 독립 반증을 소유해야 한다.
- `직접 구현하지 않음`은 수동 대기가 아니다. 미완료 idle과 blocker를 발견하면 현재 작업자를 돕고, 보조 작업자를 붙이고, 독립 의존성을 분리하거나, 명시적으로 새 owner에게 작업을 이전한다.
- 디렉터가 product code나 국소 디버깅을 직접 소유하면 역할 분리와 토큰 효율이 함께 무너진다.
- 감독은 고정 polling이 아니라 `RUNNING`, `WAITING`, `NEEDS_DECISION`, `BLOCKED`, `COMPLETE` 상태 전이에 반응해야 한다.
- durable state는 기존 `project-context`가 있으면 그것만 사용한다. 없을 때도 다단계 handoff나 session rotation이 실제로 필요한 경우에만 조건부 템플릿을 사용한다.

# Current State

독립 정본 저장소와 첫 스킬 초안, 조건부 상태 템플릿이 준비됐다. 아직 실제 director 요청에 대한 forward-test와 trigger 검증, 기존 세션 대비 행동 비교는 수행하지 않았다. Project Legibility 편입은 보류 상태다.

# Next Step

첫 초안을 실제 디렉터 사용 사례에 적용해 작업자 복구, role collapse, idle 처리, 증거 packet과 토큰 경계가 의도대로 작동하는지 forward-test하고 필요한 문장만 조정한다.

# Working Boundary

- `codex-project-director/SKILL.md`
- `codex-project-director/assets/director-state.md`
- `codex-project-director/agents/openai.yaml`
