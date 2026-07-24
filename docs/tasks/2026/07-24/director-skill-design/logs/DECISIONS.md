# Decisions

**2026-07-24**

- **Background:** 같은 모델의 디렉터가 작업 세션 밖에서 방향 이탈, 계약 충돌과 회귀를 발견했지만 직접 구현할 때는 역할과 토큰 효율이 무너졌다.
- **Decision:** 디렉터를 목표·계약·흐름을 소유하는 active non-implementing control plane으로 정의한다.
- **Why:** 품질 이점은 모델 차이보다 서로 다른 입장과 실패 비용에서 나오며, 이를 유지해야 독립 판단이 가능하다.
- **Impact:** product code와 국소 디버깅은 작업자가 소유하고 디렉터는 결과·증거·통합만 판단한다.

**2026-07-24**

- **Background:** 막힌 작업자를 방치하지 않으면서 디렉터가 대신 구현하지 않는 복구 방법이 필요하다.
- **Decision:** 현재 작업자 지원, bounded helper 배정, 독립 의존성 분리, 명시적 owner 교체 순서로 복구한다.
- **Why:** 디렉터의 추진력을 유지하면서도 실행 입장으로 붕괴하지 않고 한 write/mutation owner를 보존할 수 있다.
- **Impact:** 디렉터가 직접 실행하는 대신 필요한 액션을 소유할 다른 작업자를 배정하고 기존 owner와의 경계를 명시한다.

**2026-07-24**

- **Background:** 아직 polling, 상태 유지와 role boundary 규칙이 실제 사용에서 안정화되지 않았다.
- **Decision:** 독립 source skill로 먼저 시험하고 Project Legibility 편입은 검증 뒤 판단한다.
- **Why:** 가역적인 실험으로 과잉 발동과 불안정한 운영 규칙의 조기 제품화를 피할 수 있다.
- **Impact:** 여러 프로젝트의 반복 사용, trigger 정확도, role collapse 방지와 coordination 비용을 편입 gate로 삼는다.

**2026-07-24**

- **Background:** 독립 정본이 Project Legibility 계열 스킬과 같은 저장소 역할 경계를 가져야 하지만 기존에는 runtime tree와 공개 진입면이 임시 형태였다.
- **Decision:** 배포 runtime을 `skills/codex-project-director/`에 두고 README 한영 pair, `docs/skill-direction.md`, LICENSE와 공통 funding metadata를 갖춘 canonical skill repository 형태를 사용한다.
- **Why:** README, 설계 방향, 작업 상태와 shipped contract의 owner를 분리하고 이후 Project Legibility 편입 시 불필요한 구조 이관과 공개 표면 누락을 줄일 수 있다.
- **Impact:** 빈 reference나 release 전용 구조는 만들지 않고 실제 forward-test가 요구할 때만 tests와 추가 resource를 도입한다.

**2026-07-24**

- **Background:** 실제 director 세션은 Goal이 없으면 능동적으로 이어지지 않았고, 반대로 무차별 중간 확인과 과도한 worker 분리는 토큰을 낭비했다.
- **Decision:** 명시적으로 호출된 director session은 프로젝트당 하나의 persistent Codex Goal을 liveness anchor로 사용하고, next event·checkpoint가 도래했거나 모호하거나 늦은 작업만 제한적으로 확인한다. Bounded outcome은 owner 한 명을 기본으로 둔다.
- **Why:** Goal은 active continuation을, project-context는 세션 간 기억을, next event와 checkpoint는 감독 대상을 제한해 missed idle과 과잉 polling을 함께 줄인다.
- **Impact:** Worker별 Goal, 고정 polling interval과 추가 상태 필드는 만들지 않으며, 병렬 workstream은 독립적인 critical-path 진행이나 독립 반증이 coordination 비용을 정당화할 때만 추가한다.

**2026-07-24**

