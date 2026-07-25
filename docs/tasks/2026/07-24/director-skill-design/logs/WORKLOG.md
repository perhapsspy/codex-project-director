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
- 반복된 event·checkpoint의 무진전을 감독 전략 점검으로 연결하고, 기존 control 하나의 가역적 변경과 다음 progress signal 판정을 runtime 한영과 설계 방향에 추가했다. 독립 검증에서 기존 charter·owner·monitoring·live-harm 경계와의 정합성을 확인했고, 격리 forward-test는 추가 agent 없이 상태 checkpoint를 통합 evidence checkpoint로 바꾸는 작은 조정으로 응답했다.
- 긴 director session의 지시 누락을 막는 Director State를 `project-context`와 독립된 runtime 계약으로 바꿨다. 기본 `docs/director-state.md`에는 `Goal`, `Now`, `Waiting`, `Constraints`의 현재 상태만 덮어쓰고 표·완료 이력·evidence·worker history는 제외했다. 딥리뷰에서 네 칸의 충분성을 확인하고 매 지시 전 재독 의무를 의미 있는 event 중심으로 낮췄으며 skill, project-context shape와 diff 검증을 통과했다.
- Director State의 네 heading을 runtime 계약 안에 직접 정의하고 기본 경로를 `docs/director-state.md`로 정리해 별도 asset을 제거했다. 현재 정본 문서의 `project-context`·Project Legibility 비교 표현은 최종 기능과 검증 gate를 바로 서술하도록 다듬었다.

**2026-07-25**

- 위험한 실행과 격리된 가역적 작업의 검증 주기를 분리하고, 작업 묶음 계약, 이정표 검토, 승인 사실별 정본 증거와 반복 실패 시 재정의를 한영 실행 계약에 통합했다. 첫 사전 검증에서 관련 범위 검증 생략과 검토 중복을 발견해 문구를 교정했고, 적대적·최소성·운영 관점의 검토 뒤 고정 횟수와 과도한 필드를 제거했다. 다섯 반례 사전 검증은 위험 관문 유지, 숨은 결합 직렬화, 최종 변경분 재검증, 모순 증거 차단과 영향받는 작업만 재정의하는 행동을 모두 선택했다.
- 실제 디렉터 사용에서 현재 역할 분리와 조정 흐름이 유용하다는 사용자 확인을 받았다. 설치본보다 최신인 작업 독립성·검증 주기·증거 소유 계약을 최종 후보로 동결하고, 한영 실행 계약, 공식 스킬 형식, project-context 작업 형태와 변경분 검사를 다시 통과시켜 Project Legibility 편입 준비를 마쳤다.
- 검토 결과가 승인 계약을 확장하고 사용자 교정 뒤 낡은 지시가 계속 실행된 사례를 세 관점으로 검토했다. 결함과 해법의 분리, 정확한 계약값 보존, 영향 작업만 중단·철회하고 담당자 확인 뒤 재개하는 경계를 한영 실행 계약과 설계 방향에 통합했으며 모든 새 구조 변경의 자동 중단과 전역 장벽은 제외했다. 독립 사전 검증과 실제 디렉터 세션은 잘못된 경로 작업과 폐기된 기준의 검토만 멈추고 정확한 계약 확인 뒤 기존 담당자 범위의 수정만 재개하면서 독립 조사·검증을 계속해 의도한 경계를 충족했다.
