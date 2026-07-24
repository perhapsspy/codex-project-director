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
