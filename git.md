# 깃 사용법

작성자: 이민재

# 깃 사용법

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    (token)

- git init → 깃관리 시작
- rm -r .git → 깃관리 해제

- git clone http:~~~~~ → 레퍼지토리 파일을 가져옴
- git remote -v : 현재 remote 확인
- git branch :

- git config —global [user.name](http://user.name) "이름" → 깃 관리자명 설정
- git config —global [user.](http://user.name)email "이메일" → 깃 관리자 이메일 설정
- git config [user.name](http://user.name) → 깃 관리자명 출력
- git config [user.email](http://user.email) → 깃 관리자메일 출력

- git status → 깃의 현재 상태 확인
- git log → 깃들의 역사, 타임라인을 확인

- git add . → 모두 add함
- git commit -m "바보야" → 커밋 메세지 바보야를 등록
- git push → 레퍼지 토리에 올림
- git pull → 레퍼지토리에 다른사람이 수정한것을 업데이트 (Merge까지)
- git fetch → 레퍼지토리에 다른사람이 수정한것을 업데이트 (Merge X)

## 깃 오류

- Git push 오류 (서버에서 작업중 컴퓨터를 바꿨을때 push 하면 발생하는것 같음)
Missing or invalid credentials. Error : connect EcoNNREFUSED /~~~~/ errno: -111
git config --unset --global [user.name](http://user.name/)
git config --unset --global user.emaill
git config --unset --global credential.helper
입력후 vscode 껐다 키면 됨
- 

## 깃 연결 해제

- 깃과 리퍼지토리 연결 끊기
gir remote 입력 : 현재 연결된 레퍼지토리 있는지 확인 (대부분 origin 이라 뜰꺼임)
git remote remove origin 입력 : origin 레퍼지토리와 연결 해제
해제한후 git remote 로 다시 연결되어있는지 확인 아무것도 안뜨면 연결 끊긴것!

- 깃관리 해제
.git 파일 삭제하면 된다! 그래서 명령어에
rm -r .git 입력후 yes 계속 눌러주고, 다시 rm -r . git 해서 확인! 그럼 색깔들 사라질것이다!

## 깃 서브모듈(큰 프로젝트 다른팀들과 협업할때)

→ 자식 repo 작업자

1. 받기 : git pull로 부모 repo 작업자들이 업데이트 해놓은것을 받는다
2. 올리기 : 작업한후 git push 해준다

→ 부모 repo 작업자

1. 받기 : git pull로 부모 repo 받고, git submodule update로(or 자식 repo 에서 git pull) 서브모듈도 업데이트 해준다. 서브 모듈 변경사항이 잘 안되는 경우 **git pull origin main**을 입력해본다 
2. 올리기(부모 Repo) : 부모 repo에서 git push
3. 올리기(자식 Repo) : 자식 repo에서 git push, 이후 무보 repo에서도 git push 둘다 업데이트해줌 좋음

- git submodule add (주소) → 제일 상위의 레퍼지토리 디렉토리에서 실행
- git pull → 상위 디렉토리에서 submodule 디렉에 가서 실행하면, sub 업데이트 떙겨온다. 그후 상위레퍼디렉에서 git push
- 끊기 : 
1. .gitmodules 파일 전부 지우고 삭제
2. git rm —cached (sub디렉 경로)
3. rm -rf .git/modules/(sub module) → 필수는 아님
4. rm -rf (서브모듈 폴더)

- [https://www.youtube.com/watch?v=TAe4uZqYt6c](https://www.youtube.com/watch?v=TAe4uZqYt6c) (유튜브 강의 디테일)
- [https://ohgyun.com/711](https://ohgyun.com/711) (설명잘된 블로그)

# 깃 RP, merge 에 대해

소스트리를 사용해보자, 깃의 브랜치를 시각화도 지원하고, 명령어 없이 머지 생성 등등 가능하다.

→ 깃은 여러명이 같이 사용하면, 각자 작업을 하기위해 따로 branch를 만들고 그것을 rp(request pull) 요청하고 허락하거나 확인이 되면 merge하는 방식으로 현업, 작업 등에 사용되고 있다. → 충돌예방, 작업세분화

git branch “이름” → 이름의 branch를 만든다

git branch -d “이름” → 이름의 branch를 삭제한다.

git checkout “이름” → 이름의 branch로 바꾼다

git checkout master → 다시 원래 main branch로 전환한다. (origin이랑 헷갈림 주의)

git add . / git commit -m “m” ./ git push origin “이름” → 새로 만든 브랜치의 상태에서 똑같이 해준다.

(origin 은 깃헙의 가상 저장소를 말하고 “이름”은 나의 로컬에 있는 저장소를 말한다. git push origin “이름”의 의미는 나의 로컬에 있는 이름이라는 깃을 origin 사이트에 있는 가상 저장소로 push 한다는 의미정도쯤이다.)

→ 그럼 깃헙의  pull request에 들어가면, 새로 request 할것을 추천해주는데 그것을 누르면 된다.

→ 그후 사람들이 확인하고, 코멘트나 어셉을 한다. 관리자가 있다면 그것을 merge하는 버튼을 누르고, 그게 나이거나 상관없다면 올린사람이 merge하기도 한다.

→ branch 충돌이 일어나면 rem?? 뭐시기를 하거나, 아에 삭제한다음, 새로 만드는것도 가능하다.