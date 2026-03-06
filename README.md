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

<div align="center"><img src="https://github.com/yakgwa/Harman_UVM/blob/main/Picture/image_1.png" width="400"/>

<div align="left">

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

| 구분 | 의미 |
| :--- | :--- |
| **Simulation** | 파형을 돌려보는 행위 | XSIM 등 활용 |
| **Testing** | 제조 시 불량 없이 동작하는가 | Power/Temp 체크 |
| **Verification** | 의도한 기능을 구현했는가 | Accuracy 확인 |

- 즉, Verification은 Testbench + Automatic Check + Coverage를 포함한 시스템으로 이해할 수 있다.
- Verification Engineer ≠ Test Engineer
- SystemVerilog / UVM → Verification
- Scan, ATPG, BIST→ Testing

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
7️⃣ SystemVerilog가 특히 유리한 지점
- ✅ 블록 레벨 / IP 레벨
  - 입력 시나리오를 예측하기 어려움
  - 랜덤 검증의 효율 극대화
  - ❌ 시스템/소프트웨어 레벨
  - 이미 시나리오가 정해진 경우가 많음
  - C/C++ 기반 검증이 더 효율적일 수 있음

8️⃣ UVM은 여기서 무엇인가?
SystemVerilog 위에서 돌아가는 "표준 검증 방법론 + 클래스 라이브러리"이다.
- 새로운 언어 ❌
- SystemVerilog 코드 + 프레임워크
- uvm_macros.svh를 include 해서 사용

    간단한 검증 흐름 정리
     → Constrained Random Stimulus 생성
     → Golden Model / Assertion으로 Automatic Check
     → Functional Coverage로 Verication 완성도 판단
  
### Verification Methodologies
여러 검증 방법 중에서 SystemVerilog는 Simulation 기반 기능 검증을 수행하기 위한 언어이다.
특히 다음과 같은 현대적 검증 기법들을 직접적으로 지원한다.
- Constrained Random Verification
- Functional Coverage
- Golden Model / Assertion 기반 검증
- 다만 이는 SystemVerilog라는 ‘언어’에 초점을 둔 관점이며, 실제 반도체 설계 검증에서는 이보다 훨씬 다양한 검증 방법론(Verification Methodologies) 이 함께 사용된다. 이에 따라, 전체적인 검증 방법론의 큰 지도를 살펴볼 필요가 있다.

​✅ Simulation Technologies
- 시뮬레이션을 기반으로 한 검증 기법들 – Testbench가 핵심
- RTL 또는 그 추상 모델을 실행하여 설계의 기능적 올바름을 검증하는 방식

- 1️⃣ Hardware Simulation
  - RTL/게이트 모델을 직접 시뮬레이션
  - Testbench가 중심 역할 수행

- 2️⃣ Event-driven Simulators
  - 신호 변화(event)가 있을 때만 동작
  - 불필요한 계산을 줄여 효율적
  - 일반적인 RTL 기능 검증에 사용

- 3️⃣ Cycle-based Simulators
  - 클록 엣지 단위로 한 사이클씩 동작
  - 동기식 회로(synchronous design)에 적합
  - 이벤트 정확도는 낮지만 속도는 빠름

- 4️⃣ Enhancing Simulation Speed
  - 정확도 ↔ 속도 trade-off에 따라 RTL, BFM, ISS, C 등의 모델을 선택하는 전략 방법론

​✅ Rapid Prototyping & Emulation

- 1️⃣ Rapid Prototyping Systems
  - RTL과 실제 펌웨어(Object Code) 를 FPGA/ICE 환경에서 결합
  - 실제 칩이 나오기 전에 HW/SW 통합 검증
  - Simulation 이후, 실리콘 이전 단계로서, 칩처럼 행동하는 시스템을 미리 만들어 검증하는 방법

<div align="center"><img src="https://github.com/yakgwa/Harman_UVM/blob/main/Picture/image_2.png" width="400"/>

<div align="left">

- 2️⃣ Emulation Systems
  - 대형 하드웨어 에뮬레이터 사용
  - RTL을 하드웨어로 가속 실행
  - 대규모 SoC, 장시간 시나리오 검증에 사용

​​✅ Static Technologies
시뮬레이션 없이 설계 문제를 찾아내는 기법들

- 1️⃣ Inspection
  - 사람이 직접 검토하는 방식으로, 초기 단계에서 매우 효과적
  - 1단계, Design Inspection : 사양, 아키텍처, 인터페이스 검토
  - 2단계, Code Inspection : RTL 코드 리뷰

