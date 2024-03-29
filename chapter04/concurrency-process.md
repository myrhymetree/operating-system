# 4. 병행 프로세스

## 4.1 병행 프로세스의 개념

### 4.1.1 병행성

![image](https://github.com/myrhymetree/operating-system/assets/94158097/87541649-1382-4784-965e-1063963f6522)

1. 병행성(concurreny)
    - 여러 개의 프로세스 또는 쓰레드가 동시에 실행되는 시스템의 특성
2. 병행 프로세스
    - 동시에 실행되는 여러 개의 프로세스 또는 쓰레드
3. 병행 프로세스의 실행 형태
- 1개의 CPU : 인터리빙 형식
    
    ![image](https://github.com/myrhymetree/operating-system/assets/94158097/3dc15213-d45d-4539-a6a6-00a6ff2181c4)
    
- 여러 개의 CPU : 병렬처리 형식
    
    ![image](https://github.com/myrhymetree/operating-system/assets/94158097/1102b0c8-ad12-4aac-87a0-a3ef7bdff7fc)
    
- 멀티프로세서 시스템에서의 메모리 구조에 따라
    
    ![image](https://github.com/myrhymetree/operating-system/assets/94158097/ea5611d3-d6af-4142-bf38-b4095db42c5c)
    
1. 프로세스 간의 관계
    - 독립 프로세스
        - 수행 중인 다른 프로세스에 영향을 주지도 받지도 않음
        - 데이터 및 상태를 다른 프로세스와 공유하지 않음
        - 프로세스의 실행
            - 결정적 : 실행결과는 입력에 의해서만 결정됨
            - 재생 가능 : 같은 입력에 대해 항상 동일한 실행 결과
    - 협력 프로세스
        - 수행중인 다른 프로세스와 영향을 주고 받음
        - 데이터 및 상태를 다른 프로세스와 공유
        - 프로세스의 실행
            - 비결정적 : 실행결과는 실행순서에 좌우됨
            - 재생 불가능 : 같은 입력에 대해 항상 동일한 실행결과를 보장하지 못함
        - 병행성 문제
            - 협력 프로세스인 경우 발생하는 문제
                - 상호배제
                - 동기화
                - 통신

### 4.1.2 단일 프로세스 내의 병행성

1. 우선순위 그래프
    - 어떤 연산의 일부분이 가지는 우선순위 제약조건을 정의하는 데 유용한 방법
    - 각 정점이 개개의 문장에 대응하는 사이클이 없는 방향 그래프
    - 정점 S₁에서 정점 S₂로의 간선(edge)을 연결함은 S₁가 수행을 끝낸 후에야 비로소  S₂를 수행할 수 있음을 의미.
2. Fork/Join 구조
    - fork L 명령어는 프로그램 내에서 2개의 병행 수행을 만들어 냄
    - join 명령어는 병행하는 2개의 연산을 하나로 재결합 시키는 방법을 제공
3. 병행문
- 1개의 프로세스가 여러 가닥의 병렬 프로세스로 분할되었다가 다시 한 가닥의 프로세스로 결합하는 것을 나타냄
- parbegin/parend 문

## 4.2 동기화와 임계영역

1. 프로세스 동기화(synchronization)
    
    ![image](https://github.com/myrhymetree/operating-system/assets/94158097/6bf92408-6b3f-467b-9346-b287f0984840)
    
    - 2개 이상의 프로세스에 대한 처리순서를 결정하는 것.
    - 동시에 사용할 수 없는 공유자원이 있는 경우 동기화 필요
    - 한 프로세스의 처리 결과에 따라 다른 프로세스의 처리가 영향을 받는 경우 동기화 필요
2. 임계영역(critical section)
    - 2개 이상의 프로세스가 동시에 사용하면 안되는 공유자원을 액세스하는 프로그램 코드 영역
3. 상호배제(mutual exclusion)
    
    ![image](https://github.com/myrhymetree/operating-system/assets/94158097/33f69aa2-79f6-414e-a601-83749229c4ad)
    
    - 2개 이상의 프로세스가 동시에 임계영역에 진입하지 못하도록 하는 것.
4. 통신
    - 프로세스들이 데이터를 공유하기 위해 반드시 필요
        - 프로세스 간 통신(IPC)
    - 통신 방법
        - 하나의 변수 사용
        - 메시지를 주고 받음
5. 임계영역 문제 해결을 위한 요구조건
    - 상호배제
    - 진행
    - 제한된 대기

### 4.2.1 Test-and-Set

1. Test-and-Set
    - 분리가 불가능한 단일 기계 명령어
    - 원자적으로 수행

Test-and-Set 개념 추상화

```pascal
function Test_and_Set(var target: boolean): boolean;
	begin
		Test_and_Set := target;
		target := true;
	end;

repeat
	while Test_and_Set(lock) do skip;
	임계영역
	lock := false;
	잔류영역
until false;
```

이 코드는 "테스트 앤 세트(Test and Set)"라는 동기화 메커니즘을 구현한 것으로 보이며, 사용된 언어는 **`Pascal`** 또는 그에 유사한 언어로 보입니다. Pascal은 알고리즘과 데이터 구조를 명확하게 표현하기 위해 고안된 프로그래밍 언어로, 교육용으로 많이 사용됩니다. 이 코드에서 **`Test_and_Set`** 함수는 주어진 **`target`** 변수의 원래 값을 반환하고, 그 변수를 **`true`**로 설정하는 기능을 합니다. 이러한 기능은 동시성 제어에서 중요한 역할을 하며, 여러 프로세스 또는 스레드가 동일한 자원에 동시에 접근하는 것을 방지하는 데 사용됩니다.

1. 단점
    - 많은 프로세스가 임계영역에 들어가기를 원할 때 기아가 발생
    - 기아(starvation) : 프로세스가 필요한 자원할당을 받지 못하고 계속적으로 대기하게 되는 상황
    - 대기 프로세스는 비생산적이고 자원만을 소비하는 busy-waiting이 일어남

원자적 : 인터럽트 되지 않은 하나의 단위로 처리됨.

### 4.2.2 세마포어

- 상호배제와 동기화 문제를 해결하기 위한 도구
- Dijkstra가 제안

```pascal
P(s):
	if(s > 0) then
			s := s-1;
	else
		현재의 프로세스 대기;

V(s):
	if(1개 이상의 프로세스가 대기중) then
		그중 1개의 프로세스만 진행;
	else
		s := s+1;
```

```pascal
repeat
	P(mutex);
	임계영역
	V(mutex);
	잔류영역
until false;
```

1. 세마포어(semaphore) s
    - 정수형 공용변수
        - 저장값 : 사용 가능한 자원의 수 또는 잠김이나 풀림의 상태
    - 상황에 맞춰 0 이상인 정수로 초기화
    - 두 표준단위연산(기본 연산) P와 V에 의해서만 접근됨
        - 기본연산 : 인터럽트되지 않고 하나의 단위로 처리됨
    
    ![image](https://github.com/myrhymetree/operating-system/assets/94158097/cc001cbb-d321-4bd5-8c56-8dd5d876c3e1)
    
    - P : 검사, 또는 감소시키려는 시도
    - V : 증가
    - 세마포어마다 대기 큐 필요

### 4.2.3 상호배제 해결

- 한 프로세스가 임계영역 수행 중
    - 다른 프로세스는 임계영역에 진입해서는 안됨
- 임계영역 수행 중이던 프로세스가 임계영역 벗어남
    - 누군가 하나는 임계영역을 새로이 수행할 수 있어야 함
- 임계영역 진입 못하고 대기하는 프로세스
    - 적절한 시간 내에 임계영역 수행을 시작할 수 있어야 함
- 상호배제를 위한 임계영역 주변의 코드 영역
    
    ![image](https://github.com/myrhymetree/operating-system/assets/94158097/2c92fd90-9b1d-4278-a07c-f73003507d90)
    
- 세마포어 이용
    
    ![image](https://github.com/myrhymetree/operating-system/assets/94158097/b142cfbf-27ea-4852-80bf-6b3ea1ef4625)
    
- 상호배제 해결 예시
    
    ![image](https://github.com/myrhymetree/operating-system/assets/94158097/2ccc82e1-97ee-4309-8c55-ede0bd54b25f)
    

### 4.2.4 동기화 해결

- 상황 : 프로세스 A가 코드 S₁을 수행한 후 프로세스 B가 코드 S₂를 수행하도록 동기화
    
    ![image](https://github.com/myrhymetree/operating-system/assets/94158097/5213ca7d-d2fa-43be-9e59-73c48bf78f2d)

- 세마포어 sync 초깃값은 0

## 4.3 프로세스의 상호협력

### 4.3.1 생산자/소비자 문제

1. 생산자/소비자 문제
    
    ![image](https://github.com/myrhymetree/operating-system/assets/94158097/b7c516a1-9225-452f-84d4-1c4ac3983bc9)
    
    - 두 협력 프로세스 사이에 버퍼를 두고 생산자와 소비자의 상황을 다루는 문제
    - 고정된 크기를 가진 버퍼를 생산자와 소비자 사이에 둠
        - 생산자 : 데이터를 넣는 프로세스
        - 소비자 : 데이터를 꺼내는 프로세스
    - 버퍼에 여러 프로세스가 동시에 접근할 수 없음
        - 버퍼에 데이터를 넣는 동안에는 데이터를 꺼낼 수 없음
        - 버퍼에서 데이터를 꺼내는 동안에는 데이터를 넣을 수 없음
            
            → 상호배제 필요
            
    - 버퍼의 크기가 유한(유한 버퍼 문제)
        - 버퍼가 비어 있다면 소비자가 기다리게 되고 버퍼가 가득 차면 생산자가 기다리게 됨
        
        → 동기화 필요
        
    - 세마포어를 이용한 해결
        - 상호배제 : 세마포어 mutex (초깃값 1)
    
    ![image](https://github.com/myrhymetree/operating-system/assets/94158097/94d4ae00-ed69-40ab-a664-ffbeb0abca9f)
    
    - 버퍼가 가득 찬 경우 동기화 :세마포어 empty (초깃값 n)
    
    ![image](https://github.com/myrhymetree/operating-system/assets/94158097/7e4e7ce0-c540-42e3-a76a-b391c9cdf2e8)
    

- 버파가 빈 경우 동기화 : 세마포어 full (초깃값 0)

    ![image](https://github.com/myrhymetree/operating-system/assets/94158097/76fa9a6b-62d9-479e-a29e-4a934fa0a080)

- 3개의 세마포어 : mutex(초깃값 1), empty(초깃값 n), full(초깃값 0)

    ![image](https://github.com/myrhymetree/operating-system/assets/94158097/b9a4401f-4c4a-4506-aa5e-cb242a4d5d71)

생산자 프로세스에 대한 코드

```pascal
repeat
	...
	nextp에 데이터 항목을 갱신함
	...
	P(empty);
	P(mutex);
	...
	nextp를 버퍼에 넣음
	...
	V(mutex);
	V(full);
until false;
```

소비자 프로세스에 대한 코드

```pascal
repeat
	P(full);
	P(mutex);
	...
		버퍼에서 데이터 항목을 꺼내 nextc에 넣음
	...
	V(mutex);
	V(empty);
	...
	nextc에 있는 데이터 항목을 소비함
	...
until false;
```

### 4.3.2 판독기/기록기 문제

- 여러 협력 프로세스 사이에 공유자원을 두고 판독기와 기록기의 상황을 다루는 문제
    - 판독기 : 데이터를 읽는 프로세스
    - 기록기 : 데이터를 쓰는 프로세스
- 2개의 판독기가 동시에 공유 데이터 객체에 접근하고자 할때는 아무런 문제가 일어나지 않지만, 기록기와 또 다른 프로세스(판독기 또는 기록기)가 동시에 공유객체에 접근한다면 문제가 발생하여 병행성 조건을 침해.
    
    이런 형태의 어려운 점이 생기지 않도록 하기 위해서는 기록기가 공유객체에 대해 배타적 접근을 하도록 해야 함(상호 배제).
    

![image](https://github.com/myrhymetree/operating-system/assets/94158097/bf408799-32ef-429e-ad35-b5cbbf7b5eb0)

1. 판독기/기록기 문제
    - 여러 개의 판독기가 동시에 공유 데이터 객체에 접근하는 것은 문제가 없음
        - 판독기가 읽는 중 새로운 판독기 읽기 시도 → 가능
        - 판도기가 읽는 중 기록기 대기 → 새로운 판독기 읽기 시도 → 가능/불가능
    - 기록기가 판독기나 다른 기록기와 동시에 공유 데이터 객체에 접근하는 경우 배타적 접근을 해야 함(상호배제)
2. 제 1 판독기/기록기 문제
    - 기록기가 이미 공유 객체를 사용하도록 허가되지 않았다면 판독기는 대기하지 않음
    - 판독기가 공유 자원에 접근 중이라면 기록기보다 판독기에 우선순위를 줌
    - 즉, 새로운 판독기는 즉시 공유자원에 접근 가능
    - 문제점 : 기록기의 기아상태 유발 가능
    - 세마포어를 이용한 해결
        - 상호배제 : 세마포어 wrt (초깃값 1)
            
            ![image](https://github.com/myrhymetree/operating-system/assets/94158097/0a322433-9a1c-446c-b0d7-8e8d68347289)
            
        - 판독기 우선 : 일반변수 rcount(초깃값 0), 세마포어 mutex(초깃값 1)
            
            ![image](https://github.com/myrhymetree/operating-system/assets/94158097/28f7042a-024e-4483-b1bb-ed5875fff6dd)
            
        - 2개의 세마포어 wrt(초깃값 1), mutex(초깃값 1), 일반변수 rcount(초깃값 0)
            
            ![image](https://github.com/myrhymetree/operating-system/assets/94158097/ad0cae32-0bf5-4322-8b74-c2612c6f7b76)
            
3. 제 2 판독기/기록기 문제
    - 판독기가 공유자원에 접근 중이라면 판독기보다 기록기에 우선순위를 줌
    - 일단 기록기가 준비되었다면 기록을 가능한 한 빨리 수행할 수 있도록 함
    - 즉, 대기 중인 기록기가 있다면 새로운 판독기는 공유자원에 접근 불가능
    - 문제점
        - 판독기의 병행성이 떨어짐
        - 판독기의 기아상태 유발 가능
    - 세마포어를 이용한 해결
        - 5개의 세마포어 rd(초깃값 1) ,wrt(1), mutex1(1), mutex2(1), mutex3(1)
        
        ![image](https://github.com/myrhymetree/operating-system/assets/94158097/93b0435d-293f-490c-9dc9-c8cf1e91ef0e)
        

## 4.4 프로세스 간의 통신(IPC)

- InterProcess Communication
- 병행 프로세스가 데이터를 서로 공유하는 방법
    - 공유 메모리 방법
    - 메시지 전달방법
- 공유기억장치 기법과 메시지 시스템 기법은 상호 배타적이 아닌, 단일 운영체제 내에서 동시에 사용됨
- 하나의 운영체제에서 두 방법 함께 사용 가능

### 4.4.1 공유기억장치 기법

1. 공유 기억장치(메모리) 기법

![image](https://github.com/myrhymetree/operating-system/assets/94158097/5a24ec06-c1b2-4999-ad57-652f54dab22f)

- 프로세스 간의 공유 변수를 두어 프로세스가 이를 이용하여 정보 교환
    - 동일한 변수 : 공유자원인 메모리 공간 사용
- 예
    - 생산자-소비자 문제의 유한 버퍼
    - 판독기-기록기 문제의 공유자원
- 대량 데이터 교환 : 고속의 통신을 할 수 있음
- 통신 기능 제공의 책임은 응용 프로그래머에게 있음
- 운영체제는 공유기억장소만을 제공

### 4.4.2 메시지 시스템 기법

1. 메시지 시스템 기법
    
    ![image](https://github.com/myrhymetree/operating-system/assets/94158097/c2a5b3d0-d22a-48bc-a033-84f445789b2e)

- 메시지 교환방식을 이용하여 프로세스가 서로 정보 교환
- 통신기능은 시스템 호출 send와 receive 연산자의 형태로 제공
- 보다 소량의 데이터를 교환하는데 유용한 방식
- 통신기능 제공의 책임은 운영체제에 있음

1. 통신 링크
    
    ![image](https://github.com/myrhymetree/operating-system/assets/94158097/ce99280e-ce61-44d1-9d67-573a9db5d5ff)
    
    - 메시지가 지나다니는 통로
    - 통신을 원하는 프로세스들 사이에 존재해야 함
    - 논리적 구현에 대한 다양한 이슈 존재
    - 통신링크의 실질적 구현
        - 연결 대상 : 두 프로세스, 셋 이상 프로세스
        - 두 프로세스 사이 링크 개수 : 하나, 둘 이상
        - 방향성 : 단방향, 양방향
        - 용량 : 무한, 유한, 0
        1. 어떻게 링크를 설정하는가?
        2. 한 링크가 2개 이상의 프로세스와 연결될 수 있는가?
        3. 통신 프로세스의 쌍(pair)사이에 얼마나 많은 링크가 있는가?
        4. 링크의 용량은 얼마인가? 즉 링크가 어느정도 버퍼 공간을 갖는가? 갖는다면 어느정도?
        5. 메시지의 크기는 어느정도? 링크가 가변크기 또는 고정크기 메시지를 수용할 수 있는가?
        6. 링크가 단방향인가? 양방향인가? 즉 P와 Q사이에 링크가 있을 때 메시지가 한 방향으로(예를 들어, P에서 Q로만) 또는 양방향 모두 가능한가?
2. 직접 통신
    - 두 프로세스가 직접 서로를 지정하여 메시지 전달
        
        ![image](https://github.com/myrhymetree/operating-system/assets/94158097/9847c63a-5b0a-4aaf-84ff-02c8fd5b69fe)
        
    - 오직 하나의 통신 링크가 자동 설정
    - 하나의 통신 링크는 오직 두 프로세스 사이에만 연관
    - 통신 링크는 양방향
    - 메시지 전달 연산에 수신자나 송신자 이름을 명시(유연하지 못함)
    - send(P, message) : 프로세스 P로 메시지를 보냄
    - receive(Q, message) : 프로세스 Q에서 메시지를 받음
    - 대칭형 주소 지정
        
        ![image](https://github.com/myrhymetree/operating-system/assets/94158097/896ece21-768e-4cc0-997b-22787ae61362)
        
    - 비대칭형 주소 지정
        
        ![image](https://github.com/myrhymetree/operating-system/assets/94158097/90286d1a-a08d-41ed-952f-b7a1d804ce8e)
        
        - 수신자가 여러 송신자와 통신 링크를 갖는 경우 사용
3. 간접 통신
    
    ![image](https://github.com/myrhymetree/operating-system/assets/94158097/d820133e-708b-49f7-95b6-96566af41ced)
    
    - 우편함(mailbox 또는 port)을 통해 메시지를 주고 받음(유연함)
    - 두 프로세스는 공유 우편함을 가질 때만 통신할 수 있음
    - 같은 우편함을 이용하는 경우 통신 링크가 설정
    - 여러 우편함을 이용하면 여러 개의 통신 링크 존재
    - 하나의 통신 링크가 여러 프로세스와 연관 가능
    - 통신링크는 단방향 또는 양방향
    - send(A, message) : 우편함 A로 메시지를 본냄
    - receive(Q, message) : 프로세스 Q에서 메시지를 받음
4. 우편함의 소유권
    
    ![image](https://github.com/myrhymetree/operating-system/assets/94158097/284ead35-16ff-4df2-befb-ae2258200026)
    
    - 프로세스 소속
        - 우편함이 수신 프로세스에 소속
        - 소유자는 수신만, 사용자는 송신만 함
        - 통신링크는 단방향
        - 수신 프로세스가 종료하면 우편함도 사라짐
        
        ![image](https://github.com/myrhymetree/operating-system/assets/94158097/6175ed7a-3128-4bc4-98be-2878a930c539)
        
    - 운영체제 소속
        - 우편함은 스스로 존재
        - 수신자 여럿
        - 한순간에 하나의 수신자만 가능
        - 운영체제가 수신자 관리
        - 통신링크는 양방향
5. 링크의 용량
    
    ![image](https://github.com/myrhymetree/operating-system/assets/94158097/2960a83b-558a-4647-9302-3d164cc08637)
    
    - 무제한 용량 : 송신자는 대기할 필요가 없음
    - 제한된 용량 : 큐가 가득차면 송신자는 대기해야 함
    - ‘0’용량 : 송신자와 수신자는 메시지 전송을 위해 동기화 되어야 함.

7. 예외 조건

- 프로세스 종료
- 메시지 상실
- 메시지 혼합
