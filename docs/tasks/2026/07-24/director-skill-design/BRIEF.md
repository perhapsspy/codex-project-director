# Goal

실제 Codex 디렉터 세션에서 확인된 장점과 실패를 바탕으로, 여러 작업을 프로젝트 완료까지 지휘하면서도 직접 구현·과잉 감시·과대 절차로 흐르지 않는 재사용 가능한 스킬을 만든다.

# Scope

- 디렉터, 작업자, 리뷰어의 입장과 책임을 분리한다.
- 상태 전이, 개입, 증거, 복구, handoff의 최소 운영 계약을 정한다.
- 실제 director session에서 trigger, continuation, recovery와 coordination cost를 검증한다.

# Current Understanding

- runtime 계약은 `skills/codex-project-director/SKILL.md`, 설계 방향과 변경 기준은 `docs/skill-direction.md`가 소유한다.
- 실제 설치 세션 회고에서 사용자 charter보다 Goal·검토 결과가 앞서는 문제와 live harm 뒤 forward mutation을 멈추는 경계가 부족한 것으로 확인됐다.
- runtime은 authority precedence와 live-harm stop의 공통 경계를 소유한다.
- 자연어로 director session을 명시 지정한 경우에도 적용되도록 precise trigger와 implicit invocation을 함께 사용한다.
- 작은 synthetic director 검증도 12,225·6,294 tokens를 사용했으므로 단일 국소 작업 exclusion과 coordination-cost 관찰이 중요하다.
- 반복된 event나 checkpoint에도 진전이 없을 때는 작업을 더 추가하기 전에 감독 전략을 작은 가역적 변경으로 시험하고, 세션 교훈은 검증 전까지 scoped hypothesis로 유지한다.
- Director State는 현재 작업 queue이며, 기본 위치는 `docs/director-state.md`다. `Goal`, `Now`, `Waiting`, `Constraints`만 덮어써 재독 비용을 제한한다.

# Current State

자연어 지정, `$skill` 직접 호출, 단순 리뷰 exclusion, charter 충돌, live-harm과 adaptive supervision forward-test가 통과했다. 최소 Director State는 형식·최소성 검토를 통과했고 실제 session 검증이 남아 있다.

# Next Step

실제 multiple-workstream director 사례에서 모든 중요한 사용자 지시가 짧은 Director State에 귀속되고 event마다 현재형으로 정리되는지 확인한다.

# Working Boundary

- `skills/codex-project-director/SKILL.md`
- `docs/skill-direction.md`