- 2️⃣ Lint Checking
  - 툴을 이용한 RTL 분석.
  - Synthesizer의 preprocessor 역할
  - RTL purification (RTL DRC) : syntax 오류, semantic(의미) 오류
  - Rule-based checking : 기본 규칙 +  사용자 정의 규칙 체크

- 3️⃣ Static Timing Analysis (STA)
  - 시뮬레이션 없이 타이밍 분석
  - 입력 패턴 불필요
  - Worst-Case 기준
  - 검증 항목 : Setup violation, Hold violation, Path delay, Clock skew 등

​​✅ Physical Verification and Analysis
  - 물리적 구현 관점의 검증
  - 레이아웃 및 공정 수준에서의 검증 항목들:Timing, Signal Integrity, Crosstalk, IR drop, Electro-migration, Power analysis, Process antenna effects, Phase shift mask, Optical proximity, correction (OPC)

✅ Formal Technologies
시뮬레이션 없이, 수학적·논리적으로 증명하는 검증
Formal Verification의 특징: 테스트벤치, 입력 벡터 없음, 결과는 증명 또는 반례

- 1️⃣ Theorem Proving
  - 공리와 규칙을 이용한 수학적 증명
  - 자동화 어려움, 종료 보장 없음
  - 항공/우주, 의료, 군수 등 고신뢰 시스템에서 사용

- 2️⃣ Model (Property) Checking
  - 모든 가능한 상태를 탐색
  - FSM, concurrent 시스템 대상
  - 실무에서 가장 많이 사용되는 Formal 기법
    
- 3️⃣ Equivalence Checking
  - 두 설계가 논리적으로 동일한지 확인
  - RTL ↔ Gate
  - CTS, Scan 삽입, ECO 이후 필수
  - Systemverilog(UVM)-Based Verification : 권장하는 Testbench 구조

<div align="center"><img src="https://github.com/yakgwa/Harman_UVM/blob/main/Picture/image_3.png" width="400"/>

<div align="left">

1️⃣ Scenario 레벨 – Generator
- 🔹 Generator
  - 무엇을 시험할지 결정
  - Transaction(패킷, 명령, 요청)을 생성
  - Constrained Random의 시작점
  - 👉 여기서는 “read/write 섞어라”, “에러 상황도 포함해라” 같은 의도만 표현
  - 📌 신호 타이밍 모름
  - 📌 프로토콜 디테일 모름

2️⃣ Functional 레벨 – Agent / Scoreboard / Checker
- 🔹 Agent (중심 허브)
  - Generator에서 Transaction을 받음
  - Driver + Monitor를 묶은 개념
  - “이 인터페이스 담당자”

- 🔹 Scoreboard
  - Golden Model
  - “이 입력이면, 이 출력이 나와야 한다”를 계산
  - DUT 결과와 비교

- 🔹 Checker
  - 규칙 기반 검사
  - 순서, 일관성, 프로토콜 규칙 등
  - 👉 “맞는 값인가?”뿐 아니라
  - 👉 “맞는 방식으로 나왔는가?”

3️⃣ Command (=Signal) 레벨 – Driver / Monitor / Assertions
- 🔹 Driver
  - Transaction → 실제 핀 신호
  - 타이밍, 핸드셰이크, 프로토콜 구현

- 🔹 Monitor
  - DUT 신호를 관찰
  - 다시 트랜잭션 형태로 복원
  - Scoreboard / Checker로 전달

- 🔹 Assertions
  - DUT에 직접 붙어 있음
  - “이 순간 이 조건은 항상 성립해야 한다”
  - 실시간 위반 감지

4️⃣ DUT (Design Under Test)
- 검증 대상 설계
- Testbench와 명확히 분리됨

따라서 현대의 Testbench는 Constrainted Random 기반 Transaction-level Testbench로, 시나리오 수준에서 생성된 자극을 Driver가 신호로 변환하여 DUT에 인가하고, Monitor/Scoreboard/Asssertion을 통해 자동 검증하는 구조를 이룬다.

## 📝 About Verification : Data Types

1️⃣Logic type
- 🔹 reg / wire → logic
  - SystemVerilog에서는 기존 Verilog의 reg와 wire를 logic 하나로 통합함.

    logic a, b;
    logic clk;
    logic rst_l;

- 🔹 logic의 사용 가능 범위
  - logic은 아래 모든 경우에서 사용 가능함.

✅ 변수 (procedural assignment)

    always @(posedge clk)
      q <= d;
      
✅ 연속 할당 (continuous assignment)

    assign rst_l = ~rst_h;
    
✅ gate / module 포트 연결

    my_module u0 (
      .clk(clk),
      .rst(rst_l)
    );
    
