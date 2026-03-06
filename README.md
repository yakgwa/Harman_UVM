<div align="center">

<!-- logo -->
<img src="https://www.silverchips.co.kr/images/soc-verification.jpg" width="400"/> 

### Harman UVM 🖍️

[<img src="https://img.shields.io/badge/-readme.md-important?style=flat&logo=google-chrome&logoColor=white" />]() [<img src="https://img.shields.io/badge/release-v1.0.0-ㅎㄱㄷ두?style=flat&logo=google-chrome&logoColor=white" />]() 
<br/> [<img src="https://img.shields.io/badge/프로젝트 기간-2025.07.01~2026.01.26-fab2ac?style=flat&logo=&logoColor=white" />]()

</div> 

## 📝 About Verification : What is Systemverilog

### 왜 검증(Verification)이 이렇게 중요한가?
- 현대 반도체 설계에서 검증은 전체 개발 시간의 70% 이상
- 공정 미세화 + SoC 복잡도 증가 → 실리콘 재제작(Respins) 비용 폭증
- 한 번의 검증 실패 = 일정 지연 + 비용 폭탄
  
👉 따라서 “설계를 잘하는 것”보다 “틀리지 않았음을 증명하는 것”이 더 중요해짐
👉 즉,시뮬레이션 = 버그가 있다는 건 보여줄 수 있음, 검증 = 버그가 없다는 걸 최대한 논리적으로 증명하려는 시도​

### SystemVerilog는 왜 등장했는가?
1️⃣ 기존 Verilog의 한계
- 테스트벤치 작성에 부적합
- 랜덤 테스트, 자동화, 커버리지 개념 부족
- 대규모 SoC 검증에 비효율적

2️⃣ SystemVerilog의 정체
- 검증에 살아남은 방법들을 모두 모아놓은 언어
- 기존 Verilog + 객체지향(OOP) + 고급 데이터 타입 + Constraint Random + Automatic Verification + Coverage

3️⃣ SystemVerilog 검증의 핵심 컨셉 3가지
- Constrained Random Verification (CRV)
  - 사람이 모든 테스트 시나리오를 직접 작성 ❌
  - 제약 조건만 정의 → 나머지는 랜덤 생성
  - Corner case, 예상 못한 상황 발견에 매우 강력
  
📌 왜 유리할까?
- 블록 레벨에서는 “무슨 입력이 올지 모르는 상황”이 가장 위험
- Directed Test는 내가 생각한 것만 검증
- 즉, CRV는 Verification Engineer가 의미 있는 제약을 정의하고, 그 안에서 stimulus를 랜덤으로 생성해 설계를 검증하는 방법이다.
- 의미 있는 제약이란? 이 DUT가 가질 수 있는 의미 있는 상태 공간으로, Spec Behavior(기능, 정상 동작 시나리오), Corner Cases(경곗값, 불연속, 에러조건) 등을 기준으로 정의되는 제약이다.

- Automatic Verification 
  - 1️⃣ Golden Model
    - DUT의 이상적인 동작을 소프트웨어/모델로 구현
    - DUT 출력 ↔ Golden Model 결과 비교
    - 대량 자동 비교 가능
    - 👉 “정답지와 비교하는 방식”

  - 2️⃣ Assertion 
    - 시뮬레이션 중 조건이 깨지는 순간을 즉시 탐지
    - 상태 변화, 프로토콜 위반 감지에 강력(단, 기존 Verilog 문법과 성격이 너무 달라서 추가 학습이 필요)

  - 3️⃣ Coverage-driven Verification (CDV)
    - “테스트 많이 돌렸다” ❌
    - “우리가 검증 밀도를 높여, 검증해야 할 모든 경우를 실제로 다 돌렸는가?” ⭕
    - Coverage = 검증 진행률 + 완성도 지표 → 검증에 대한 정량적 지표 제공
    - 즉, Coverage를 기준으로 테스트를 생성·조정·종료하는 검증 방법론으로, 검증 진행 상황을 정량화하고 sign-off 기준을 제공
      ​
4️⃣ Verification Goals
- Functionality (SystemVerilog 존재 이유), Timing, Performance, Power, Physical effects(IR drop, crosstalk, 공정 변동성 등)
- SystemVerilog는 그 중에서도 기능 검증에 최적화된 언어라고 볼 수 있다.

