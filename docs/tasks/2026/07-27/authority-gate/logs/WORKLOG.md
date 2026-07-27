# 작업 기록

**2026-07-27**

- 정본·조립·publisher 저장소의 owner 경계와 clean 상태를 확인하고, 정본과 Project Legibility의 `main`을 fast-forward 동기화했다. 설치 cache는 배포 사본이므로 읽기만 하고 수정하지 않았다.
- 기존 스킬의 Goal continuation, 운영 순환의 split·recover·reassign, 독립 의존 작업 분리와 idle recovery가 mutation 권한 사전 확인 없이 이어지는 우회로임을 확인했다.
- Authority Gate를 한영 정본의 Goal 앞에 두고 모든 작업 생성·재개·복구·분리·재배정에 네 필드 사전 확인을 요구했다. 별도 운영 권한과 사용자 분리 시 완전한 감독 종료도 같은 우선순위에 연결했다.
- 정적 회귀 검토에서 승인된 Fielder 작업 중 reconciler gap 발견은 `NEEDS_DECISION`, “계속해”는 기존 Fielder만 재개, 독립 분리는 reconciler 감독 완전 종료로 판정됨을 확인했다. 과거의 무조건적인 dependency split과 Goal continuation 문구가 제거됐는지도 실패 조건으로 검사했다.
- skill quick validation, `git diff --check`, project-context runtime shape, Authority Gate 정적 계약 검사가 통과했다. Project Legibility 0.6.3의 offline lock·snapshot 무결성, bundle validation과 31개 repository test도 baseline으로 통과했다.
- 정본 변경은 아직 push되지 않아 Project Legibility의 lock·generated snapshot·manifest version과 publisher pin, 설치 cache는 변경하지 않았다. 이 사본들은 공개 정본 commit과 release commit이 생긴 뒤 각 룰북 절차로만 갱신한다.
- 적대 리뷰에서 초기 후보가 영문 정본을 34% 늘리고 부정 경계 표현을 18회에서 44회로 늘렸으며, latest instruction·owner 교체·분리 후 완료 판정에 모순이 생김을 확인했다. Authority Gate를 affirmative authorization record와 일치 행동의 정상 경로로 다시 써 증가 폭을 약 15%, 부정 경계 표현을 24회로 낮추고 하위 절의 중복 금지를 제거했다.
- 재작성본 독립 리뷰에서 분리 작업의 상태·완료 주장 종료 범위와 새 worker 요청 규칙의 중복 두 건을 발견해 한 문장 소유 경계와 Mission 정본으로 정리했다. 최종 재리뷰는 추가 finding 없이 A/B/C, 고위험 효과, continuation, owner 교체와 한영 의미 동등성을 승인했다. 최종 영문 정본은 기존 대비 약 15% 증가, 부정 경계 표현 23회다.
- ChatGPT Pro 적대 리뷰에서 세 필드의 “일치”를 완료 필요성이나 같은 저장소로 넓게 해석할 수 있는 우회로를 발견했다. 필드를 각 사용자 권한 근거와 독립 대조하고 모호한 적용을 `NEEDS_DECISION`으로 판정하도록 보강했다. 담당 이전은 기존 작업자로 제한하고, 레코드가 없을 수 있는 분리 대상을 명확히 했다. 후속 독립 리뷰에서는 서로 겹치는 제한 영역 전체를 한 소유 경계와 한 담당자로 묶고 Mission에 이미 있는 새 작업자 규칙의 반복을 제거했다.
- 실제 감독 실패와 ChatGPT Pro 검토를 바탕으로 `RUNNING`의 다음 사건·점검 시점, 묶음 event wait, 영향 작업 한 번 확인, 한 번의 같은 범위 재개 지시와 완료 전 감독 지속을 기존 운영 절에 통합했다. 판단 기반 checkpoint와 기존 `BLOCKED`·`NEEDS_DECISION` 전이를 사용했다.
- 후속 독립 리뷰에서 상태 보고만 반복해 `RUNNING`을 유지하는 우회로와 보고 없이 끝난 작업의 결과 회수 누락을 발견했다. 한 번의 재개 지시 뒤 상태 보고만 이어지면 `BLOCKED`로 정규화하고, 완료 사건에는 해당 작업을 한 번 읽어 남은 결과와 증거를 회수하도록 보강했다.
- 최종 독립 재리뷰는 두 우회로의 해소, 권한 관문 우선순위, 한영 의미 동등성과 간결성을 추가 finding 없이 승인했다.
- Edge 설치 사건을 ChatGPT Pro와 두 decision reasoner가 독립 검토했다. 새 규칙층 대신 기존 문장을 교체해 한 문장 제품 계약, 발견과 승인 밖 변경 제안의 분리, 외부 효과 기준 실패 복구, 실제 사용자 경로 증거와 담당자 수준 지휘를 반영하고 사건 회귀 시나리오를 추가했다. 최종 exact-text 재검토는 추가 P0/P1 없이 통과했다.