❗ 중요한 제한: 단일 드라이버(Single Driver)
- logic은 하나의 소스만이 신호를 구동할 수 있음.
- 즉, procedural + continuous, always 블록 여러 개 사용은 불가능하다.

    // ❌ 잘못된 예
  
        always @(*) a = b;
        assign a = c;   // multiple driver → 에러
  
2️⃣ Two-State Variables (2-state vs 4-state)
| 타입 | 상태 |
| :--- | :--- |
| **2-State** | **0, 1** |
| **4-State** | **0, 1, X, Z** |

- 🔹 대표적인 2-state 타입
  - bit
  - byte
  - int

- 🔹 장점과 단점
  - ✅ 장점
    - 시뮬레이션 빠름
    - 메모리 사용 적음

  - ❌ 단점
    - X, Z 표현 불가
    - 초기화/미정 상태 디버깅에 불리
    - 따라서 Verification에서는 잘 안 씀. RTL 동작 검증에는 4-State가 더 안전

    ⚠️ 주의점1
    
        byte b;
        //byte 범위는 -128 ~ 127로, 0~255 아님 (C랑 다름)
    
    ⚠️ 주의점2
    
        logic x;  // 4-state
        bit   y;  // 2-state
        y = x;    // x가 X/Z면 정보 손실 발생
        //4-state → 2-state 할당 시, X/Z가 0 또는 1로 강제 변환되므로, 디버깅 시 치명적
    
3️⃣ Declaration of Arrays

- 🔹 Fixed-size array

      int ascend[4] = '{0,1,2,3};
      int descend[5];
  
- 🔹 Multi-dimensional array

      int md[2][3] = '{'{0,1,2}, '{3,4,5}};

  - *array에서 '를 붙이는 이유
    - '{...}는 array/struct의 aggregate literal(집합 표기)이다. 즉, 의미적으로 {...}는 결과가 비트 벡터 하나로 합쳐지는 느낌(다시 말해, 비트들을 한 줄로 이어붙인 하나의 덩어리 값)이라면, '{...}는 원소 단위로 배열 또는 구조체에 맵핑되는 느낌으로 생각하면 된다.

  - Array Initialization 방법

        //전체 초기화
        integer descend = '{4,3,2,1,0};
        //부분 초기화
        integer descend[0:2] = '{5,6,7};
        //반복 값 초기화
        integer samearr = '{4{8}}; //{8,8,8,8}
      
      
  - Itertation에서 배열 활용 : for vs foreach
  
        //for : 인덱스를 직접 관리
        for (int i=0; i<$size(src); i++) 
          src[i] = i;
        
        //foreach : SystemVerilog 핵심. 배열 구조 기반 자동 반복
        integer md[2][3] = '{'{0,1,2}, '{3,4,5}};
        foreach (md[i,j])
          $display("md[%0d][%0d]=%0d", i, j, md[i][j]);
        //(i=0, j=0)→(i=0, j=1)→(i=0, j=2)→(i=1, j=0)→(i=1, j=1)→(i=1, j=2)
      
4️⃣ Dynamic Arrays
- 🔹 선언

      int dyn[], d2[];
      //크기 없음. 런타임에 결정된다.
  
- 🔹 할당 / 초기화
  
      dyn = new[5];        // 5개 할당
      foreach (dyn[j])
        dyn[j] = j;
  
- 🔹 확장 + Copy

      //기존 dyn에 이어서
      dyn = new[20](dyn);
      //이는 기존 새 dyn[0..4]는 이전 값이 복사되며, dyn[5...19]는 기본값으로 초기화된다. (예:int면 0)
  
- 🔹 완전 재할당
  
      dyn = new[100];  // 기존 데이터 전부 삭제됨
  
- 🔹 메모리 해제

        dyn.delete();
        //garbage collection(시뮬레이터가 메모리 회수)을 해주는 장치
        //다만, SystemVerilog는 시뮬레이션이 끝나면 어차피 정리되는데, delete를 왜 쓸까?
        //큰 dynamic array를 새로 계속 만들면 메모리가 커지기 때문에, new 이후 delete는 반드시 권장한다.
      
    - Queue 
    
          program test;
            initial begin
              int j = 11;
              int q[$] = {10, 12, 15};  //q[$]로 선언 시, insert, pop 등의 여러 queue 함수 사용 가능
          
              q.insert(1, j);   // {10, 11, 12, 15}
              q.delete(2);      // {10, 11, 15}
          
              foreach (q[i])
                $display(q[i]);
          
              q.push_front(16); // {16, 10, 11, 15}
              j = q.pop_back;   // q = {16, 10, 11}, j = 15
              q.push_back(17);  // {16, 10, 11, 17}
              j = q.pop_front;  // q = {10, 11, 17}, j = 16
          
              foreach (q[i])
                $display(q[i]);
            end
          endprogram
    
