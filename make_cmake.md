# make, cmake 에 대해서

작성자: 이민재

소프트웨어를 배포할 때 특정 IDE의 프로젝트 파일을 배포하게 되면 그 소프트웨어를 받아서 쓰는 사람도 특정 IDE를 설치해야 하는 번거로움이 있다. 그런 번거러움을 해결하고자 make cmake등을 사용한다.

- gcc : GNU compiler collection 의 약자로 C/C++의 컴파일러이다.
- make :  여러단계의 gcc 명령을 Makefile 이라는 스크립트로 만들어 한번에 실행하게 하고, Incremental build를 지원한다.
- gmake : 리눅스에서 make와 같다.
- cmake : 중간 단계를 일일이 지정 해야하는 makefile을 좀 더 편리하게 하기 위해
- CmakeLists.txt 라는 스크립트를 이용해 더 편리하게 Makefile 관리함

## GCC 내맘대로 정리

- 전처리 (.c → .i) : #include #define 을 먼저 처리함
- 컴파일 (.i → .s) : high → low level로 바꿔줌. 목적파일로 변환. 이때오류는 문법오류로 소스파일 수정해야함
- 어셈블 (.s→.o) : 기계어로 변환
- 링크 (.o → .exe) : 링커가 여러개의 오브젝트 파일을 합치거나, 라이브러리와 합침

- gcc는 c전용, g++은 c++ 전용이다.
- g++ -o a a.cpp → a.cpp 파일로 a.exe 파일 생성 (그후 ./a 로 실행가능)
- g++ -E a.cpp → 전처리 까지만 하고 그 결과 출력 (많이 출력됨)
- g++ -c a.cpp -> .o 파일 생성(전처리, 컴파일, 어셈블까지함)
- g++ a.o -o a → 목적파일(a.o)을 통해 실행파일(.exe) 생성

## GCC 분리 컴파일과 makefile 필요성

![make,%20cmake%20%E1%84%8B%E1%85%A6%20%E1%84%83%E1%85%A2%E1%84%92%E1%85%A2%E1%84%89%E1%85%A5%2073c571d73a474a569b8149379b5b481c/1.png](make,%20cmake%20%E1%84%8B%E1%85%A6%20%E1%84%83%E1%85%A2%E1%84%92%E1%85%A2%E1%84%89%E1%85%A5%2073c571d73a474a569b8149379b5b481c/1.png)

![make,%20cmake%20%E1%84%8B%E1%85%A6%20%E1%84%83%E1%85%A2%E1%84%92%E1%85%A2%E1%84%89%E1%85%A5%2073c571d73a474a569b8149379b5b481c/2.png](make,%20cmake%20%E1%84%8B%E1%85%A6%20%E1%84%83%E1%85%A2%E1%84%92%E1%85%A2%E1%84%89%E1%85%A5%2073c571d73a474a569b8149379b5b481c/2.png)

hi.cpp와 main.cpp를 각각 실행하면 실행 안됨. 방법 2가지 있다.

1. g++ main.cpp hi.cpp -o test (두파일을 함께 컴파일해 test.exe 생성)
2. g++ -c main.cpp
g++ -c hi.cpp
g++ main.o hi.o -o test (각각 목적파일을 만들고 두개의 목적파일로 test.exe생성)

1번보다는 2번을 선호 (.o파일을 만들기 떄문)
목적파일을 만드는 이유 : 소스파일의 보안, 작업의 분업화, 프로그램의 모듈화, 이식성과 확장성 높이기 위해서

하지만 파일 하나가 수정될 경우 매번 파일들을 g++ -c ~~ 하면서 목적파일을 만들어 줘야 하는데 파일이 매우 많은경우에는 귀찮다. 그래서 여러가지 방법이 있는데, 자동화를 가장 편리하게 만든게 makefile 이다. makefile은 목적 파일이 수정되었을 경우 새로운 .o파일을 생성하고, 수정이 되지 않았을 경우는 그냥 넘어간다. 

## Makefile 기본 사용법

(기본 틀) 
만들어질 것 : 필요한것
(tab)     실행명령줄

위에 상황을 예시로 들어보면 아래처럼 makefile 을 만들어서 사용 가능하다. make를 입력해보면 정상작동. 하나의 파일을 수정하고 make하면 그 수정된것과 관련된것의 파일들이 새로만들어지고 test파일은 수정에 맞게 실행된다! 

all : test                    (make all 하면 test를 만들기위한 작업 시행)
test : main.o function.o
    g++ -o test main.o function.o
main.o : function.h main.cpp
    g++ -c -o main.o main.cpp
function.o : function.h function.cpp
    g++ -c -o function.o function.cpp

clean :                         (make clean 하면 아래명령어 실행되며 목적파일, test파일 삭제)
    rm *.o
    rm test

여기서 make → 파일에서 맨위의 target을만들기 위한 실행 (all을 사용하는 이유)
 make main.o → main.o 만 만드는 명렁어만 실행 (고프떄 make a 가 이런느낌)

