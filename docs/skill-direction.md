# 스킬 방향

## 목적

여러 Codex 작업이나 세션을 하나의 검증된 프로젝트 결과까지 이끄는 active non-implementing control plane을 제공한다.

## 설계 원칙

- 디렉터는 프로젝트 결과와 흐름을 능동적으로 소유하되 product code, 국소 구현과 디버깅은 맡지 않는다.
- 사용자가 현재 세션을 director나 supervisor로 명시 지정하면 자연어로 적용할 수 있고 `$codex-project-director`로도 직접 호출할 수 있다.
- 최신 사용자 승인 charter와 교정은 Goal, durable state와 모든 작업·검토 결과보다 우선하며 material departure에는 명시적 사용자 승인이 필요하다.
- 명시적으로 지정된 director session은 같은 프로젝트 결과의 Codex Goal 하나를 유지한다. Goal은 active continuation을, `project-context`는 세션 간 기억을 맡는다.
- 감독은 event에 반응하고, event의 부재를 관찰할 수 없을 때만 checkpoint를 둔다.
- 하나의 bounded outcome과 mutation surface에는 owner 한 명을 기본으로 둔다. 병렬 workstream은 독립 진행이나 독립 검증의 이익이 coordination 비용보다 클 때만 추가한다.
- blocker는 현재 owner 지원, bounded helper, 독립 workstream 분리, 명시적 owner 교체 순으로 복구한다.
- 완료는 compact evidence와 위험에 비례한 독립 검증으로 판단한다.
- Live harm의 첫 신뢰 가능한 증거가 나오면 해당 surface의 추가 mutation을 멈추고 승인된 복구 경로를 우선한다.
- 현재 계획은 evidence와 위험에 따라 즉시 조정하되, 재사용할 coordination rule은 반복 실패가 입증된 뒤에만 승격한다.

## 경계

- worker는 investigation, implementation, local debugging과 local verification을 소유한다.
- reviewer와 decision workflow는 독립 검증이나 고비용 결정을 별도로 맡길 가치가 있을 때만 사용한다.
- Project Legibility는 이 스킬의 검증 결과를 바탕으로 편입 여부를 판단하는 잠재 배포 대상이며 현재 정본이나 release owner가 아니다.

## 변경 기준

다음 실패가 실제 director session에서 재현될 때만 운영 계약을 바꾼다.

- Goal이 있는데도 continuation이 멈추거나 checkpoint가 과잉 polling으로 변한다.
- 복구 과정에서 구현 takeover, 동시 mutation owner 또는 불완전한 handoff가 발생한다.
- trigger·exclusion·evidence 계약 때문에 과잉 발동, 미발동 또는 잘못된 완료 판단이 반복된다.
- coordination 비용이 방지한 재작업보다 커진다.

변경은 이 독립 정본에서 먼저 forward-test한다. 이후 release와 Project Legibility 편입은 각각 별도 결정으로 다룬다.
