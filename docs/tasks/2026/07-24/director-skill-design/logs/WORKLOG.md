# Worklog

**2026-07-24**

- 기존 Codex 디렉터 세션과 독립 deep reasoning 분석을 바탕으로 별도 `codex-project-director` 정본을 시작했다.
- 첫 스킬 초안에 입장 분리, 상태 전이 기반 감독, 직접 구현 없는 작업자 복구, compact evidence와 조건부 durable state를 반영했다.
- 다음 작업은 실제 director 사례를 이용한 forward-test와 trigger 조정이다.
- Project Legibility 독립 정본들의 root와 README 공통 형태를 대조해 runtime tree를 skills/codex-project-director/로 옮기고, 한영 README와 skill companion, 설계 방향, MIT license, funding metadata와 최소 ignore를 추가했다. 공개 설치 문구는 release 전 상태에 맞게 보류했으며 빈 reference surface는 제거했다.
- 딥리즈너 분석과 사용자 관찰을 반영해 runtime을 explicit invocation, persistent Codex Goal, selective checkpoint monitoring, human-owned charter, ordered non-implementing recovery로 개정하고 110줄에서 86줄로 줄였다. 첫 읽기 전용 forward-test는 계약 정합성을 확인했지만 6문서 audit에 worker 셋과 28,157 tokens를 사용해, bounded outcome의 기본 owner를 한 명으로 제한하는 후속 교정을 만들었다.
- `tighten-docs`로 runtime, 설계 방향과 task 상태의 역할을 재확인하고 딥리뷰의 네 모호성을 최소 문구로 교정했다. 같은 결과의 Goal 재사용, 관찰 불가능한 event 부재의 checkpoint, 독립 evidence의 디렉터 직행, 현재 계획 조정과 재사용 규칙 승격의 구분을 한영 계약과 상태 템플릿에 동기화했다.
- 독립 검증에서 한영 runtime, 설계 방향, README, `openai.yaml`과 상태 템플릿의 계약 정합성을 확인했다. Skill 형식, project-context runtime shape, decision/worklog shape와 `git diff --check`가 모두 통과했다.
- 설계 토론의 비교 설명을 runtime과 현재 설계 방향에서 제거하고, 역할별 소유권과 실행 경계만 남겼다.
- 현재 main checkout의 runtime을 `$CODEX_HOME/skills/codex-project-director`에 로컬 설치하고 source와 설치본의 일치를 확인했다. `tighten-docs` 기준으로 README는 진입점과 배포 상태, 설계 문서는 원칙과 변경 gate, BRIEF는 현재 상태와 다음 forward-test만 소유하도록 압축했으며 source·설치본 skill 검증, project-context shape와 `git diff --check`가 통과했다.
- 실제 설치 세션 회고와 최소성 재검토를 거쳐 최신 사용자 승인 charter의 권한 우선순위와 첫 live harm의 mutation stop만 runtime에 승격했다. 사건별 taxonomy와 별도 token·Goal 절차는 제외했으며 한영 source와 로컬 설치본 동기화, 독립 의미 검토와 전체 형식 검증을 통과했다.
- `allow_implicit_invocation`을 활성화하고 natural-language role designation과 direct `$skill` invocation을 precise trigger에 함께 명시했다. 격리 forward-test에서 두 진입점, 단순 리뷰 exclusion, charter/live-harm guard가 통과했으며 첫 검사에서 발견한 direct-invocation 문언 불일치도 교정했다. 작은 synthetic director 검사 두 건이 12,225·6,294 tokens를 사용해 단일 국소 작업 exclusion과 실제 coordination-cost 검증 필요성을 확인했다.
- 공개 배포 승인에 따라 README 한영의 설치 진입점과 공개 상태를 갱신했다. Skill 형식, openai.yaml 정합성, 한영 runtime 의미, README 링크, project-context shape, source·로컬 설치본 일치, secret·절대경로 scan과 git diff hygiene를 독립 검증해 release blocker가 없음을 확인했다.
- GitHub 공개 저장소 `perhapsspy/codex-project-director`를 만들고 release 기준선 commit `5b7b44e`를 `main`에 push했다. 설치본이나 Project Legibility plugin cache는 변경하지 않았다.
