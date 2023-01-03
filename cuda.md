## 그래픽카드 -> cuda version -> torch version 순으로 맞춰야한다!
<br><br>

#### grapic card information
```
$ nvidia-smi
or
$ conda info
```


#### conda를 써서 파이토치 cuda버전에 맞게 설치 명령어 찾기 [https://pytorch.org/](https://pytorch.org/)

#### 파이토치 버전 확인 
```
$ print(torch.__version__)
```

#### cuda version 확인 (nvidia-smi나오는건 추천 버전임)
설치 안될시 cuda toolkit을 설치해야 한다. 
```
$ nvcc --version 
```

#### cuda toolkit 설치
```
$ sudo apt install nvidia-cuda-toolkit
```


#### cuda 밀기, cuda 버전맞게 설치
[https://whiteglass.tistory.com/15](https://whiteglass.tistory.com/15)

#### cuda 관련 오류
처음에 pycash 등등 어떤 package가 설치가 gpu에 맞게 안되고 cpu에 맞춰져서 뭔가 문제를 일으킬수 있다. 깃헙 이슈를 보면 주로 package때문이라고 하는데, 이거 설치 되어있는데 왜그러지? 한다. 하지만 이는 cpu에 맞춰져있기 때문에고, 
```
$ pip uninstall [package]
$ pip cache remove [package]
$ pip install [package]
```


### 자주보는 오류
The current Pytorch install supports CUDA capabilites sm_37 sm_50 sm_60 sm_61 sm_70 sm_75 compute _37. If you want to use the NVIDIA GeForce RTX 3080 GPU with PyTorch, please check the instructions at ~~~~~~.

-> 저런 문구가 뜨면서 어떤 싸이트 하나를 추천해주는데, 저기서 적당한 버전으로 올려주면 됨. pytorch cuda공식 사이트임