5️⃣ Associative Array
- 기존 배열과 다르게, 인덱스가 0,1,2 같은 연속된 숫자일 필요가 없는 대신, key→value 형태로 저장하는 배열을 말한다. 따라서 인덱스 타입을 본인이 정해서 쓰는 배열이라고 생각할 수 있다. (대부분의 원소 값이 0인 Sparse Matrix에서 특히 유리한데, 0인 칸을 전부 메모리 먹는 기존 fixed array와 달리, associative는 값이 있는 칸만 키로 저장하기 때문이다.)
- (단, 내부적으로 기존 fixed array보다 접근이 느릴 수 있다.)

      //Associative Array 선언 방법1
      logic [63:0] assoc[*];
      // [*]는 key 타입을 명시하지 않음(=도구가 알아서 처리)의 느낌으로 쓰는 형태로 선언할 수 있다.
      
      //Associative Array 선언 방법2
      int switch[string];
      // switch["min_addr"] = 10; 처럼 문자열이 배열 인덱스가 될 수 있다.

EX)

    logic [63:0] assoc[*], idx = 1;
    repeat (64) begin
      assoc[idx] = idx;
      idx = idx << 1;   //idx 2배
    end
    foreach (assoc[i])
      $display("assoc[%h] = %h", i, assoc[i]);
      
- Associative Array + foreach 
  - Synopsys VCS에서만 Associaitive에 대한 foreach 구문을 지원하기 때문에 보다 이식성 좋은 순회법이 필요하다.

        if (assoc.first(idx)) begin
          do
            $display("assoc[%h]=%h", idx, assoc[idx]);
          while (assoc.next(idx));
        end
        
        assoc.first(idx);
        assoc.delete(idx);
    
  - EX)

        int switch[string], min_address, max_address;
        initial begin
          int i, r, file;
          string s;
          file = $fopen("switch.txt","r"); //switch.txt를 read 모드로 읽어옴
        
        //파일 끝까지 반복해서 읽기
          while (!$feof(file)) begin //파일을 모두 읽으면 $feof(file)=1
            r = $fscanf(file, "%d %s", i, s); //$fscanf로 파일에서 문자열을 읽어 파싱 및 변수에 넣음
                                              //%d : 정수 하나 읽어서 i에 저장
                                              //%s : 공백 전까지 문자열 읽어서 s에 저장
                                              //반환값 r은 "성공적으로 읽어 넣은 항목 개수"
           //예컨대, 파일 한 줄이 12 min_address라고 해보자. i=12, s="min_address", r=2
            switch[s] = i;
          end
          $fclose(file);
        
        //"min_address" 꺼내기
          min_address = switch["min_address"];
        
        //"max_address"꺼내기
          if (switch.exists("max_address"))
            max_address = switch["max_address"];
          else
            max_address = 1000;
        
- Array Reduction 예시 - 배열에 대해 .sum, .product와 같은 리덕션(요약) 메소드 제공
  - .sum, .product, .and, .or, .xor

        bit on[10];   // 1비트짜리 원소 10개짜리 배열
        int summ;     // 32비트 signed 정수
        
        initial begin
          foreach (on[i])
            on[i] = i;         // on[i]는 0 or 1
        // on = {0,1,0,1,0,1,0,1,0,1}
        
          $display("on.sum = %0d", on.sum);  // on.sum = 5
        
          summ = on.sum;
          $display("summ = %0d", summ);      // summ = 5
        
          if (on.sum >= 32'd5)               // True
            $display("sum has 5 or more 1's");
        end
    
| i | 이진 | on[i]에 저장되는 값 (LSB) |
| :---: | :---: | :---: |
| **0** | **0000** | **0** |
| **1** | **0001** | **1** |
| **2** | **0010** | **0** |
| **3** | **0011** | **1** |
| **4** | **0100** | **0** |
| **5** | **0101** | **1** |
| **6** | **0110** | **0** |
| **7** | **0111** | **1** |
| **8** | **1000** | **0** |
| **9** | **1001** | **1** |

- Array Locator 예시 - 배열에 대해 .min, .max와 같은 로케이터 메소드 제공
  - .min, .max, .unique, sum with

      tq = q.min;      // 최소값
      tq = q.max;      // 최대값
      tq = f.unique;   // 중복 제거(유일한 값들)
      count = d.sum with (item > 7); //d 배열 원소를 돌면서, 조건을 만족하는 원소 대상으로 sum
      
  - EX) find 

        program test;
          initial begin
            int d[] = '{9, 1, 8, 3, 4, 4}, tq[$];
            tq = d.find with (item >3); //{9,8,4,4}
            foreach(tq[i])
            $display(tq[i]);
          end
        endprogram
        
        //find 계열 구문 추가 예시
        tq = d.find_index with (item > 3);  // {0,2,4}, 값 말고 인덱스를 찾는다.
        tq = d.find_first with (item > 99);   // {} 없음, 조건을 만족하는 첫 값 
        tq = d.find_first_index with (item==8); // {2}, 조건을 만족하는 첫 번째 인덱스
        tq = d.find_last with (item==4);        // {4}, 조건을 만족하는 마지막 값
        tq = d.find_last_index with (item==4);  // {5}, 조건을 만족하는 마지막 인덱스