- **Background:** 딥리뷰에서 관련 없는 active Goal, 관찰 불가능한 침묵, owner를 경유하는 독립 검증과 일회성 실패에 대한 대응이 runtime 계약에 모호하게 남아 있었다.
- **Decision:** 같은 결과의 Goal만 재사용하고, event 부재를 관찰할 수 없을 때 checkpoint를 두며, 독립 검증은 디렉터에게 직접 반환한다. 현재 계획은 evidence나 위험에 따라 즉시 조정하되 재사용 규칙은 반복 실패 뒤에만 승격한다.
- **Why:** 적극적인 진행과 효율적인 감시를 유지하면서 Goal 충돌, evidence 독립성 훼손과 첫 고위험 신호에 대한 늦은 대응을 막기 위해서다.
- **Impact:** 새 상태나 고정 절차는 추가하지 않고 기존 Goal, event, helper와 intervention 계약의 경계만 명확해진다.

**2026-07-24**

- **Background:** 문서 정합성 검토는 통과했지만 실제 설치 환경의 explicit invocation과 Goal-backed continuation 증거가 없었다.
- **Decision:** 공개 배포 전에 현재 main의 runtime을 로컬에 설치해 새 director session에서 forward-test한다.
- **Why:** 발견, 명시 호출, 지속 감독과 blocker 복구는 source 문서 검토만으로 검증할 수 없기 때문이다.
- **Impact:** 저장소가 계속 정본이며 로컬 설치본은 테스트 snapshot으로 취급한다. Project Legibility 편입과 공개 배포는 별도 결정으로 남는다.

**2026-07-24**

- **Background:** 실제 설치 세션에서 안전을 명목으로 사용자 합의를 확장하고 Goal·review 결과를 authority처럼 사용했으며, production 이상 뒤에도 forward mutation과 반복 검토를 이어간 실패가 발생했다.
- **Decision:** 최신 사용자 승인 charter가 Goal·durable state·작업·검토 결과보다 우선한다는 경계와 첫 live harm에서 affected surface의 mutation을 멈추는 경계만 runtime에 추가한다.
- **Why:** 두 문장이 charter drift, 잘못된 Goal 고착과 sunk-cost forward-fix의 공통 원인을 막으며 사건별 taxonomy, token 규칙이나 새 절차는 기존 계약과 중복된다.
- **Impact:** material departure는 명시적 사용자 승인이 필요하고, live harm 뒤에는 승인된 복구 경로를 우선하거나 추가 mutation 전에 사용자에게 묻는다.

**2026-07-24**

- **Background:** 사용자가 자연어로 현재 세션을 director나 supervisor로 명시 지정해도 `allow_implicit_invocation: false`에서는 `$skill` 직접 호출 없이는 runtime 주입을 보장할 수 없었다.
- **Decision:** precise trigger와 exclusion을 유지하면서 `allow_implicit_invocation`을 `true`로 바꿔 자연어 명시 지정을 허용한다.
- **Why:** 사용자 의도는 명시적이지만 제품 호출 방식은 implicit이며, 단일 국소 작업·리뷰·상태 요약 exclusion이 과잉 발동을 제한한다.
- **Impact:** 자연어 director 지정과 `$codex-project-director` 직접 호출을 모두 지원하며 실제 새 세션에서 발동·미발동 경계를 forward-test한다.

**2026-07-24**

- **Background:** 로컬 설치와 실제 director session 검증을 마쳤고 독립 정본을 다른 세션에서도 설치할 수 있는 공개 진입점이 필요하다.
- **Decision:** 현재 runtime과 문서를 `perhapsspy/codex-project-director` 공개 저장소의 첫 release 기준선으로 배포한다.
- **Why:** 독립 정본을 유지한 채 실제 사용 범위를 넓혀 Goal continuation, blocker 복구와 coordination 비용을 검증할 수 있다.
- **Impact:** README는 공개 설치 경로를 안내하며 Project Legibility 편입은 후속 검증 뒤 별도로 결정한다.