5️⃣ Directed Test vs Constrained Random Test
- Directed Verification (전통적 방식)
  - 스펙 기반으로 테스트 케이스 직접 작성
  - 문제점: 설계 변경 시 테스트 전면 수정, “내가 준비한 경우만 잡힌다”
- Constrained Random Verification
  - 목표 영역만 정의
  - 나머지는 랜덤 + 자동 생성
  - Coverage로 검증 진행 상황 추적

6️⃣ Verification ≠ Simulation ≠ Testing

구분

의미

Simulation

파형을 돌려보는 행위

Testing

이 설계로 제조됐을 때, 불량 없이 동작하는가

Verification

이 모델이 내가 의도한 기능을 정확히 구현하는가

즉, Verification은 Testbench + Automatic Check + Coverage를 포함한 시스템으로 이해할 수 있다.

Verification Engineer ≠ Test Engineer

SystemVerilog / UVM → Verification

Scan, ATPG, BIST→ Testing

참고 : Manufacturing Test Flow

[ Scan ] - 테스트 가능성을 확보하는 구조
  내부 상태 접근 가능하게 함
        ↓
[ ATPG ] - 그 구조를 활용해 결함 검출 패턴 생성
  결함 드러내는 패턴 생성
        ↓
[ ATE 실행 ]
  실리콘 검사
        ↓
[ BIST (병행/대체) ] - 테스트를 칩 내부로 가져와 제조 테스트 효율을 높임
  내부에서 고속 자가 검사
​

7. SystemVerilog가 특히 유리한 지점

✅ 블록 레벨 / IP 레벨

입력 시나리오를 예측하기 어려움

랜덤 검증의 효율 극대화

❌ 시스템/소프트웨어 레벨

이미 시나리오가 정해진 경우가 많음

C/C++ 기반 검증이 더 효율적일 수 있음

​

8. UVM은 여기서 무엇인가?

SystemVerilog 위에서 돌아가는 "표준 검증 방법론 + 클래스 라이브러리"이다.

새로운 언어 ❌

SystemVerilog 코드 + 프레임워크

uvm_macros.svh를 include 해서 사용

간단한 검증 흐름 정리
 → Constrained Random Stimulus 생성
 → Golden Model / Assertion으로 Automatic Check
 → Functional Coverage로 Verication 완성도 판단
Verification Methodologies

여러 검증 방법 중에서 SystemVerilog는 Simulation 기반 기능 검증을 수행하기 위한 언어이다.

특히 다음과 같은 현대적 검증 기법들을 직접적으로 지원한다.

Constrained Random Verification

Functional Coverage

Golden Model / Assertion 기반 검증

다만 이는 SystemVerilog라는 ‘언어’에 초점을 둔 관점이며, 실제 반도체 설계 검증에서는 이보다 훨씬 다양한 검증 방법론(Verification Methodologies) 이 함께 사용된다. 이에 따라, 전체적인 검증 방법론의 큰 지도를 살펴볼 필요가 있다.

​

Simulation Technologies

시뮬레이션을 기반으로 한 검증 기법들 – Testbench가 핵심

RTL 또는 그 추상 모델을 실행하여 설계의 기능적 올바름을 검증하는 방식

​

1. Hardware Simulation

RTL/게이트 모델을 직접 시뮬레이션

Testbench가 중심 역할 수행

2. Event-driven Simulators

신호 변화(event)가 있을 때만 동작

불필요한 계산을 줄여 효율적

일반적인 RTL 기능 검증에 사용

3. Cycle-based Simulators

클록 엣지 단위로 한 사이클씩 동작

동기식 회로(synchronous design)에 적합

이벤트 정확도는 낮지만 속도는 빠름

4. Enhancing Simulation Speed

정확도 ↔ 속도 trade-off에 따라 RTL, BFM, ISS, C 등의 모델을 선택하는 전략 방법론

​

Rapid Prototyping & Emulation

1. Rapid Prototyping Systems

RTL과 실제 펌웨어(Object Code) 를 FPGA/ICE 환경에서 결합

실제 칩이 나오기 전에 HW/SW 통합 검증

