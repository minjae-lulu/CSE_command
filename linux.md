# 리눅스 명령어 정리

작성자: 익명

# 리눅스 명령어 정리

### ls

- ls → 현재 위치에서 파일보기
- ls -a → 모든 파일 보기
- ls -l → 현재폴더 세세한정보(최근수정)까지 다보기
- ls -l /home → home폴더의 파일 세세하게 보기
- ls -al → 모든 파일 세세한 정보까지 다보기,

### cd (절대경로 → 첨부터, 상대경로 → 현재위치부터 (../))

- pwd → 현재 위치 확인(print working directory)
- cd a → a폴더로 이동
- cd libhcs/build/bin → 한번에 libhcs→build→bin 으로 이동
- cd .. → 상위폴더로 이동 (cd ../../../  연속으로 이동가능)
- cd ../../a/b/c → 폴더 두번나가고 a→b→c로 이동
- cd / → 최상위 디렉토리로 이동

### rm

- rm a.cpp → a.cpp 파일 삭제
- rm *.o → 확장자가 .o인것 모두 삭제
- rm -r a → 폴더(디렉토리) a 삭제

### mkdir, touch (폴더생성)

- mkdir a → 현재위치에서 a 폴더를 만든다
- touch a → 현재위치에서 text파일 a를 반든다.

### mv(이동,이름변경)

- mv file1 file2 → 파일1에서 2로 이름을 변경함
- mv file1 dir1/ → file1을 dri1로 이동함
- mv file1 file2 dir1/ → 여러개파일 한번에 이동가능
- mv dir1/ dir2/ → 디렉토리 이름 1에서 2로 변경

### cp(복사)

- cp file1 file2 → file1을 복사하여 file2를 생성
- cp file1 dir1/ → file 1을 dir1/ 에 복사한다
- cp file1 file2 dir1/ → 여러개 복사 가능
- cp -r dir1/ dir2/ → 디렉토리를 복사하기 위해서는 -r옵션을 사용한다.

### Cat

- cat a.cpp → a.cpp 내용 출력
- cat -n a.cpp → a.cpp내용 번째줄 해서출력
- cat > hey , 입력 ctrl +d → hey파일 생성하고 안에 내용 입력후 저장
- cat >> hey, 입력 ctrl +d → hey파일 뒤에서 이어서 작성후 저장
- cat friend seongmin > uho → 유호 성민 파일합쳐서 friend 만듬
- cat b > a → a파일을 b에 복사

### FInd (find [경로] - name[파일명])

- find → 현재 디렉에서 존재하는 파일, 디렉토리 모두 출력
- find dir1 → dir1에서 존재하는 파일,디렉 모두 출력
ex) find /home/minjae/aaa/ → 절대경로의 home앞에는 / 붙인다. aaa모든것 출력
- find / -name "test" → 최상위 디렉토리에서 test 라는 파일이나 디렉토리 검색
- find . -name "test" →  현재 디렉토리에서 test 라는 파일이나 디렉토리 검색
ex) find . -name time.cpp → 현재,하위 디렉토리에서 time.cpp 위치 출력
- find . -name "B*" → B로시작하는 파일, 디렉 찾기

### 잡것들 모음

- pwd → 현재 위치 확인(print working directory)
- 귀찮게 물어보면 옵션뒤에 f를 붙이면 force라는 뜻으로 강제로 명령 수행함. 단 신중히 사용! ㅋㅋ

## 서버 상태 확인

- top 입력 → 현재 서버 어떤 프로세스가 사용중인지, 얼마나 cpu를 먹는지 확인가능

# 설치관련 명령어!

- apt instlall abc ⇒ abc 패키지 설치 + 의존성 패키지도 설치
- apt remove abc ⇒ abc 패키지 삭제, 설정파일은 삭제안함
- apt purge abc ⇒ 설정파일 포함하여 abc 패키지 삭제함
- apt autoremove ⇒ 더이상 필요없는 패키지들 삭제

- apt show abc ⇒ 패키지 정보 출력
- apt list —installed ⇒ 설치된 패키지 목록 출력
- apt list —upgradable ⇒업글 가능한 패키지 목록 출력

- sudo apt list ⇒ 현재 리스트 불러옴
- sudo apt update ⇒ 패키지 최신화
- sudo apt upgrade ⇒ 리스트 업데이트

## 

### 설치관련 error
- sudo apt-get install update → E: unable to fetch some archives blabla
- sudo apt-get update → E: Unable to locate package upgrade

일단 위에 두 명령어를 치고 다시시도한다!