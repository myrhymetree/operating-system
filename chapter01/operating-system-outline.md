# 운영체제 개요

## 1.1 운영체제의 개요

### 1.1.1 운영체제의 역할

![image](https://github.com/myrhymetree/operating-system/assets/94158097/01203510-655e-47d3-b7c1-36506cb661c8)

1. 운영체제
    - 대표적인 시스템 소프트웨어
    - 컴퓨터 시스템의 자원을 관리하고 컴퓨터 프로그램이 동작하기 위한 서비스를 제공하는 프로그램들의 모음
2. 컴퓨터 시스템의 운영
    - 컴퓨터 시스템의 자원을 제어 및 관리
    - 자원 : 하드웨어 자원, 소프트웨어 자원, 데이터
    - 예 : 저장장치에서 데이터 읽어 오기, 키보드나 마우스 제어, 프로그램 동시 실행 시 CPU와 메모리를 효율적으로 관리
    - 응용 프로그램들의 실행을 도와주는 소프트웨어
    - 컴퓨터 시스템을 효율적으로 운영하는 목적
3. 사용자 지원
    - 사용자의 명령을 해석하여 실행하게 함
    - 사용자와 하드웨어 사이의 매개체 역할 수행
    - 사용자에게 편의성을 제공하는 목적

### 1.1.2 컴퓨터 시스템과 운영체제

1. 운영체제가 없던 초기의 컴퓨터 시스템
    - 응용 프로그램이 직접 컴퓨터 시스템의 자원제어
        - 응용 프로그램 개발자는 하드웨어 제어방법을 잘 알아야 함
    - 여러 사용자가 하드웨어를 공유하는 경우 자원 분할 어려움
    
    ![image](https://github.com/myrhymetree/operating-system/assets/94158097/c2b13658-5f21-4321-a5c6-eaf9508ab4bd)

1. 운영체제가 있는 컴퓨터 시스템
    - 하드웨어와 응용 프로그램 사이에 위치
        - 하드웨어에 대한 제어는 운영체제만 함
        - 응용 프로그램은 운영체제를 통해서만 하드웨어 이용
    - 운영체제가 컴퓨터 시스템의 자원 제어
    - 컴퓨터 시스템이 안정적이고 효율적으로 동작하도록 함

    ![image](https://github.com/myrhymetree/operating-system/assets/94158097/8b12f74f-e933-46ca-a40a-f7d08e73d444)

### 1.1.3 커널 모드와 사용자 모드

1. 커널 모드(슈퍼바이저 모드)
    - 운영체제의 커널이 동작되는 모드
    - 하드웨어를 직접 제어할 수 있는 CPU 명령어 사용 가능
2. 사용자 모드(보호 모드)
    - 응용 프로그램이 동작되는 모드
    - 하드웨어를 직접 제어할 수 있는 CPU 명령어 사용 불가능
3. 시스템 호출
    - 응용 프로그램이 운영체제에 서비스를 요청하는 메커니즘

### 1.1.3 커널

1. 커널(kernel)
    - 커널 모드에서 동작하는 운영체제의 핵심 요소
    - 응용프로그램과 하드웨어 수준의 처리 사이의 가교 역할
2. 일체형 커널(monolithic Kernel)
    - 운영체제의 모든 서비스가 커널 내에 포함됨
    - 커널 내부 요소들이 서로 효율적으로 상호작용을 할 수 있음
    - 한 요소에 있는 오류로 인해 시스템 전체에 장애가 발생할 수 있음
    - UNIX와 Linux 운영체제들이 일체형 커널임
3. 마이크로 커널(microkernel)
    - 운영체제의 대부분의 요소들을 커널 외부로 분리
    - 커널 내부에는 메모리 관리, 멀티태스킹, 프로세스 간 통신(IPC) 등 최소환의 요소들만 남겨 놓음
    - 새로운 서비스를 추가하여 운영체제를 확장하기 쉬움
    - 커널 외부 요소의 문제는 커널 자체에 영향을 주지 않으므로 유지보수가 용이하며 안정성이 우수함
    - 커널 외부 요소들 사이는 프로세스 간 통신(IPC)을 통해야 하므로 성능 저하가 발생함
4. 시스템 호출
    - 응용 프로그램이 하드웨어에 대한 제어가 필요한 경우 이용
    - 운영체제에 서비스를 요청하는 메커니즘

![image](https://github.com/myrhymetree/operating-system/assets/94158097/b248802a-3ae1-4653-b7d5-28d693325c4a)

## 1.2 운영체제의 구성

- 컴퓨터 시스템의 자원의 성격에 따라 구분

![image](https://github.com/myrhymetree/operating-system/assets/94158097/662bb786-5f35-4da2-a3a8-0bb443457f17)

1. 프로세스 관리자
    
    ![image](https://github.com/myrhymetree/operating-system/assets/94158097/fa4c8ab0-17cf-4f0e-a289-6140b77cde21)
    
    - 프로세스를 생성, 삭제, CPU 할당을 위한 스케줄 결정
    - 프로세스의 상태를 관리하며 상태 전이를 처리
2. 메모리 관리자
    
    ![image](https://github.com/myrhymetree/operating-system/assets/94158097/7e634591-ca0d-4038-98c0-81eecba6bdcb)
    
    - 메모리(주기억장치) 공간에 대한 요구의 유효성 체크
    - 메모리 할당 및 회수
    - 메모리 공간 보호
3. 장치 관리자
    
    ![image](https://github.com/myrhymetree/operating-system/assets/94158097/3a5d77d4-ea44-4eab-a843-f506d50a71f1)
    
    - 컴퓨터 시스템의 모든 장치를 관리
    - 시스템의 장치를 할당, 작동 시작, 반환
4. 파일 관리자
    
    ![image](https://github.com/myrhymetree/operating-system/assets/94158097/7abc010b-9661-4a4a-8e73-61dd5bacce20)
    
    - 컴퓨터 시스템의 모든 파일을 관리
    - 파일의 접근 제한 관리
    - 파일을 열어 자원을 할당하거나 파일을 받아 자원을 회수
    - 저장장치의 공간 관리

## 1.3 운영체제의 유형

1. 일괄처리(batch processing) 운영체제
    - 작업을 모아서 순서대로 처리하는 방식
    - 사람(오퍼레이터)이 하던 일을 프로그램이 빠르게 처리하게 되면서 전체적인 작업 처리 속도가 향상됨
    - 나중에 들어온 작업은 앞선 작업들이 모두 끝날 때까지 아무런 상호작용 없이 기다려야만 함
    - 사용자와 상호 작용 없이 순차적으로 실행
    - 주어진 시간 안에 처리된 작업의 수(처리량)와 반환시간으로 효율성 평가
2. 시분할 운영체제(Time-sharing) 
    - Time-sharing
        
        각 사용자의 프로그램을 한 번에 조금씩 수행하는 방식
        
    - 대화형(interactive) 운영체제 라고도 함
    - 사용자들은 마치 혼자 컴퓨터를 사용하는 듯한 느낌을 받음
    - 일괄처리 운영체제보다 빠르지만 실시간 운영체제보다는 느린 응답시간
        - 응답시간 : 요청한 시점부터 반응이 시작되는 시점까지의 소요시간
    - 이용자에게 즉각적인 피드백을 제공
3. 실시간(real-time) 운영체제
    - Real-time
        - 원하는 시간 내에 프로그램의 결과를 얻을 수 있는 방식
    - 가장 빠른 응답 시간
    - 처리의 결과가 현재의 결정에 영향을 주는 환경에서 사용
        - 우주선 비행 시스템, 미사일 제어, 증권 거래 관리 시스템, 은행 입출금 시스템 등에 사용
    - 중요한 작업에 대한 처리 기한을 맞추는 것이 중요
        - 우선순위가 높은 작업을 우선 처리할 수 있는 기법 활용
4. 하이브리드(hybrid) 운영체제
    - 일괄처리 운영체제와 대화형 운영체제의 결합
    - 이용자는 터미널을 통해 접속하고 빠른 응답시간을 얻음
    - 대화형 작업이 많지 않을 경우 백그라운드에 배치 프로그램 실행
    - 현재 사용되고 있는 대부분의 대형 컴퓨터 시스템은 하이브리드 운영체제
5. 분산 운영체제
    - 분산 시스템을 관리하기 위한 운영체제
        - 분산 시스템 : 2개 이상의 컴퓨터 시스템이 네트워크로 서로 연결되어 서로의 자원을 이용하는 시스템
    - 다른 컴퓨터 시스템의 자원을 이용하는 것이 마치 자신의 컴퓨터 시스템에 있는 자원을 이용하는 것처럼 가능해야 함

## 1.4 운영체제의 역사

1. 1940년대 : 초기 전자식 디지털 컴퓨터
    - 운영체제가 존재하지 않음
    - 기계적 스위치에 의해 작동
2. 1950년대 : 단순 순차처리 및 단일흐름 일괄처리
    - 한번에 오직 하나의 작업만을 수행
    - 최초의 운영체제 등장(IBM 701용)
3. 1960년대 : 멀티프로그래밍
    - 멀티프로그래밍, 멀티프로세싱, 시분할 처리 개념
    - 다중 대화식 사용자 지원
4. 1970년대 : 멀티모드 시분할
    - 일괄처리, 시분할 처리, 실시간 처리를 지원하는 멀티모드 시분할과 보편화
    - 근거리 지역 네트워크(LAN)의 실용화
    - 정보보호 및 보안 문제의 증대로 암호화의 중요성 대두
5. 1980년대 : 분산 네트워크
    - 운영체제 기능이 하드웨어 자체에 포함된 펌웨어 개념의 대두
    - 2개 이상의 프로세서를 이용하는 멀티프로세서 환경
    - 개인용 컴퓨터 및 워크스테이션의 시대
    - 네트워크의 대두와 함께 클라이언트/서버(client/server) 모델 확산
6. 1990년대 : 병렬처리 및 분산처리
    - 순차처리를 벗어나 분산 및 병렬 처리가 발달
    - CPU 사용 비용 낮아짐
    - 네트워크와 멀티미디어 처리 기술 발달
    - 인터넷 보급의 급속한 확산
    - 그래픽 사용자 인터페이스(GUI)의 강화
    - 선점형, 멀티태스킹, 멀티쓰레딩, 가상 메모리의 보편화
7. 2000년대와 그 이후 : 모바일 및 임베디드 운영체제
    - 시스템은 고속화 · 고기능화 · 경량화 방향으로 발전
    - 다양한 통신망의 확대와 개방형 시스템의 발달
    - 운영체제는 기능 다양화, 확장성과 호환성 및 사용자 편의성 향상
    - 네트워크 기바느이 분산 및 병렬 운영체제의 보편화
    - 클라우드 환경의 운영체제
    - 64비트 CPU에 호환되는 64비트용 운영체제
    - PDA, PMP, 스마트폰, 태블릿 등의 모바일 장치와 대중화로 모바일 운영체제 보편화
    - 가전제품을 위한 임베디드 운영체제의 보편화
