# 운영체제 사례

## 12.1 Linux

### 12.1.1 리눅스의 개요

1. MINIX
    - 1987년 Andrew S. Tanenbaum 교수가 개발
    - 유닉스(UNIX) 기반의 마이크로 커널 구조
    - 아주 작은 수업용 운영체제
2. Linux
    - 1991년 Linus Torvalds가 MINIX를 수정하여 만듦
    - GNU GPL하에 커널 소스를 공개하여 급속히 발전
    - 일체형 커널 구조
    - 소스 공개
    - 개발자 뿐 아니라 일반인 및 기업용으로 사용 가능한 운영체제
    - 인텔 CPU뿐 아니라 ARM 등 다양한 CPU 지원
    - 실습용 컴퓨터부터 슈퍼 컴퓨터까지 널리 사용됨

### 12.1.2 리눅스의 장단점

1. 장점
    - 유닉스와 완벽하게 호환
    - 공개 운영체제
    - 안정적인 운영체제
    - 무료 운영체제
    - 낮은 성능의 하드웨어에서 동작 가능
    - 하드웨어의 기능을 효과적으로 사용
    - 강력한 네트워크 및 멀티태스킹 지원
    - 다양한 응용프로그램 제공
    - 인터넷의 모든 기능을 지원
    - 개인용 컴퓨터에서 서버 기능 수행 가능
2. 단점
    - 공개 운영체제이므로 문제점 발생 시 보상받을 수 없음
    - 교육, 유지보수 문제
    - 보안 문제가 상대적으로 심각할 수 있음
        - 생소한 사람이 환경설정 세팅할때 문제 발생 가능성
    - 떨어지는 보급율
        - 초보자가 사용하기 어려움
    - 특정 하드웨어가 지원되지 않을 수 있음
        - 최근에 좋아지고 있음

### 12.1.3 리눅스 커널

