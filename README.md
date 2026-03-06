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
    
EX)

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
| :--- | :--- | :--- |
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
      
EX) find 

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


