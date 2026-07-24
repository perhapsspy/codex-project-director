# AGENTS.md

- 이 저장소는 `codex-project-director` 스킬의 정본이다.
- 응답과 일반 문서는 한국어를 기본으로 작성한다.
- 장기 또는 재개 가능한 작업은 `project-context` 기준으로 `docs/tasks/`에 기록한다.
- 배포되는 계약은 `codex-project-director/SKILL.md`가 소유한다.
- 디렉터 스킬은 작업자의 구현을 대신하지 않고 목표, 작업 간 계약, 증거, 복구와 handoff를 조정한다.
- 스킬과 상태 템플릿은 실제 director 세션의 시행착오로 검증한 뒤 일반 규칙으로 승격한다.
- 설치본이나 plugin cache를 직접 수정하지 않고 이 저장소를 먼저 변경한다.

## 검증

- `python3 /Users/pie/.codex/skills/.system/skill-creator/scripts/quick_validate.py codex-project-director`
- `git diff --check`
