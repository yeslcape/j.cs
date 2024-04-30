# CPU
![](https://github.com/yeslcape/j.cs/assets/45252618/9b39c024-4da1-4a83-9e1b-2a3260b0badf)

### CPU 구성 요소
- ALU (Arithmetic and Logical Unit, 산술논리연산장치)
  - 가산기, 누산기, 보수기, 데이터 레지스터, 상태 레지스터, 인덱스 레지스터 등으로 구성
  - 캐시나 메모리로부터 읽어온 데이터는 레지스터(Register)라는 CPU 전용의 기억장소에 저장 
  - 레지스터에 저장된 데이터를 이용하여 덧셈, 곱셈 등과 같은 산술 연산을 수행
  - 부동소수연산장치(FPU)와 정수연산장치, 논리연산(AND, OR 등) 장치 등
- 레지스터 : 속도가 가장 빠른 기억장치. 데이터 혹은 주소 저장
  - 범용 레지스터 : ALU에 의해 사용됨
  - 전용 레지스터 : PC 등 특수 목적에 사용됨
  - IR(Instruction Register) : 현재 수행 중에 있는 명령어 부호를 저장하고 있는 레지스터
  - PC(Program Counter) : 명령이 저장된 메모리의 주소를 가리키는 레지스터. 다음에 수행할 명령어 주소 저장
  - AC(Accumulator) : 산술 및 논리 연산의 결과를 임시로 기억하는 레지스터
  - MAR(메모리 주소 레지스터) : 읽기와 쓰기 연산을 수행할 주기억장치 주소 저장
  - MBR(메모리 버퍼 레지스터) : 주기억장치에서 읽어온 데이터 or 저장할 데이터 임시 저장
- 제어 장치 : 명령어를 해석하고 실행하기 위한 제어 신호 전달
  - Program Counter(프로그램 계수기) : 프로그램 수행 순서 제어
  - Instruction Register(명령 레지스터) : 현재 수행중인 명령어의 내용 임시 기억
  - Instruction Decoder(명령해독기) : 명령 레지스터에 수록된 명령을 해독하여 수행될 장치에 제어 신호 보냄
  - 제어 장치 구현 방식

      |고정 배선 제어(Hardwired)|Micro Program|
      |---|---|
      |제어신호가 Hardwired Circuit에 의해서 생성 되도록 하드웨어 구성하며 상태계수기와 PLA(Programmable Logic Array) 회로로 구성|발생 가능한 제어 신호들의 조합을 미리 구성하여 ROM에 저장했다가 필요 시 신호를 발생시키는 Software 방식|
      |고속 처리, 고가|하드웨어 방식에 비해 속도도 낮고 가격도 저렴|
      |RISC 시스템에 적용|CISC에 적용|

    - CISC(Complex Instruction Set Computer)
        - 여러 사이클로 명령어 처리
        - 많은 명령어가 메모리를 참조하는 방식 
        - 파이프라이닝의 사용이 어려움 
        - 복잡한 마이크로 프로그램 구조
    - RISC(Reduced Instruction Set Computer)
      - 하나의 사이클로 명령어를 처리 
      - 메모리 Load / Store 명령만 처리하는 방식
      - 파이프라이닝, 슈퍼스칼라의 사용 가능
      - 복잡한 컴파일러 구조

### CPU 명령어 수행 과정
명령어 형식 = 연산코드 + 기억장치 주소 (연산에 사용될 데이터가 저장된 주소)
1. 명령어 인출 : 제어 장치를 통해서 메모리에 저장된 명령어를 읽어와 레지스터(Register)라는 CPU 내부의 기억장소에 저장
    ```
    PC에 저장된 주소를 MAR로 전달
    저장된 내용을 토대로 주기억장치의 해당 주소에서 명령어 인출
    인출한 명령어를 MBR에 저장
    다음 명령어를 인출하기 위해 PC 값 증가시킴
    메모리 버퍼 레지스터(MBR)에 저장된 내용을 명령어 레지스터(IR)에 전달
   
    T0 : MAR ← PC
    T1 : MBR ← M[MAR], PC ← PC+1
    T2 : IR ← MBR
    ```
2. 명령어 해독 : 레지스터에 저장된 명령어는 제어장치를 통해서 명령어를 해석한 다음 저장된 데이터가 필요하다고 판단하면 추가적으로 메모리를 읽어 데이터를 가져와 레지스터에 저장
3. 명령어 실행 : 레지스터에 저장된 데이터를 이용해서 ALU에서 산술 연산 수행
    ```
   [ADD addr 명령어 연산]
    T0 : MAR ← IR(Addr)
    T1 : MBR ← M[MAR]
    T2 : AC ← AC + MBR
   
   [LOAD addr 명령어 연산]
   T0 : MAR ← IR(Addr)
    T1 : MBR ← M[MAR]
    T2 : AC ← MBR
   
   [STA addr 명령어 연산 : AC에 있는 데이터를 기억장치로 저장하는 명령어]
   T0 : MAR ← IR(Addr)
    T1 : MBR ← AC
    T2 : M[MAR] ← MBR
   
   [JUMP addr 명령어 연산 : PC값을 IR의 주소값으로 변경하는 분기 명령어]
   T0 : PC ← IR(Addr)
    ```
4. 저장 : 계산한 결과값은 레지스터에 저장되었다가 저장하는 추가 명령어에 의해 메모리에 계산된 결과값 저장



- https://velog.io/@rsuubinn/%EC%BB%B4%ED%93%A8%ED%84%B0-%EA%B5%AC%EC%A1%B0-%EC%BB%B4%ED%93%A8%ED%84%B0%EC%9D%98-%EA%B8%B0%EB%B3%B8-%EA%B5%AC%EC%A1%B0-CPU%EC%99%80-%EB%A9%94%EB%AA%A8%EB%A6%AC
- https://too-march.tistory.com/3
- https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Computer%20Architecture/%EC%A4%91%EC%95%99%EC%B2%98%EB%A6%AC%EC%9E%A5%EC%B9%98(CPU)%20%EC%9E%91%EB%8F%99%20%EC%9B%90%EB%A6%AC.md
- https://velog.io/@hyunji015/%EC%BB%B4%ED%93%A8%ED%84%B0-%EA%B5%AC%EC%A1%B0-%EC%BB%B4%ED%93%A8%ED%84%B0%EB%A5%BC-%EA%B5%AC%EC%84%B1%ED%95%98%EB%8A%94-%EC%9A%94%EC%86%8C