6️⃣ typedef, parameter

typedef, parameter는 define과 다르게, 컴파일러가 의미를 이해하여 심볼 테이블에 등록하고, 중복이 발생 할 경우에는 에러를 띄움으로써 언어 차원에서 타입/상수로 관리한다.

    parameter OPSIZE = 8;
    typedef reg [OPSIZE-1:0] opreg_t;
    
    opreg_t op_a, op_b;
    
- 'define 매크로가 위험한 이유

      `define x a+b
      `define y c*x
      //하지만 일반적인 컴파일러는 이를 문자열 치환으로 처리하므로
      //y  →  c*a+b
      //즉, 우리가 기대한 c*(a+b)가 아니다.
      //따라서 'define 사용 시, 반드시 괄호를 사용하는 것이 관례이다.
  
7️⃣ sturct, packed struct, union

    //1. struct : 각 필드는 독립된 메모리로서, C언어에서의 구조체와 거의 동일하다.
    typedef struct {
      bit [7:0] r;
      bit [7:0] g;
      bit [7:0] b;
    } pixel_s;
    
    //2. struct packed //전체가 하나의 연속된 비트 벡터
    //아래의 예시는 총 24bit → [23:0] 레지스터 하나로 매핑가능하다.
    //특히, 하나의 레지스터에 비트를 묶음별로 다르게 사용하는 IP 관점에서 struct packed 타입이 유리하다.
    typedef struct packed {
      bit [7:0] r;
      bit [7:0] g;
      bit [7:0] b;
    } pixel_p_s;
    
    //3. union //i, f는 표현만 다를 뿐, 같은 메모리를 공유한다.
    typedef union {
      int  i;
      real f;
    } num_u;
    
8️⃣Enumeration

    //1. 기본 enum
    enum {RED, BLUE, GREEN} color; //RED=0, BLUE=1, GREEN=2
    
    //잘못된 enum 설계
    typedef enum {FIRST=1, SECOND, THIRD} ordinal_e; //초기값은 0이므로 SECOND=1=FIRST와 충돌
    //해결책
    typedef enum {ERR_0=0, FIRST=1, SECOND, THIRD} ordinal_e;
    
EX)

    program test;
      initial begin
        typedef enum {RED, BLUE, GREEN} COLOR_E;
        COLOR_E color, c2;
        integer c;
        color = 0; //color 값 초기화
        c = color;
        
        c2 = COLOR_E'(c); 
        //type'(expression) 형태의 강제 캐스팅 -> 정수 c를 enum 타입 COLOR_E로 억지로 해석해라
        $display("Color is %0d / %0s", c2, c2.name);
        
        c++;
        if(!$cast(color,c)) $display("Cast failed for c=%0d",c);
        //$cast(dest,src) : src를 dest 타입으로 변환해보고, 가능하면 dest에 넣고 1 반환하고,
        //불가능하면 dest는 안 바꾸고 0 반환한다.
        $display("Color is %0d / %0s", color, color.name);
      end
    endprogram
    
EX) String 예제

    program test;
      initial begin
        string s;
        s = "SystemVerilog";
        $display(s.getc(0));       // 83 ('S')
        $display(s.toupper());     // SYSTEMVERILOG
        s = {s, "3.1b"};           // concat -> "SystemVerilog3.1b"
        s.putc(s.len()-1, "a");    // 마지막 문자 b -> a
        $display(s.substr(2, 5));  // stem
        my_log($psprintf("%s %5d", s, 42));
      end
    
      task my_log(string message);
        $display("@%0d: %s", $time, message);
      endtask
    endprogram

## 📝 About Verification : Procedural Statements and Routines & OOP & Connecting the Testbench and Design

### Procedural Statements and Routines

SystemVerilog는 Verilog의 Procedural Statement(절차문)과 Task/Function을 C/C++ 스타일 + 검증 친화적인 구조로 확장하였다.

👉 “Verilog vs SystemVerilog 문법 차이”
- ✅ for문에서 변수 선언 가능

      for (int i = 0; i < 10; ++i)
          array[i] = i;
    
