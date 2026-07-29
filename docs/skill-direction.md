# 스킬 방향

## 목적과 문서 역할

`codex-project-director`는 여러 Codex 과제나 세션을 하나의 검증된 프로젝트 결과까지 이끄는 능동적이고 비구현적인 control plane이다.

- `skills/codex-project-director/SKILL.md`: 영어 runtime 계약의 유일한 정본
- `skills/codex-project-director/SKILL.ko.md`: 같은 계약을 설명하는 한국어 companion
- 이 문서: runtime에 포함할 규칙의 기준과 회귀 범위

## 포함 기준

runtime에는 실제 세션에서 반복된 실패를 여러 상황에서 막는 최소 불변식만 둔다. 현재 저자유도 경계는 sourced completion gate, 효과별 권한, 겹치는 변경 영역의 단일 담당자, 사건 뒤 scheduler pass와 yield 조건, 반복 실패의 증거 우선 복구, 세션 컨텍스트의 비권위성과 Charter·State의 역할 분리다.

사례별 대상명, topology, 숫자 한도, 고정 테스트·review 절차는 runtime 규칙으로 승격하지 않는다. 다음 선택은 상황과 증거에 맞게 모델 또는 변경 담당자에게 맡긴다.

- 독립 lane 수와 WIP 배치
- 진단 방법과 instrumentation 형태
- acceptance claim에 맞는 테스트 범위와 review 깊이
- 승인된 권한 안의 branch, release, deploy 순서와 polling 방식
- 담당자의 파일·함수·harness·수정·재검증 선택
- 판단 컨텍스트의 유지 기간과 구현·검증 세션의 크기·재사용 여부

판단 연속성이 필요하면 컨텍스트를 유지하고, 구현·검증은 범위가 정해진 세션으로 분리할 수 있다. 이는 경제성 판단이지 runtime 의무가 아니다. 정확성은 세션의 길이나 새로움이 아니라 승인된 정본 인계 또는 명시된 지속성 한계, 변경 소유권과 바뀐 근거의 재도출로 보장한다.

## 진화와 회귀 기준

운영 계약은 반복 실패가 기존 불변식으로 막히지 않고, 더 작은 일반 계약이 재현 시나리오를 개선할 때만 바꾼다. 사례는 runtime에 누적하지 않고 회귀 fixture로 유지한다.

필수 회귀 시나리오는 다음 행동을 확인한다.

- 승인된 구현 → 출시 → 배포 → readback을 단계별 재승인 없이 이어감
- offline Edge가 있어도 owning fleet contract의 reachable 수렴과 queued work로 완료를 판단함
- causally changed revision에서 같은 실패가 반복되면 stage/class 증거 전까지 추정 배포를 멈춤
- focused test가 주장을 입증하면 finding이나 위험 변화 없이 full/race/re-review를 반복하지 않음
- owner 보고 뒤 다음 승인 tranche나 독립 read-only audit을 이어감
- 사용자 결정이 한 mutation만 막으면 다른 runnable lane을 계속함
- workspace branch 규칙을 independent child repository에 자동 상속하지 않음
- 부분적이거나 불명확한 live effect에는 영향 영역만 멈춤
- 조정 기록 쓰기가 승인되면 후속 세션이 이전 transcript 없이 정본 기록으로 재개함
- idle 세션의 governing source나 결정적 증거가 바뀌면 영향 작업만 다시 도출함
- 내부 변경 담당 세션을 회수해도 in-flight 또는 unknown effect가 있는 영역에 새 담당자를 배치하지 않음

변경은 정본 저장소 검증과 별도 배포 관문을 통과한다.