![make,%20cmake%20%E1%84%8B%E1%85%A6%20%E1%84%83%E1%85%A2%E1%84%92%E1%85%A2%E1%84%89%E1%85%A5%2073c571d73a474a569b8149379b5b481c/3.png](make,%20cmake%20%E1%84%8B%E1%85%A6%20%E1%84%83%E1%85%A2%E1%84%92%E1%85%A2%E1%84%89%E1%85%A5%2073c571d73a474a569b8149379b5b481c/3.png)

(예제에서는 add 대신 function 파일 사용 헤더파일과 main.cpp 어떻게 연결해서 동작하는지 참고하라고 붙여놓음)

## Makefile 변수사용법

CC = g++                    (이렇게 변수 지정할수 있음)
$(CC)                         (g++ 대신 CC 사용하면 됨 단 변수사용할떄는 $() 안에 넣어줘야함)

CFLAGS = -o, OBJS = main.o function.o, TARGET = test 등등 이렇게 해서 사용도 가능

(난 사실 cmake가 중요해서 추후 makefile 공부하면서 더 업데이트 할게용!)

## CMake의 필요성

프로젝트의 규모가 커지면서 관리해야할 소스 파일들이 많아지고, 의존성 관계가 서로 복잡하게 엉키면서 Makefile로는 빌드가 꼬이기 시작하고, 매번 clean build를 해야해서 불편. makefile을 자동생성함. 그래서 Cmake를 사용해 의존성 정보를 일일이 기술하지 않고, step잘 구성하면 소스코드를 수정하더라도, 스크립트를 수정하지 않아도 됨

주로 깃헙에서 오픈소스를 받으면 거의 CMakeLists.txt 가 있는데 이를 통해 빌드할수 있다. 오픈소스를 다운받는 사람마다 다양한 OS를 가지고 있는데 Cmake를 통해 여러 OS에서도 문제없이 빌드하기 위해 필요하다. (unix, ms, mac 다가능)

이것 이외에도 단순한 구문, 여러 호환성 등등 다양한 이점이 있다.

정리잘된 글 : [https://gist.github.com/luncliff/6e2d4eb7ca29a0afd5b592f72b80cb5c](https://gist.github.com/luncliff/6e2d4eb7ca29a0afd5b592f72b80cb5c)

## CMake 사용법

- Cmake 설치후, CMakeLists.txt 파일을 만듬 (대소문자 구분)
- CMakeLists.txt 파일의 맨위에 cmake_minimum_required(VERSION x.x) x.x는 최소버전
- PROJECT ("프로젝트명") 프로젝트명이 씨메잌프로젝트네임 변수에 저장됨
- MESSAGE ([<Type>] <메세지>) → 콘솔에 출력함
MESSAGE (${CMAKE_PROJECT_NAME})  → 프로젝트 이름 콘솔에 출력

- 빌드 대상 (Target) : 모든 빌드가 끝나고 최종적으로 출력되는 실행파일과 라이브러리

1. ADD_EXECUTABLE (<실행파일명> <소스파일> <소스파일>...) → 소스파일로 실행파일생성
ADD_EXECUTABLE (test main.cpp foo.cpp bar.cpp) → 3개로 test 파일 만듬

2. ADD_LIBRARY(<라이브러리명> [STATIC|SHARED|MODULE] <소스파일> <소스파일> ...) 라이브러리명, 라이브러리 종류(생략시 STATIC) 라이브러리 생성하는데 필요한 소스파일
ADD_LIBRARY (app STATIC foo.cpp bar.cpp) → libapp.a 라는 라이브러리 생성

3. ADD_CUSTOM_TARGET(
    <이름> [ALL]
    [COMMENT <출력메시지>] 등등 많음 생략함
)

4. ADD_DEPENDENCIES (<타겟명> <의존대상> <의존대상>)
- LINK_LIBRARIES - 링크 옵션 추가
LINK_LIBRARIES (<라이브러리명> <라이브러리명>) → 링크시 사용할 라이브러리 추가

1. CMAKE_EXE_LINKER_FLAGS_<빌드 형상> 

2.  SET(RUNTIME_OUTPUT_DIRECTORY output/bin) → 빌드한 실행 바이너리를 output/bin 에 저장한다.

3. SET (LIBRARY_OUTPUT_DIRECTORY output/lib) → 빌드한 라이브러리를 프젝폴더 내의 output/lib에 저장

4. SET (ARCHIVE_OUTPUT_DIRECTORY output/lib/static) → 빌드한 아카이브를 프젝폴더 내의 output/lib/static에 저장한다.
- 변수 정의 
SET ( <변수명> <값>)
SET ( <목록_변수명> <항목> <항목> <항목> ... ) 
변수를 참조할때는 $을 붙이거나 ${}을 사용한다.

SET ( SRC_FILES main.c foo.c bar.c)
ADD_EXECUTABLE ( test ${SRC_FILES}) → 이런식으로 사용가능

## CMake 실행법

- 파일 작성후 터미널에 cmake CMakeLists.txt 입력한다. 그럼 파일들이 촤라락 생김
- cmake 로 만든 makefile이 생성되고 make를 입력하면 cmake 가 만든 makefile 실행되면서 .exe파일이 생성되고 ./test 해서 실행가능