- ✅ do…while 문 지원

      do
          sum += array[j];
      while (j--);

- ✅ begin : label / end : label (최신 verilog는 모두 지원한다고 알고 있)

      begin : example
         ...
      end : example
  
👉 “C/C++ vs SystemVerilog 루프 제어 스타일 차이”

- 📌C/C++ 스타일 루프 제어

      while (...) begin
          switch (...) begin
              case ...
                  continue; //현재 반복만 스킵하고 loop의 다음 iteration으로 넘어간다.
              case ...
                  break;   //loop 자체를 탈출한다. (switch - case 구문도 포함)
          endcase
      end

- 📌SystemVerilog 스타일 루프 제어
    - Verilog/SystemVerilog는 C/C++과 달리, case 구문으로 들어가면 해당 변수에 대해 만족하는 특정 구문만 실행된다. 따라서 Verilog/SystemVerilog에서는 while begin - case - end 구문이 있을 때, 특정 case에서 break 구문을 만나게 되면, while문 전체를 빠져나오게 된다는 차이점이 있다.


👉 “Verilog vs SystemVerilog Task/Function 구문 차이”
| Task | Function |
| :---: | :---: |
| **시간 소모 가능** | **❌ 시간 소모 불가** |
| **#delay, wait, @(posedge clk) 가능** | **❌ task 호출 불가** |
| **blocking operation 가능** | **✅ 반드시 값 반환 (Verilog 기준)** | 

🚀 SystemVerilog 개선점
- ✅ void function 지원
  - 이를 통해, 반환 값 없이도 함수 사용이 가능하며, task처럼 쓰되, 시간은 소비하지 않는 '순수 계산/출력용 함수' 개념이 명확해졌다.
  
        function void print_state();
            $display(...);
        endfunction

- ✅task/function 내부 begin...end 생략 가능

      task multiple_lines;
          $display("First line");
          $display("Second line");
      endtask

- ✅task 구문에서 return

      task load_array(int len, ref int array[]);
          if (len <= 0) begin
              $display("Bad len");
              return;
          end
          ...
      endtask

task가 하나의 절차적 함수로 취급됨에 따라 return;시, 즉시 task 구문이 종료된다.

👉 timescale의 구조적 문제 해결