Simulation 이후, 실리콘 이전 단계로서, 칩처럼 행동하는 시스템을 미리 만들어 검증하는 방법


2. Emulation Systems

대형 하드웨어 에뮬레이터 사용

RTL을 하드웨어로 가속 실행

대규모 SoC, 장시간 시나리오 검증에 사용

​

Static Technologies

시뮬레이션 없이 설계 문제를 찾아내는 기법들

​

1. Inspection

사람이 직접 검토하는 방식으로, 초기 단계에서 매우 효과적

1단계, Design Inspection : 사양, 아키텍처, 인터페이스 검토

2단계, Code Inspection : RTL 코드 리뷰

​

2. Lint Checking

툴을 이용한 RTL 분석.

Synthesizer의 preprocessor 역할

RTL purification (RTL DRC) : syntax 오류, semantic(의미) 오류

Rule-based checking : 기본 규칙 +  사용자 정의 규칙 체크

​

3. Static Timing Analysis (STA)

시뮬레이션 없이 타이밍 분석

입력 패턴 불필요

Worst-Case 기준

검증 항목 : Setup violation, Hold violation, Path delay, Clock skew 등

​

Physical Verification and Analysis

물리적 구현 관점의 검증

레이아웃 및 공정 수준에서의 검증 항목들:Timing, Signal Integrity, Crosstalk, IR drop, Electro-migration, Power analysis, Process antenna effects, Phase shift mask, Optical proximity, correction (OPC)

​

Formal Technologies

시뮬레이션 없이, 수학적·논리적으로 증명하는 검증

Formal Verification의 특징: 테스트벤치, 입력 벡터 없음, 결과는 증명 또는 반례

​

1. Theorem Proving

공리와 규칙을 이용한 수학적 증명

자동화 어려움, 종료 보장 없음

항공/우주, 의료, 군수 등 고신뢰 시스템에서 사용

​

2. Model (Property) Checking

모든 가능한 상태를 탐색

FSM, concurrent 시스템 대상

실무에서 가장 많이 사용되는 Formal 기법

​

3. Equivalence Checking

두 설계가 논리적으로 동일한지 확인

RTL ↔ Gate

CTS, Scan 삽입, ECO 이후 필수

Systemverilog(UVM)-Based Verification : 권장하는 Testbench 구조


1️⃣ Scenario 레벨 – Generator

🔹 Generator

무엇을 시험할지 결정

Transaction(패킷, 명령, 요청)을 생성

Constrained Random의 시작점

👉 여기서는 “read/write 섞어라”, “에러 상황도 포함해라” 같은 의도만 표현

📌 신호 타이밍 모름

📌 프로토콜 디테일 모름

​

2️⃣ Functional 레벨 – Agent / Scoreboard / Checker

🔹 Agent (중심 허브)

Generator에서 Transaction을 받음

Driver + Monitor를 묶은 개념

“이 인터페이스 담당자”

​

🔹 Scoreboard

Golden Model

“이 입력이면, 이 출력이 나와야 한다”를 계산

DUT 결과와 비교

​

🔹 Checker

규칙 기반 검사

순서, 일관성, 프로토콜 규칙 등

👉 “맞는 값인가?”뿐 아니라

👉 “맞는 방식으로 나왔는가?”

​

3️⃣ Command (=Signal) 레벨 – Driver / Monitor / Assertions

🔹 Driver

Transaction → 실제 핀 신호

타이밍, 핸드셰이크, 프로토콜 구현

​

🔹 Monitor

DUT 신호를 관찰

다시 트랜잭션 형태로 복원

Scoreboard / Checker로 전달

​

🔹 Assertions

DUT에 직접 붙어 있음

“이 순간 이 조건은 항상 성립해야 한다”

실시간 위반 감지

​

4️⃣ DUT (Design Under Test)

검증 대상 설계

Testbench와 명확히 분리됨

​

따라서 현대의 Testbench는 Constrainted Random 기반 Transaction-level Testbench로, 시나리오 수준에서 생성된 자극을 Driver가 신호로 변환하여 DUT에 인가하고, Monitor/Scoreboard/Asssertion을 통해 자동 검증하는 구조를 이룬다.
