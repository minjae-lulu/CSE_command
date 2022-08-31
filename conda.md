# conda 사용법 (가상환셩)

작성자: 익명

conda info —envs → 현재 가상목록 확인

conda env list → create된 env를 확인

conda remove -n 가상환경이름 —all → 가상목록 삭제

conda create --name 환경이름 python=3.x →가상환경 만들기

conda activate 환경이름 → 가상환경 활성화

conda deactivate → 가상환경 비활성화(이름 안적어도 됨)

conda list(pip list) → 패키지 확인

conda install 패키지이름 → 패키지 설치

conda remove 패키지명 → 패키지 삭제(활성화상태일때)


## requirements.txt파일 
이것을 사용하면 쉽게 바로바로 다 설치할수 있음

pip install -r requirements.txt → 입력하면, requirements.txt에 적힌 것들 pip명령어로 모두 설치

pip freeze > reqirements.txt → 입력하면 현재 activate된 가상환경이나 현재 python에 pip으로 설치된 패키지 목록 모드 requirements.txt에 담아서 생성됨