![image](https://github.com/myrhymetree/operating-system/assets/94158097/2c1f42d9-9650-4313-a6dd-5476303848c2)
![image](https://github.com/myrhymetree/operating-system/assets/94158097/0d261e0c-a35b-425e-8eed-0f16da6d60d1)

1. 특징
    - 일체형 커널
        - 소스가 공개되어 있기 때문에 필요 없는 부분은 제거 가능
    - 멀티태스킹, 멀티유저 시스템
    - 멀티코어, 멀티프로세스 시스템
    - 여러가지 하드웨어 지원(멀티플랫폼)
        - 리눅스의 대부분은 C언어로 작성되어 있어 다양한 플랫폼에 손쉽게 이식됨
    - POSIX 표준 준수
        - IEEE에서 지정한 운영체제간 호환성을 유지하기 위한 표준
        - POSIX를 준수하는 운영체제는 POSIX를 준수하는 다른 운영체제와 호환되어야 함
        - 참고 : [https://velog.io/@bjk1649/POSIX란](https://velog.io/@bjk1649/POSIX%EB%9E%80)
    - 프로세스 간 통신 지원
        - 세마포어, 메시지 큐, 공유 메모리 등
    - 페이징
    - 유닉스 시스템 V IPC 지원
    - 다양한 파일 시스템 지원
        - ext4, FAT, NTFS(윈도우), HPFS(OS2) 등
    - 다양한 실행 파일 형식 지원
    - 네트워킹
    - 공유 라이브러리
    - 모듈 형태로 커널에 새로운 기능 추가
        - 필요한 서비스를 모듈로 만들어, 커널을 교체하거나, 시스템을 재시동하지 않고 기능 추가 가능
    - 광범위한 주변장치 지원
    - 파일 형태의 주변장치 접근

### 12.1.4 임베디드 리눅스

1. 임베디드 시스템
    - 미리 정해진 특정한 기능들을 수행하기 위해 하드웨어와 소프트웨어가 결합된 특수 목적 컴퓨터 시스템
    - 한 가지 일을 잘하도록 설계된 시스템
    - 예 : 세탁기
        - 여러 센서를 이용하여 물의 양, 세탁물에 대한 정보 등 측정
        - 효율적인 세탁을 위해 임베디드 시스템의 제어를 통한 동작
    - 보통 실시간 시스템에 이용됨
2. 임베디드 운영체제
    - 임베디드 시스템에서 동작하는 운영체제
    - 최근의 임베디드 운영체제는 실시간 운영체제임
3. 실시간 시스템
    - 시스템의 상황과 무관하게 정해진 마감시간 내에 주어진 이벤트에 반응해야 함
    - 실시간 운영체제(ROTS)는 빠르게 주어지는 마감시간 내에 작업을 처리하는 데 중점을 둠, 정해진 시간 내에 필요한 결과를 얻을 수 있음
    - 경성 실시간 시스템(Hard real-time system)
        - 정해진 시간 내에 반드시 작업한 결과가 절대적으로 출력되어야 하는 시스템
        - 전투기 비행 제어 시스템, 핵발전소 제어 시스템, 인공위성 제어 시스템, 심박동기 등
    - 연성 실시간 시스템(soft real-time system) : 정해진 시간 내에 작업의 결과가 나오지 않더라도 치명적인 결과를 양산하는 시스템이 아닌 경우(마감시간 내 작업을 완수하면 좋지만 못해도 실패x)
        - 기준에 따라 어떤 작업을 완수할 것인가 결정해야 함
        - 디지털 멀티미디어 장치 등
4. 임베디드 리눅스
    - 저성능의 CPU와 소용량의 메모리를 가진 임베디드 시스템 용으로 개발된 리눅스
5. 임베디드 리눅스의 필수 조건
    - 소용량 메모리를 감안하여 리눅스의 크기와 기능을 최소화 · 경량화하고, 목표 시스템에 맞게 쉽게 재구성이 가능해야 함
    - 저성능 프로세서가 채용되는 상황을 감안하여 임베디드 리눅스의 성능이 최적화 되어야 함
    - 리눅스는 원래 범용 컴퓨터 시스템을 위한 운영체제이므로 실시간 처리에 대응할 수 있어야 함
6. 임베디드 리눅스의 장점
    - 검증된 코드로 효율적 · 안정적이며 성숙된 내용
    - 운영체제를 응용에 적합하게 수정 가능
    - 운영체제의 최신 동향 반영
    - 리눅스에 익숙한 개발자는 빠르게 적응 가능
    - 로열티 없음
    - 코드의 최소 · 최적화가 용이
    - 다양한 네트워크 코드와 장치 드라이버 제공으로 넓은 적용 영역
    - 실시간 지원
7. 임베디드 리눅스의 단점
    - 개발환경 접근이 어려움
    - 경성 실시간 시스템에 적절하지 못하고 요구되는 H/W 사양 높음

## 12.2 Window

1. 윈도우 운영체제
    - 1985년 마이크로소프트 사에서 GUI를 제공하는 것을 목적으로 개발
    - IBM-PC상에서 GUI를 실현

### 12.2.1 윈도우의 특징

1. Windows 1.0 : 16비트 멀티태스킹 GUI 환경
2. Windows 2.0 : 중첩 윈도 사용
3. Windows 3.0 : 보호모드(사용자 모드)에서 윈도우가 동작, 가상 메모리 지원, 아이콘 기반 프로그램 관리자, 트리 구조 파일 관리자 사용
4. Windows 95, 98
    - 이전과 달리 윈도우 안에 MS-DOS 포함
    - 32비트 다중 쓰레드 선점형 멀티태스킹 지원, 16비트 프로그램에 대한 호환성 유지를 위한 하이브리드 16비트/32비트 운영체제
5. Windows NT
    - 서버 및 사무용 데스크톱 운영체제로 보안과 신뢰성을 강조, OS/2 및 POSIX 서브 시스템 제공, IIS 웹서버 내장, 분산 파일 시스템 지원
    - POSIX 표준 및 Windows 3.0 API를 지원하는 Win32 추가
6. Windows XP
    - Windows NT 커널을 기반으로 Windows 9x 사용자 편의성을 합침, 원격 데스크톱 기능 지원
7. Windows Vista
    - 64비트 지원, 향상된 NUMA 지원, IPv6 지원
8. Windows 7
    - Windows Vista의 점증적 업그레이드, SSD 지원, 암호화 파일 시스템
9. Windows 8
    - 모바일 운영체제와의 경쟁력 제고, Metro UI, 라이브 타일
10. Windows 10
    - 멀티 데스크탑, 코타나 음성인식, 마이크로소프트 에지 브라우저 지원

### 12.2.2 윈도우 커널

![image](https://github.com/myrhymetree/operating-system/assets/94158097/0141e2bd-469d-4037-86ef-aa96976579dc)
![image](https://github.com/myrhymetree/operating-system/assets/94158097/7ece1baa-a330-4078-9167-472bf0beb3db)

1. 사용자 모드와 커널 모드
    ![image](https://github.com/myrhymetree/operating-system/assets/94158097/12ad35e8-d722-4a47-828e-8446d79d54e0)
    - 마이크로 커널
        - 컴퓨터과학에서 운영체제에 추가되어야 하는 메커니즘을 최소한으로 제공하는 초소형 커널
        - 낮은 수준의 주소 공간 관리, 스레드 관리, 프로세스 간 통신(IPC) 포함
        - 참고 : [https://ko.wikipedia.org/wiki/마이크로커널]            (https://ko.wikipedia.org/wiki/%EB%A7%88%EC%9D%B4%ED%81%AC%EB%A1%9C%EC%BB%A4%EB%84%90)
    - 마이크로 커널을 확장한 형태
        - 커널 모드에서는 마이크로커널 위에 여러 서비스가 동작
            - I/O 관리자, Win32 윈도우 관리자 GDI, 보안 참조 모니터, LPC 기능, 가상 메모리 관리자, 객체 관리자, 프로세스 관리자 등
        - 사용자 모드에서는 OS/2, POSIX, Win32에 대응되는 하위 시스템이 동작
        - NT API가 커널 모드와 사용자 모드를 연결
    - I/O 관리자
    - Win32 관리자와 그래픽 장치 인터페이스(GDI)
        - 사용자의 입력과 화면 출력을 제어
        - Win32 하위 시스템이지만 성능 향상을 위해 커널 모드에서 동작
    - 보안 참조 모니터
        - 자원의 접근 가능 여부 점검
    - LPC(Local Procedure Call) 기능
        - 같은 기계에서 동작하는 프로세스 사이의 정보교환
    - 가상 메모리 관리자
    - 객체 관리자
        - 다른 서비스가 자원을 접근하려면 거쳐야 하는 자원 관리 서비스
        - 모든 자원은 객체로 간주
    - 프로세스 관리자
3. 수정 마이크로 커널
    - 마이크로 커널과 일체형 커널의 적절한 혼합
    - 프로세스 관리자나 가상 메모리 관리자 등 기본적인 운영체제의 서브 시스템은 커널 모드로서 동작
    - 여타 운영체제 환경들(DOS, Win16, Win32, OS/2, POSIX 등)은 별도의 프로세스로 실행
4. 윈도우 실행부
    - NT 운영체제의 가장 거대한 부분
    - 객체 관리자, 프로세스 관리자, 가상 메모리 관리자, I/O 관리자, 로컬 프로시저 호출 기능, 보안 참조 모니터, 윈도우 관리자와 그래픽 장치 인터페이스(GDI) 등의 여러 컴포넌트로 구성
    

## 12.3 Android

### 12.3.1 모바일 환경의 요구조건

- 배터리로 동작하기 때문에 전력 소모량을 줄여야 함
- 대부분 무선 네트워크로 인터넷에 연결됨
- 터치 스크린 등 입출력장치가 일반적인 PC 환경과 다름
- 저수준 운영체제와 고수준 사용자 인터페이스가 결합된 형태

### 12.3.2 대표적인 모바일 운영체제

- 안드로이드
- iOS

### 12.3.3 안드로이드의 개요

- 2008년 처음 발표
- 스마트폰에서 가장 널리 사용되고 있음
- 셋톱 박스, 스마트 TV, 자동차 등 사용 범위가 넓어지고 있음

### 12.3.4 안드로이드의 특징

- 기본적으로 소스는 공개되어 있지만, 회사에 따라 디바이스 드라이버 등이 비공개되는 경우가 늘고 있음
- ARM, x86 CPU 지원
    - 다른 CPU 지원도 이론적으로 가능
- 리눅스에 기반한 일체형 커널 구조
- C, C++로 구현된 운영체제에 Java로 개발된 응용 프로그램 동작
- iOS에 비해 다양한 하드웨어를 지원하기에 파편화 문제 존재
    - 파편화 문제 : 특정 H/W에서만 동작하는 S/W 존재 가능
- 안드로이드 런타임(ART)
    - 응용 프로그램을 처음 설치할 때 중간 코드를 실제 기계 코드로 번역하고 이후 실행할 때 번역된 코드를 실행해 성능을 높임
    - 설치 시 코드를 번역하는 과정이 포함되기 때문에 설치에 시간이 더 걸림
