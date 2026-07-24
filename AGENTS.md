# AGENTS.md

- 이 저장소는 `codex-project-director` 스킬의 정본이다.
- 응답과 일반 문서는 한국어를 기본으로 작성한다.
- 장기 또는 재개 가능한 작업은 `project-context` 기준으로 `docs/tasks/`에 기록한다.
- 배포되는 계약은 `skills/codex-project-director/SKILL.md`가 소유한다.
- `SKILL.md`는 영어 정본, `SKILL.ko.md`는 frontmatter 없는 한국어 companion으로 유지한다.
- 디렉터 스킬은 작업자의 구현을 대신하지 않고 목표, 작업 간 계약, 증거, 복구와 handoff를 조정한다.
- 스킬과 상태 템플릿은 실제 director 세션의 시행착오로 검증한 뒤 일반 규칙으로 승격한다.
- 설치본이나 plugin cache를 직접 수정하지 않고 이 저장소를 먼저 변경한다.

## 역할 경계

- README는 소개, 현재 배포 상태, 사용 진입점, 지원과 라이선스 안내를 맡는다.
- `docs/skill-direction.md`는 설계 방향과 진화 기준을 맡는다.
- `docs/tasks/**`는 현재 작업 상태와 검증 기록을 맡고 runtime 계약이 되지 않는다.
- `skills/codex-project-director/`는 배포할 runtime 파일만 맡는다.

## 검증

- `python3 "$CODEX_HOME/skills/.system/skill-creator/scripts/quick_validate.py" skills/codex-project-director`
- `git diff --check`