기존 verilog 방식은 `timescale 1ns / 1ps로 timescale을 정의하는데, 예컨대, 파일 A가 1ns/1ps, 파일 B가 10ns/1ns이면, 컴파일 순서가 바뀜에 따라 시뮬레이션 결과가 달라질 수 있다. 이에 따라 SystemVerilog는 다음과 같이 개선하였다.

    module timing;
        timeunit 1ns;
        timeprecision 1ps;
​
👉 Call by Reference를 지원하는 SystemVerilog

    task bus_read(
        input logic [31:0] addr, //input datatype : Call by value
        ref   logic [31:0] data  //ref datatype : Call by Reference
    );
    
버스의 read/write 같은 동작은 값을 받아오는 행위이므로, ref를 사용하게 되면, C의 포인터 전달과 유사하게 여러 output을 깔끔하게 처리할 수 있다.

### Basic OOP

모듈 중심의 Verilog 사고에서 객체(class) 중심의 검증 사고로 전환 SystemVerilog의 OOP(클래스)에 관한 문법은 상당히 중요하다.

​- 용어 정리
  
  - 1️⃣ Class : 데이터 + 동작을 묶은 설계 블록
    - 변수(property) + 함수/태스크(method)를 한 덩어리로 묶음
    - Verilog의 module과 개념적으로 가장 유사 (단, module은 하드웨어 구조이지만, class는 검증용 소프트웨어 객체라고 이해하면 된다.)

          class BusTran;
            int addr;
            function void display();
            endfunction
          endclass

  - 2️⃣ Object : 클래스로부터 만들어진 실제 인스턴스
    - class 자체는 설계도
    - new로 만들어진 것이 object
    - module instantiation ↔ class object 생성

          BusTran bt;
          bt = new();

  - 3️⃣ Handle : 객체를 가리키는 참조(reference)
    - a는 객체 그 자체 ❌
    - 객체를 가리키는 핸들(handle) ⭕

          BusTran a;
          a = new();
      
  - 4️⃣ Property : 클래스 안에 있는 데이터(변수)

        class BusTran;
          int addr;
          logic [31:0] data;
        endclass
    
  - 5️⃣ Method : 객체의 동작을 정의하는 코드

        function void display();
          $display("%0d", addr);
        endfunction
    
  - 6️⃣ Prototype : task/function의 선언부

        function void display();
    
👉 SystemVerilog Class

    class BusTran;
        logic [31:0] addr, crc, data[8];
        function new;
            addr = 3;
            foreach (data[i])
                data[i] = 5;
        endfunction
    endclass
    
    BusTran b;
    
- b는 BusTran 타입의 핸들(handle)
- 아직 어떤 객체도 가리키지 않음
- 내부 상태: null (즉, b==null → b.display()하면 런타임 에러)

      b = new;  //c++ 대응 개념 : BusTran* b = new BusTran();

👉 new가 하는 일
- 힙(heap)에 BusTran 객체 생성
- 생성자(constructor) new() 실행
- 그 객체의 주소를 핸들 b에 저장

이제서야 비로소 Instantiation이 일어나면서, 하나의 Object가 생성된다. Object가 생성되면서, 위에서 정의한 function new; 가 자동 호출되면서 객체의 초기 상태를 정의하게 된다.

### 개념 차이 : new() vs new[]

- ✅ new() : Class Object Instantiation

      BusTran b;
      b = new;
      b = new(10);   // 생성자 인자

- ✅ new[] : 동적 배열(dynamic array) 생성

      int dyn[];
      dyn = new[5];
  
🔥 핵심 오해 포인트 정리1 - new()와 new[]의 차이를 명확히 보여주는 예제

    BusTran arr[];     // ❗ 클래스 핸들 배열
    arr = new[4];      // 핸들 4개 생성
    
    /*
    이 상태에서:
    arr[0] == null
    arr[1] == null
    …
    ❗ 객체는 하나도 없음
    */
    
    foreach (arr[i])
        arr[i] = new;  // ← 여기서 진짜 객체 생성
        
🔥 핵심 오해 포인트 정리2 - 객체 생성 과정에서 주의점

    BusTran b1, b2;   // handle 두 개 선언
    b1 = new;         // 첫 번째 객체 생성
    b2 = b1;          // 같은 객체를 가리킴
    /*
    b1 ─┐
        ├──> object #1
    b2 ─┘
    */
    
    b1 = new;         // 두 번째 객체 생성
    /*
    b1 ───> object #2
    b2 ───> object #1
    */
    
🔥 핵심 오해 포인트 정리2 - Garbage Collection의 정확한 의미(Deallocation)

    BusTran b;
    b = new;     // 첫 번째 객체
    //object #1 생성
    //참조 핸들 수 = 1
    
    b = new;     // 두 번째 객체 (첫 번째는?)
    //object #2 생성
    //b가 object #1을 더 이상 가리키지 않음
    //따라서 object #1에 대해서는 참조 핸들 수가 없으므로 garbage collection 대상에 포함된다.
    
    b = null;    // 두 번째 객체는?
    //만약 b=null 해버리면 b는 아무런 object도 가리키지 않게되면서 objct #2 역시 참조 핸들 수가 사라진다.
    
🔥 핵심 오해 포인트 정리3 - Compilation Order (아직 정의되지 않은 클래스를 쓰고 싶을 때)
(단, 컴파일러에 따라 typedef 선언 없이도 되는 경우가 있지만, 표준적으로는 unsafe하므로, 이식성을 위해 항상 쓰는 것이 정석이다.)

    typedef class Statistics;   // 미리 알려줌
    
    class BusTran;
        Statistics stats;       // OK
    endclass
    
    class Statistics;
    endclass
    
- 1️⃣ SystemVerilog 특징1 - 'extern' + '::'
  - SystemVerilog에서는 클래스 외부에 함수 정의가 가능하지만, 반드시 extern 선언 + ClassName::function 형식을 사용해야 한다.

        class BusTran;
            bit [31:0] addr, crc, data[8];
            extern function void display();
        endclass

        function void BusTran::display();
            $display("@%0d: BusTran addr=%h, crc=%h", addr, crc);
            $write("\tdata[0-7]=");
            foreach (data[i]) $write(data[i]);
            $display();
        endfunction
    
- 2️⃣SystemVerilog 특징2 - 'this' handle
  - 클래스 맴버(위에서 정의한 string oname)과, function에서 정의한 argument의 이름이 충돌할 경우, 현재 겍체를 가리키는 this 핸들을 사용할 수 있다. 따라서 this는 함수가 호출되는 시점의 자기 자신의 객체를 가리키는 참조 변수에 해당한다.

        class Scoping;
            string oname;
        
            function new(string oname);
                this.oname = oname;
            endfunction
        endclass
    
- 3️⃣SystemVerilog 특징3 - static
  - static으로 데이터 타입을 설정한 경우, 해당 멤버는 객체마다 하나가 아니라 '클래스 전체에서 단 하나만 존재'한다.

        program test;
        
        class BusTran;
            static int count = 0; // Number of objects created (클래스 변수)
            int id;               // Unique instance ID (객체 변수)
        
            function new;
                id = count++;     // 현재 count를 id에 넣고, count 증가
            endfunction
        endclass
        
        BusTran b1, b2;
        
        initial begin
            b1 = new;  // First instance
            b2 = new;  // Second instance
            $display("Second id=%0d, count=%0d", b2.id, b2.count);
        end
        
        endprogram
        
        /*
        (1) 시작 시점
        BusTran.count = 0
        b1 = null
        b2 = null
        
        (2) b1 = new;
        count = 0
        id = 0
        count++ → count = 1
        따라서
        b1.id = 0
        BusTran.count = 1
        
        (3) b2 = new;
        count = 1
        id = 1
        count++ → count = 2
        따라서
        b2.id = 1
        BusTran.count = 2 -> b2.count = b1.count
        */
        
        /*
        최종 정리
        BusTran class
         └─ static count = 2   ← 모든 객체가 공유
        
        b1 ── id = 0
        b2 ── id = 1
        */
Connecting the Testbench and Design

Testbench - DUT 연결을 안전하고, 재사용 가능하고, 타이밍 버그 없이 만들기 위해 단순 포트 연결이 아닌 추가 개념이 확장되었다. 두 가지 코드를 비교해보자.

//-------------------------
// (1) Testbench module
//-------------------------
module test (
  input  logic [1:0] grant,
  output logic [1:0] request,
  input  logic       reset,
  input  logic       clk
);
  initial begin
    @(posedge clk);
    request <= 2'b01;
    $display("@%0d: Drove req=01", $time);
    repeat (2) @(posedge clk);
    if (grant != 2'b01)
      $display("@%0d: a1: grant != 2'b01", $time);
    ...
    $finish;
  end
endmodule

//-------------------------
// (2) DUT module (ports)
//-------------------------
module arb_port (
  output logic [1:0] grant,
  input  logic [1:0] request,
  input  logic       reset,
  input  logic       clk
);
  ...
  always @(posedge clk or posedge reset) begin
    if (reset)
      grant <= 2'b00;
    else
      ...
  end
endmodule

//-------------------------
// (3) Top module: wiring
//-------------------------
module top;
  logic [1:0] grant, request;
  logic       clk = 0, reset;
  always #5 clk = ~clk;
  arb_port a1 (grant, request, reset, clk);
  test     t1 (grant, request, reset, clk);
endmodule
기존 코드

포트 나열 순서가 맞아야 하며, 신호 수가 늘어수록 실수할 부분들이 급격하게 늘어난다.

//-------------------------
// (1) Interface definition
//-------------------------
interface arb_if (input bit clk);
  logic [1:0] grant, request;
  logic       reset;
endinterface

//-------------------------
// (2) Testbench module
//-------------------------
module test (arb_if arbif);
  ...
  initial begin
    // reset code left out
    @(posedge arbif.clk);
    arbif.request <= 2'b01;
    $display("@%0d: Drove req=01", $time);
    repeat (2) @(posedge arbif.clk);
    if (arbif.grant != 2'b01)
      $display("@%0d: a1: grant != 2'b01", $time);
    $finish;
  end
endmodule : test

//-------------------------
// (3) DUT module (interface port)
//-------------------------
module arb (arb_if arbif);
  ...
  always @(posedge arbif.clk or posedge arbif.reset) begin
    if (arbif.reset)
      arbif.grant <= 2'b00;
    else
      arbif.grant <= next_grant;
    ...
  end
endmodule

//-------------------------
// (4) Top module
//-------------------------
module top;
  bit clk;
  always #5 clk = ~clk;
  arb_if arbif(clk);

  arb  a1(arbif);
  test t1(arbif);

endmodule : top
interface arb_if(input bit clk);를 통해 arb_if가 grant/request/reset/clk를 한 덩어리로 묶고, clk는 interface 포트로 들어가서, interface 내부에서 arbif.clk처럼 접근 가능해졌다. 만약 개별로 꺼내서 사용하고 싶다면, 다음과 같이 사용하면 된다.

arb_port a1 (
.grant (arbif.grant),
.request (arbif.request),
.reset (arbif.reset),
.clk (arbif.clk)
);
❗ 문제 : interface 안에 있는 신호들은 기본적으로 양방향처럼 보임

arbif.grant = ...;   // testbench도 가능
arbif.grant = ...;   // DUT도 가능 → 위험!
✅ 해결: modport : “누가 무엇을 읽고/쓰는지”를 명확히 규정

modport TEST (output request, reset, input grant, clk);
modport DUT  (input request, reset, clk, output grant);
●Interface의 Trade-off
