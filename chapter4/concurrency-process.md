# 4. 병행 프로세스

## 4.1 병행 프로세스의 개념

### 4.1.1 병행성

1. 병행성(concurreny)
    - 여러 개의 프로세스 또는 쓰레드가 동시에 실행되는 시스템의 특성
2. 병행 프로세스
    - 동시에 실행되는 여러 개의 프로세스 또는 쓰레드

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
    - 2개 이상의 프로세스에 대한 처리순서를 결정하는 것.
    - 동시에 사용할 수 없는 공유자원이 있는 경우 동기화 필요
    - 한 프로세스의 처리 결과에 따라 다른 프로세스의 처리가 영향을 받는 경우 동기화 필요
2. 임계영역(critical section)
    - 2개 이상의 프로세스가 동시에 임계영역에 진입하지 못하도록 하는 것.
3. 상호배제(mutual exclusion)
    - 2개 이상의 프로세스가 동시에 임계영역에 진입하지 못하도록 하는 것.
4. 임계영역 문제 해결을 위한 요구조건
    - 상호배제
    - 진행
    - 제한된 대기

### 4.2.1 Test-and-Set

1. Test-and-Set
    - 분리가 불가능한 단일 기계 명령어
    - 원자적으로 수행
2. 단점
    - 많은 프로세스가 임계영역에 들어가기를 원할 때 기아가 발생
    - 기아(starvation) : 프로세스가 필요한 자원할당을 받지 못하고 계속적으로 대기하게 되는 상황
    - 대기 프로세스는 비생산적이고 자원만을 소비하는 busy-waiting이 일어남

### 4.2.2 세마포어

1. 세마포어(semaphore) s
    - 정수형 공용변수
    - 두 표준단위연산 P와 V에 의해서만 접근됨
    - P : 검사, 또는 감소시키려는 시도
    - V : 증가

## 4.3 프로세스의 상호협력

### 4.3.1 생산자/소비자 문제

1. 생산자/소비자 문제
- 유한 버퍼 문제라고도 함
- 고정된 크기를 가진 버퍼를 생산자와 소비자 사이에 둠
- 버퍼가 비어있다면 소비자가 기다리게 되고 버퍼가 가득차면 생산자가 기다리게됨
- 상호배제와 동기화가 필요

### 4.3.2 판독기/기록기 문제

1. 판독기/기록기 문제
    - 여러 개의 판독기가 동시에 공유 데이터 객체에 접근하는 것은 문제가 없음
    - 기록기가 판독기나 다른 기록기와 동시에 공유 데이터 객체에 접근하는 경우 배타적 접근을 해야 함
2. 제 1 판독기/기록기 문제
    - 기록기가 이미 공유 객체를 사용하도록 허가되지 않았다면 판독기는 대기하지 않음
    - 기록기의 기아상태 유발 가능
3. 제 2 판독기/기록기 문제
    - 일단 기록기가 준비되었다면 기록을 가능한 한 빨리 수행할 수 있도록 함
    - 판독기의 기아상태 유발 가능

## 4.4 프로세스 간의 통신

### 4.4.1 공유기억장치 기법

1. 공유 기억장치 기법
    - 프로세스 간의 공유 변수를 두어 프로세스가 이를 이용하여 정보 교환
    - 고속의 통신을 할 수 있음
    - 통신 기능 제공의 책임은 응용 프로그래머에게 있음
    - 운영체제는 공유기억장소만을 제공

### 4.4.2 메시지 시스템 기법

1. 메시지 시스템 기법
    - 메시지 교환방식을 이용하여 프로세스가 서로 정보 교환
    - 통신기능은 send와 receive 연산자의 형태로 제공
    - 보다 소량의 데이터를 교환하는데 유용한 방식
    - 통신기능 제공의 책임은 운영체제에 있음
2. 통신 링크
    - 통신을 원하는 프로세스들 사이에 존재해야 함
    - 논리적 구현에 대한 다양한 이슈 존재
3. 직접 통신
    - 메시지 전달 연산에 수신자나 송신자 이름을 명시
    - send(P, message) : 프로세스 P로 메시지를 보냄
    - receive(Q, message) : 프로세스 Q에서 메시지를 받음
4. 간접 통신
    - 우편함(mailbox 또는 port)을 통해 메시지를 주고 받음
    - 두 프로세스는 공유 우편함을 가질 때만 통신할 수 있음
    - send(A, message) : 우편함 A로 메시지를 본냄
    - receive(Q, message) : 프로세스 Q에서 메시지를 받음
5. 우편함의 소유권
    - 프로세스 소속 : 소유자는 수신만, 사용자는 송신만 함
    - 운영체제 소속 : 우편함은 스스로 존재
6. 링크의 용량
    - ‘0’용량 : 송신자와 수신자는 메시지 전송을 위해 동기화되어야 함.
    - 제한된 용량 : 큐가 가득차면 송신자는 대기해야 함
    - 무제한 용량 : 송신자는 대기할 필요가 없음
7. 예외 조건
    - 프로세스 종료
    - 메시지 상실
    - 메시지 혼합