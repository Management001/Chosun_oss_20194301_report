# Chosun_oss_20194301_report: 조선대학교 오픈소스소프트웨어 03분반 제 2차 과제 작성
# 학과 : 컴퓨터공학과 / 학번 : 20194301 / 이름 : 강정태 
## 1
### 2
#### 3
##### 4
###### 5
####### 6

---
***
---
***


## Linux top 명령어

### top 명령어란?

실시간으로 CPU 사용률을 체크해주는 도구이다. 윈도우의 작업관리자와 비슷하며, 리눅스를 사용하는 서버의 현재 성능이나 동작하는 프로세서의 상황을 볼 때 사용한다.

### top 사용법


```
root#> top 
```



### 요약 영역

요약 영역은 top에서 상단에 위치하고 있습니다. 이 요약영역은 전체 프로세스가 OS에 대해서 리소스를 어느정도 차지하고 있는지를 알려줍니다. 요약 영역에 나타나는 대표적인 값은 시간, 유저, 로드 에버리지(Load Average), 테스크(Tasks), CPU, 메모리(memory)로 아래의 이미지를 보시면 각 영역에 대해 나태내는 값이 어디에 위치하는지 알 수 있습니다.
![image](https://user-images.githubusercontent.com/44454495/170070022-1a0a1091-964e-4881-8cae-010135a31ced.png)



### 시스템 현재 시간, OS가 살아있는 시간, 유저 세션수(System time, uptime and user sessions)

이미지의 가장 왼쪽 위를 보시면 시스템 현재 시간, OS가 살아있는 시간, 그리고 유저의 세션수가 표시되는 영역이 있습니다. 가장 먼저 보이는 숫자가 시스템의 현재 시간입니다. 이 시간은 GMT 기준으로 표시됩니다. 위 예제 기준으로 GMT 16:58:55 이라는 것입니다. 이것은 한국시간으로 보면 +9를 한 00시 58분 55초와 동일합니다. 다음으로 표시되는 것이 OS가 얼마나 살아있는지 나타냅니다. days와 시간으로 표시되며 위 예제로보면 7일과 1시 15분 동안 서버가 살아있었다는 것을 알 수 있습니다. 그리고 다음 나타나는것이 현재 접속중인 유저 세션 수입니다.

좀 더 자세한 유저세션이 궁금하다면 who 명령어를 통해 알 수 있습니다.
![image](https://user-images.githubusercontent.com/44454495/170070053-fd77ae6e-5255-49d5-aa7b-038c90d1bdbb.png)



### 로드 애버리지(Load Average)

2번째 영역은 로드 애버리지 영역입니다. 해당 영역은 CPU Load의 이동 평균를 표시합니다. 앞에서 부터 1분, 5분, 그리고 15분에 대한 평균값입니다. CPU Load란 CPU가 수행하는 작업의 양 입니다. 리눅스에서는 실행되거나 대기중인 프로세스의 평균입니다. 싱글 코어일 경우 1.0의 값이 CPU 100%를 사용하고 있다는 의미입니다. 멀티 코어라면 해당 코어수 만큼 * N을 한 값이 CPU 100%를 사용한다는 의미가 됩니다. 만약 100%를 넘어간다면 CPU에서 처리하지 못하고 대기하고 중인 프로세스가 있다고 보시면됩니다.



### Tasks

2번째 줄에는 Tasks에 관한 내용이 출력됩니다. Tasks는 현재 프로세스들의 상태를 나태내주는 영역입니다. Total은 전체 프로세스, running은 running 상태인 프로세스, sleeping은 대기상태인 process, stopped는 종료된 프로세스, zombies는 좀비상태인 프로세스의 수를 나타냅니다.
프로세스는 일반적으로 IO 기반의 일(IO bound)과 CPU 기반의 일(CPU-bound)을 번갈아 가면서 수행하게 됩니다. 이러한 프로세스의 상태는 일반적으로 아래와 같습니다. IO 기반의 일을 하게 될 때는 CPU는 idle 타임에 들어가게 됩니다. 또한 프로세스 스케줄링 알고리즘에 의해 프로세스는 번갈아가면서 실행되게 됩니다. 이렇게 멀티테스킹 작업을 시도하는데 이때 프로세스에는 아래와 같은 상태의 변동이 있습니다.

+ 실행(Runnable) - CPU에 의해서 명령어가 실행중인 Process
+ 준비(Ready) - CPU의 명령어 실행을 기다리는 Process
+ 대기(Waiting) - I/O operation이 끝나기를 기다리는 Process
+ 종료(Terminated) - Ctrl + Z 등의 signal로 종료된 Process
+ Zombie - Process는 root Process로 부터 뿌리내린 자식 Process 의 형식으로 트리구조를 형성합니다. 이 때 부모가 먼저 종료된 다면 root process로 부터 닿을 수 없는 Process가 생깁니다. 이를 zombie process라고 부릅니다.
![image](https://user-images.githubusercontent.com/44454495/170070081-2b95278e-0a73-4c2c-8d34-0b1523e6a864.png)



### CPU 사용량

Tasks 아래 %Cpu(s)라는 영역이 있습니다. 이 영역은 CPU가 어떻게 사용되고 있는지 그 사용율을 보여주는 영역입니다. 모든 값의 총 합은 100% 이며 이를 퍼센테이지로 나누어서 보여줍니다. 각 요소는 아래와 같습니다.

+ us : 프로세스의 유저 영역에서의 CPU 사용률
+ sy : 프로세스의 커널 영역에서의 CPU 사용률
+ ni : 프로세스의 우선순위(priority) 설정에 사용하는 CPU 사용률
+ id : 사용하고 있지 않는 비율
+ wa : IO가 완료될때까지 기다리고 있는 CPU 비율
+ hi : 하드웨어 인터럽트에 사용되는 CPU 사용률
+ si : 소프트웨어 인터럽트에 사용되는 CPU 사용률
+ st : CPU를 VM에서 사용하여 대기하는 CPU 비율



### 메모리 사용량

%Cpu(s) 영역 아래에 메모리와 관련된 영역이 있습니다. 첫번째 줄은 RAM의 메모리 영역으로 Mem이라 표시되어있는 부분입니다. 그리고 아랫줄은 디스크를 메모리 처럼 이용하는 Swap 메모리 영역입니다. 일반적으로 Mem의 사용량이 거의 가득 찼을때 Swap 메모리 영역을 사용합니다. 이 영역은 디스크이기 때문에 RAM 메모리보다 속도가 많이 느린 단점을 가집니다.

+ total : 총 메모리 양
+ free : 사용가능한 메모리 양
+ used : 사용중인 메모리 양

buff/cache에서 buff는 buffers의 약자입니다. 이 값은 커널 버퍼에서 사용되는 메모리를 뜻합니다. cache는 Disk의 페이지 캐시를 말합니다. 즉, buff/cache는 IO와 관련되어 사용되는 버퍼에 사용되는 메모리를 말합니다. 이 메모리가 있으므로써 IO에 상대적으로 빠른 속도를 가질 수 있습니다. avail Mem은 swap 메모리를 사용하지 않고 사용할 수 있는 메모리의 크기를 말합니다.



### 디테일 영역

지금부터는 top 명령어의 디테일 영역에 대해서 알아보도록 하겠습니다. 디테일 영역에는 각 프로세스에 대한 상세한 내용이 나옵니다. 위 예제에서는 아래의 이미지 부분이 디테일 부분입니다. 각 요소에 대해서 하나씩 보도록하겠습니다.

![image](https://user-images.githubusercontent.com/44454495/170070130-c0dd7a5a-9ddc-4760-928f-43c946d24063.png)

+ PID
1) PID는 프로세스 ID이며 프로세스를 구분하기 위한 겹치지않는 고유한 값입니다.
+ USER
1) 해당 프로세스를 실행한 USER 이름 또는 효과를 받는 USER의 이름입니다.
+ PR & NI
1) PR : 커널에 의해서 스케줄링되는 우선순위입니다.
2) NI : PR에 영향을 주는 nice라는 값입니다.
+ VIRT, RES, SHR, %MEM
1) 해당 필드들은 프로세스의 메모리와 관련있습니다.
2) VIRT : 프로세스가 소비하고 있는 총 메모리입니다. 프로그램이 실행중인 코드, heap, stack과 같은 메모리, IO buffer 메모리를 포함합니다.
3) RES : RAM에서 사용중인 메모리의 크기를 나타냅니다.
4) SHR : 다른 프로세스와의 공유메모리(Shared Memory)를 나타냅니다.
5) %MEM : RAM에서 RES가 차지하는 비율을 나타냅니다.
+ S : 프로세스의 현재 상태를 나타냅니다.
+ TIME+ : 프로세스가 사용한 토탈 CPU 시간
+ COMMAND : 해당 프로세스를 실행한 커맨드를 나타냅니다.



### 유명한 top용 커맨드

#### k - kill process

top를 통해 프로세스를 모니터링하며 프로세스를 종료해야겠다고 생각할 수 있습니다. 이때 top에서는 top화면을 보며 프로세스를 종료할 수 있는 기능을 제공해주고 있습니다. 해당 기능을 사용하기 위한 커맨드는 k입니다.

![image](https://user-images.githubusercontent.com/44454495/170070186-4283e67c-bcaa-4815-a726-3649c9081929.png)

#### Sorting the process list

디테일 영역에 대해서 원하는 값을 기준으로 정렬하는 방법을 제공합니다. 제공하는 커맨드는 아래와 같습니다. 또한 이미지는 메모리 사용량을 기준으로 정렬한 값입니다.

+ ‘M’ to sort by memory usage
+ ‘P’ to sort by CPU usage
+ ‘N’ to sort by process ID
+ ‘T’ to sort by the running time
+ ‘R’ to sort by 오름차순과 내림차순을 토글 변경합니다.

![image](https://user-images.githubusercontent.com/44454495/170070236-2d16e6c6-1ad0-4928-b6ff-e4548a389e1b.png)

#### Showing a list of threads instead of processes

top는 기본적으로 프로세스를 기본으로하여 정보를 보여줍니다. 하지만 H를 누르면 쓰레드(thread)를 기준으로 보여주는 방식으로 변경됩니다. 변경되는 부분은 요약의 Tasks 영역과 디테일 영역입니다.

![image](https://user-images.githubusercontent.com/44454495/170070314-1bc4be9a-0833-4553-a7bf-95f08645ebe4.png)

#### Filtering through processes

프로세스가 너무 많다면 필터링 기능또한 제공해주고 있습니다. 해당 기능을 사용하기 위해서는 o 또는 O를 누르시면 됩니다. 필터는 COMMAND, %CPU 등등 다양한 방법으로 가능합니다.

COMMAND에 JAVA가 포함되는 프로세스만 확인
![image](https://user-images.githubusercontent.com/44454495/170070362-9c1eb6e0-5711-4465-bf32-ccceb4454ae8.png)


%MEM값이 3% 이상인 프로세스만 확인
![image](https://user-images.githubusercontent.com/44454495/170070434-8cf4a177-38ae-443b-ba54-b4881f6b834c.png)


---

안녕하세요 이것은 과제를 제출하기 위한 read.md 파일입니다.

확인차 vim 에서 수정하여 처음으로 commit and push 하겠습니다.

exit.


