
# Chosun_oss_20194301_report: 
## 조선대학교 오픈소스소프트웨어 03분반 제 2차 과제 작성 - 학과 : 컴퓨터공학과 / 학번 : 20194301 / 이름 : 강정태 

---

## Linux top 명령어

### top 명령어란?

  ***실시간으로 CPU 사용률을 체크해주는 도구이다. 윈도우의 작업관리자와 비슷하며, 리눅스를 사용하는 서버의 현재 성능이나 동작하는 프로세서의 상황을 볼 때 사용한다.***

### top 사용법


```
root#> top 
```

### 요약 영역

  요약 영역은 top에서 상단에 위치하고 있습니다. 이 요약영역은 전체 프로세스가 OS에 대해서 리소스를 어느정도 차지하고 있는지를 알려줍니다. 요약 영역에 나타나는 대표적인 값은 **시간, 유저, 로드 에버리지(Load Average), 테스크(Tasks), CPU, 메모리(memory)로 아래의 이미지를 보시면 각 영역에 대해 나태내는 값이 어디에 위치하는지 알 수 있습니다.**

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

> COMMAND에 JAVA가 포함되는 프로세스만 확인
> ![image](https://user-images.githubusercontent.com/44454495/170070362-9c1eb6e0-5711-4465-bf32-ccceb4454ae8.png)


> %MEM값이 3% 이상인 프로세스만 확인
> ![image](https://user-images.githubusercontent.com/44454495/170070434-8cf4a177-38ae-443b-ba54-b4881f6b834c.png)


---

## Linux ps 명령어

### ps 명령어란?

**ps는 Process Status의 줄인말로 현재 실행중인 프로세스 목록과 상태를 보여줍니다.**

여러분들이 컴퓨터를 사용할때 가장 많이 사용하는 명령이 있습니다. 그 중 한가지 경우가 프로세스에 대한 정보를 알고 싶을 경우인데요. 예를 들어 어떤 프로세스가 수행중인데, 이 프로세스가 CPU를 굉장히 많이 소모시킨다고 합니다. kill 명령으로 그 프로세스를 종료시키고 싶지만 pid를 알아야하겠죠. 이때 pid등의 정보를 볼 수 있는 명령이 있습니다. 그 process의 상태를 알고 싶을때 매우 많이 사용하는 명령이 바로 ps입니다.

ps는 프로세스에 대한 많은 정보를 담고 있고 매우 많이 사용되는 명령으로 옵션이 매우 다양합니다. ps는 옵션에는 세가지 종류가 있습니다.
1) Unix Option : 앞에 '-' (dash)가 붙는 옵션 표기방법입니다. 
2) BSD Option : '-' 를 붙이지 않습니다.
3) GNU Option : 명령어 앞에 '--' (double dash)를 붙입니다.
물론 Unix, BSD, GNU 옵션들을 모두 우리가 알 수도 없고, 외울 수도 없지만 그래도 유용한 옵션정도는 알고 있어야겠죠? 


### ps 사용법

```
ps
```

### 기본 ps 명령어 구성

ps 명령어를 치면 아래와 같이 나오게 됩니다.  별로 몇개 나오지 않는 다는 것을 알 수 있는데, 이것은 ps가 기본적으로 같은 EUID(Effective User ID)의 프로세스이며 같은 터미널의 프로세스만을 골라서 보여주기 때문입니다. 
보여주는 정보는 프로세스 ID(PID), 터미널(TTY), CPU 점유 시간(TIME), 그리고 프로세스가 수행된 명령어(CMD)입니다. 여기서 a.out은 제가 임의로 무한 루프를 돌린 프로세스를 실행시켜서 그렇고 시간은 TIME이 00:04:31인것을 볼 수 있네요.

![image](https://user-images.githubusercontent.com/44454495/170078400-4ff7a571-3d79-440a-94ab-9fadb1b72d60.png)

+ ps -e, -A : 모든 프로세스를 보여줍니다. 
+ ps -a : 세션 리더와 터미널과 연관된 프로세스들을 제외한 모든 프로세스를 보여줍니다.
+ ps -d : 세션 리더를 제외한 모든 프로세스를 보여줍니다.
+ ps -f : full format으로 세션의 정보를 표시합니다. 
+ ps -ef : -e와 -f의 옵션 조합인데, 모든 프로세스를 full format으로 보여줍니다.

아래는 그 결과를 보여줍니다. UID, PID, PPID, C, STIME, TTY, TIME, CMD의 정보를 볼 수 있네요. TTY(연결 터미널)가 없으면 대부분 데몬 혹은 커널 프로세스입니다. 

> ps -ef 결과 1
> ![image](https://user-images.githubusercontent.com/44454495/170078448-40546aa1-8622-4518-ab48-c1232e8259ef.png)

> ps -ef 결과 2
> ![image](https://user-images.githubusercontent.com/44454495/170078462-71c51f54-e54d-44b1-a59d-47f66a3c2e30.png)


+ ps -u userlist : EUID 혹은 유저 이름으로 프로세스를 고릅니다. 이때 여러 uid를 줄수 있는데 ','(comma)로 구분하여 명시해줍니다. euid는 프로세스가 수행할때 갖는 유저 권한을 말합니다.
+ ps -U userlist : -u 옵션과는 동일하나 RUID가 갖는 프로세스만을 찾아냅니다. ruid는 real user id라는 것으로 실제 프로그램을 실행한 uid를 의미합니다. 이때도 쉼표로 여러 uid를 지정할 수 있습니다.
+ ps -p pidlist : 프로세스 id가 일치하는 프로세스를 출력합니다. 여러 pid들을 뽑아내고 싶다면 마찬가지로 ','(comma)로 pid를 구분하여 명시해줄 수 있습니다. 이 명령은 ps --pid pidlist와 같습니다.
+ ps --ppid pidlist : 부모 프로세스 id와 일치하는 프로세스를 출력합니다. 역시 여러 ppid를 ','(comma)로 구분가능합니다.
+ ps -t ttylist : tty와 일치하는 프로세스들을 출력해줍니다. 이 명령은 t 혹은 --tty 옵션과 같습니다. 
+ ps -o format : 사용자가 지정한 format대로 출력합니다. format에 대해서는 설명이 길지만 간략하게 원하는 column만 보여준다고 기억하시면 됩니다. 예를 들어 사용자가 임의로 pid, ppid, cmd, uid 등을 표시할 수 있습니다.

#### 다음의 표는 format에 대해 정리한 표입니다.

|CODE|NORMAL|HEADER|
|---|---|---|
|%C|pcpu|%CPU|
|%G|group|GROUP|
|%P|ppid|PPID|
|%U|user|USER|
|%a|args|COMMAND|
|%c|comm|COMMAND|
|%g|rgroup|RGROUP|
|%n|nice|NI|
|%p|pid|PID|
|%r|pgid|PGID|
|%t|etime|ELAPSED|
|%u|ruser|RUSER|
|%x|time|TIME|
|%y|tty|TTY|
|%z|vsz|VSZ|

#### 아래의 예는 uid가 0, 1000인 프로세스를 출력하는데, uid, ruid, euid, guid, pid, ppid, cmd를 출력해줍니다.

> ps -u userlist -o format
> 
> ![image](https://user-images.githubusercontent.com/44454495/170079565-c73250a7-6a28-4b06-baa5-09820f02e350.png)

#### ps aux : BSD 문법으로 실행중인 모든 프로세스를 나타냅니다. ps -aux와는 다른 옵션입니다. 

> ps aux
> 
> ![image](https://user-images.githubusercontent.com/44454495/170079625-94d43f8b-e85e-4361-a792-9da3f22796ef.png)

#### 위의 보이는 것 중에 프로세스의 상태를 나타내는 STAT 혹은 S는 아래의 코드로 구성됩니다. 다른건 필요없고 Z로 표시된 프로세스는 좀비 프로세스로 자원을 점유하므로 시스템 관리가 필요합니다. 반드시 없애야합니다.

|Code	|Desc|
|---|---|
|D	|Uninterruptible sleep|
|Idle	|Idle kernel thread|
|R	|Running or runnable|
|S	|Interruptible sleep|
|T	|stopped by job control signal|
|t	|stopped by debugger during tracing|
|W	|paging|
|X	|dead|
|Z	|defuct (zombie) process|

#### BSD format에서는 추가 문자가 쓰일 수 있습니다.

|Character|	Desc|
|---|---|
|<	|high-priority(not nice to other users)|
|N	|low-priority(nice to other users)|
|L	|has pages locked into memory|
|s	|is a session leader|
|l	|is multi-threaded|
|+	|is in the foreground process group|

#### "ps | grep" 원하는 프로세스만 추출

대개 ps명령은 많은 결과를 출력하는데 이때 grep을 이용하여 원하는 프로세스를 찾을 수 있습니다. 예를 들면 sshd와 관련된 프로세스를 찾기를 원하면 이렇게 사용할 수 있습니다.

> ps -ef | grep sshd
> 
> ![image](https://user-images.githubusercontent.com/44454495/170079891-40bc93d5-56ee-4478-af1e-5654e5f14c10.png)


#### ps -ejH
프로세스를 트리 형태로 조금 보기 좋게 표시하고 싶다면 -ejH옵션을 사용하면 됩니다. 자식 트리면 CMD가 한칸 띄어져서 출력이 됩니다.

> ps -ejH 1
> 
> ![image](https://user-images.githubusercontent.com/44454495/170079907-be967053-139e-4c9e-bed7-4d0b1e1311ce.png)
  
> ps -ejH 2
> 
> ![image](https://user-images.githubusercontent.com/44454495/170080078-b7458d0c-b865-4eaa-826a-26ecbd0e0068.png)

사실 트리모양으로 보기 좋게 출력하고 싶다면 아래의 pstree 명령이 더 보기 좋습니다.

#### pstree
여러분이 트리 형식으로 실행중인 프로세스를 보고 싶으시면 pstree 명령을 사용하시면 됩니다. 이 트리는 기본적으로 init 혹은 systemd 프로세스가 루트인데, 만약 pid를 명시한다면 그 pid가 루트가 됩니다. 

> pstree
> 
> ![image](https://user-images.githubusercontent.com/44454495/170080171-04c1226f-e415-417a-bc79-310203b808c3.png)

---

## Linux jobs 명령어

### jobs 명령어란?

**리눅스 명령어 jobs는 작업이 중지된 상태, 백그라운드로 진행 중인 작업 상태, 변경 되었지만 보고되지 않은 상태 등을 표시하는 명령어다.**

+ 백그라운드로 실행되는 작업목록(작업번호, 상태, 명령어)을 보여주는 리눅스 명령어
+ 여기서 작업번호는 PID와는 달리, 별도로 부여되는 백그라운드 작업목록 상의 번호이다.
+ 작업목록은 현재 쉘 세션에 딸린 것이며, 다른 세션과는 독립적이다.
+ 현재 쉘 프로세스(bash)의 자식 백그라운드 프로세스들을 보여준다고 할 수 있다.
+ 리눅스 kill 명령어 뒤에 %작업번호를 입력하여 종료시킬 수 있다.

### 사용법

```
jobs [option]
```

### jobs로 알 수 있는 세션의 상태 값

| 상태	| 설명|
| Running	| 작업이 일시 중단되지 않았고 종료하지 않고 계속 진행 중임|
| Done	| 작업이 완료되어 0을 반환하고 종료 했음을 의미|
| Done(code)	| 작업이 정삭적으로 완료되었으며, 0이 아닌 코드를 반환 했음을 의미|
| Stopped	| 작업이 일시 중단|
 |Stopped(SIGTSTP)	| SIGTSTP 신호가 작업을 일시 중단|
| Stopped(SIGSTOP)	| SIGSTOP 신호가 작업을 일시 중단|
| Stopped(SIGTTIN)	| SIGTTIN 신호가 작업을 일시 중단|
| Stopped(SIGTTOU)	| SIGTTOU 신호가 작업을 일시 중단|


### 옵션

 |옵션	| 설명|
| -l	| 프로세스 그룹 ID를 state 필드 앞에 출력|
| -n	| 프로세스 그룹 중에 대표 프로세스 ID를 출력|
| -p	| 각 프로세스 ID에 대해 한 행씩 출력|
| command	| 지정한 명령어를 실행|


### 사용

```
testuser@ubuntu1:~$ sleep 300 &
[1] 30335
testuser@ubuntu1:~$ sleep 400 &
[2] 30336
testuser@ubuntu1:~$ sleep 500 &
[3] 30337
testuser@ubuntu1:~$ jobs
[1]   Running                 sleep 300 &
[2]-  Running                 sleep 400 &
[3]+  Running                 sleep 500 &
testuser@ubuntu1:~$ kill %2
testuser@ubuntu1:~$ 
[2]-  Terminated              sleep 400
testuser@ubuntu1:~$ jobs
[1]-  Running                 sleep 300 &
[3]+  Running                 sleep 500 &
testuser@ubuntu1:~$ kill %1 %3
testuser@ubuntu1:~$ 
[1]-  Terminated              sleep 300
[3]+  Terminated              sleep 500
testuser@ubuntu1:~$ jobs
testuser@ubuntu1:~$
```

---

## Linux kill 명령어

### kill 명령어란?
**프로세스에 특정한 signal을 보내는 명령어
일반적으로 종료되지 않는 프로세스를 종료 시킬 때 많이 사용한다. 리눅스에서 작업을 할 때 응용프로그램이나 프로세스가 멈추는 것을 볼 수 있습니다. 이 때의 유일한 해결책은 그 프로세스를 종료하는 것입니다. 리눅스는 이러한 시나리오에서 사용할 수 있는 kill 유틸리티를 제공합니다.**


### 프로세스 죽이는 방법 및 사용 예

***kill 명령어는 대개 프로세스를 죽일 때 사용합니다.*** 하지만 내부적으로는 프로세스에 시그널을 보내 원하는 작업을 하게 하는 명령어입니다. 이 툴을 사용하려면 다음 구문을 사용합니다.

```
kill [옵션 or 시그널(번호 또는 이름)] PID
$ kill -9 1234
$ kill -SIGKILL 1234
```

예를들어 node.js로 실행 중인 서버를 죽이고 싶다면 ps 명령어를 통해 node.js의 pid를 얻고 kill 명령어의 파라미터로 넘겨 실행시키면 종료시킬 수 있습니다.

> ![image](https://user-images.githubusercontent.com/44454495/170103949-5776ddb4-50d6-4751-b1b7-bd75ab6cd3fd.png)


### 사용자 지정 시그널 전송 방법
kill 명령어의 default 시그널은 TERM(15) 입니다. 하지만 -s 명령으로 다른 시그널을 보낼 수 있습니다.

```$ kill -s [signal] [pid]```

예를 들어 프로세스가 TERM(15) 시그널에 응답하지 않으면 다음의 명령어 처럼 KILL(9)를 사용해 강제로 죽일 수 있습니다.

```$ kill -s KILL [pid]```

### 사용 가능한 시그널의 목록
-l (List의 엘) 명령어를 통해 지원하는 시그널의 목록을 확인할 수 있습니다.

### 옵션
-l : signal 의 종류를 출력한다.

``` $ kill -l ```

> ![image](https://user-images.githubusercontent.com/44454495/170104083-a5a20bf5-5b1d-4bf1-b2a1-11e42b5d2cef.png)


### Signal 의 종료
> 1) SIGHUP : 연결 끊기. 프로세스의 설정파일을 다시 읽음
> 2) SIGINT : 인터럽트
> 3) SIGQUIT : 종료
> 4) SIGILL : 잘못된 명령
> 5) SIGTRAP : 트렙 추적
> 6) SIGABRT
> 7) SIGBUS : 버스 에러
> 8) SIGFPE : 고정 소수점 예외
> 9) SIGKILL : 죽이기
> 10) SIGUSR1
> 11) SIGSEGV : 세그멘테이션 위반
> 12) SIGUSR2     
> 13) SIGPIPE : 읽을 것이 없는 파이프에 대한 시그널
> 14) SIGALRM : 경고 클럭
> 15) SIGTERM : 소프트웨어 종료 시그널
> 16) SIGSTKFLT : 프로세서 스택 실패
> 17) SIGCHLD : 자식 프로세서의 상태변화
> 18) SIGCONT : STOP 시그널 이후 계속 진행할 때 사용
> 19) SIGSTOP : 정지
> 20) SIGTSTP : 키보드에 의해 발생하는 시그널
> 21) SIGTTIN      
> 22) SIGTTOU     
> 23) SIGURG      
> 24) SIGXCPU     
> 25) SIGXFSZ
> 26) SIGVTALRM  
> 27) SIGPROF     
> 28) SIGWINCH   
> 29) SIGIO         
> 30) SIGPWR
> 31) SIGSYS

---

## VIM EDITOR MACRO 명령어

### VIM EDITOR MACRO는 무엇인가?

**Vim 에서 반복되는 같은 동작(vim 명령어)들을 기록하고 자동으로 실행하여 인간의 수고로움을 덜어주는 기능을 말한다.**


### 매크로가 필요한 순간
가령 다음 스크린샷의 좌측과 같은 코드가 있다고 가정해보자. 이를 오른쪽 코드와 같이 바꾸고자 한다. javascript 에서 key 를 그대로 value 에 넣은 뒤 이를 대문자로 바꾸려고 한다.

> ![img1 daumcdn](https://user-images.githubusercontent.com/44454495/170123475-f3d2cc6b-5dd6-4962-845d-3c487e82ca28.png)
> Vim Macro 기능을 활용해 좌측 코드를 우측 코드와 같이 바꿔보고자 한다.

일단, jazz 가 포함된 라인(2번줄)에서 vim 을 활용하여 이 과정을 진행해보자.
다음과 같이 기존 코드를 변경할 것이다.


```c
// fromjazz: ""// tojazz: "JAZZ"
```


이를 수행하기 위한 시퀀스는 다음과 같다.

> 1) jazz 의 j 로 커서를 이동한다. (^)
> 2) 단어를 복사한다. (yiw)
> 3) 첫 번째 따옴표로 이동한다. (f")
> 4) 복사한 단어를 붙여넣는다. (p)
> 5) 붙여넣어진 단어를 대문자로 변경한다. (gUaw)
> *참고: `gU{모션}` 은 모션 범위를 대문자로 변경한다. gu 는 소문자로.
> 6) 아래 줄로 이동한다. (j)

> ![img1](https://user-images.githubusercontent.com/44454495/170123787-e7854dfd-33ad-45dd-aac2-6b594c27449d.gif)
> key 에 해당하는 문자열을 value string 에 그대로 넣은 뒤 대문자로 변경하는 예제

위에서 설명한 1~6 과정이 그대로 반복된다면 opera 가 포함된 라인에도 동일한 동작이 수행되게 할 수 있다.
차라리 노가다를 택할 수도 있고, 굳이 매크로를 쓰지 않아도 적절히 몇번 반복하면 끝난다고 생각할 수도 있겠지만, 동일한 작업을 해야하는 라인이 수십줄이 넘어간다고 상상해보자. 
매크로를 활용하지 못한다면, 각 라인마다 각각 12회의 키를 입력해야 한다.
 
일련의 동작들을 기록하고 재사용할 수 있다면 어떨까? 그게 바로 Vim Macro 이다.
 
### Vim Macro 사용방법

>  `q{레지스터}` 로 매크로 기록 시작
>  `q` 로 매크로 기록 종료
>  `@{레지스터}` 로 저장된 매크로 실행
>  `@@` 로 직전에 실행한 매크로 재실행
>  `{반복횟수}@{레지스터}` 또는 `{반복횟수}@@` 로 저장된 매크로를 '반복횟수' 만큼 재실행

|기능|	일반모드|	예제|
|---|---|---|
|녹화|	q+(매크로KEY)|	qa|
|녹화종료|	q|	q|
|재생|	@+(매크로KEY)|	@a|
|마지막매크로실행|	@@|	@@|
|횟수실행|	(횟수)@(매크로KEY)|	10@a|

매크로를 정해진 횟수만큼 반복할 때 사용하는 방법인데요. a에 매크로 작업한 것을 10회 반복해서 연속 실행할 때는 10@a 라고 일반모드에서 입력하면 됩니다. 정말 편하죠!

여기서 하나 더 Vim에서 숫자 증가 감소를 일반모드에서 할 수 있는데요. 

|기능|	일반모드|	예제|
|---|---|---|
|숫자증가|	CTRL + a|	증가시키고 싶은 숫자에 커서 두고 ^a|
|숫자증가|	CTRL + x|	감소시키고 싶은 숫자에 커서 두고 ^x|

**증가하고자 하는 숫자위로 가서 커서를 두고 CTRL+a를 누르면 숫자가 증가하고 CTRL+x를 누르면 숫자가 감소하게 됩니다.**

#### q - Vim Macro 기록하기 & 기록 종료하기

Normal Mode 에서 q 를 입력하면, 하단 상태표시줄에 q 가 표시된다. 이는 앞으로 기록할 레지스터를 지정해주기를 대기하고 있는 상태이다. 레지스터(a-z, 0-9 중 하나)를 정하여 입력하면 상태표시줄에 'Recording @a'(레지스터로 'a'를 입력했다고 가정) 와 같이 실제 명령어를 대기하고 있는 상태가 된다. 
 
일련의 동작들을 입력한 뒤 다시 q 를 입력하면 매크로 기록이 종료된다.
 
다음 스크린샷에서 위에서 1~6 과정에서 입력한 과정들을 매크로로 기록하는 과정을 살펴보자.

> ![img2](https://user-images.githubusercontent.com/44454495/170123928-9a64064a-af1c-42a1-97e0-158918a2f3ee.gif)
> qa 명령어로 a 레지스터에 일련의 동작들을 기록한 뒤 q 명령어로 기록을 중지했다. (기록상황은 하단 상태표시줄에 나타난다.)

이 예제에서는 매크로를 기록할 레지스터로 a 를 사용했다. 

#### @ - Vim Macro 실행하기
`@{레지스터}` 로 특정 레지스터에 저장된 매크로를 실행시킬 수도 있고, `@@` 로 직전에 실행한 매크로를 재실행할 수도 있다.
 
"opera" 라인(3번줄)은 `@a` 로 재실행해보자. 이전 스크린샷에서 그대로 이어진다.

> ![img3](https://user-images.githubusercontent.com/44454495/170124065-14c881f8-903a-46ab-b1ec-a82d19cc25da.gif)
> @{매크로가 저장된 레지스터}를 통해 저장된 매크로를 실행시킨다.
 
rock 라인은(4번줄)은 `@@` 로 직전에 실행한 매크로를 반복해보자. 이전 스크린샷에서 그대로 이어진다.

> ![img4](https://user-images.githubusercontent.com/44454495/170124247-c28f7520-c75c-4bf8-b8eb-f2ad6fef78bb.gif)
> @@ 는 직전에 실행된 매크로를 재실행한다.


이렇게 매크로를 알아보았다. 사실 이렇게 매크로를 활용하는 것이 거의 전부이다. 매크로와 관련하여 몇가지 사항을 아래에서 더 알아보도록 하자. 


#### 레지스터에 저장된 매크로 확인해보기
vim 에서는 레지스터에 저장된 내용을 확인하기 위한 command mode 명령어를 제공한다. `:register` 가 그것이다. 단순히 이 명령어를 입력하면 모든 레지스터의 저장된 값들을 리스팅해준다. ':register' 명령어는 인자를 받기도 하는데, `:register a` 와 같이 명령어의 인자로 레지스터명을 전달하면 해당 레지스터에 저장된 값을 표현해준다. (오리지널 vim 에서도 UI 만 다를 뿐 VSCode Vim 과 동일하게 동작한다.)


> ![img5](https://user-images.githubusercontent.com/44454495/170124382-bdd1be12-02dc-48dc-836d-9a785ad4353f.gif)
> VSCode Vim 에서 `:register` 커맨드 모드 명령어로 레지스터의 내용을 확인하는 모습, a 레지스터에 우리가 저장한 동작이 보인다.


![img6](https://user-images.githubusercontent.com/44454495/170124456-168aad04-a7ca-41a7-a97a-a75cc67b72ab.gif)
`:register a` 명령어를 입력하여 a 레지스터에 저장된 내용을 확인하는 모습, 우리가 위 과정을 통해 저장한 일련의 동작들이 확인된다.


레지스터에 저장된 내용이기 때문에, 당연하게도 `"ap` 명령어로 a 레지스터의 내용을 붙여넣을 수 있다.


> ![img7](https://user-images.githubusercontent.com/44454495/170124560-2d663376-5af6-47c0-861a-b22494347d8f.gif)
> 레지스터를 지정하여("a) 붙여넣기(p)를 수행한 모습이다. 우리가 매크로로 기록했던 내용이 붙여넣어졌다.


매크로는 레지스터에 저장된다는 점을 활용하여 복잡한 매크로의 경우 .vimrc 등의 파일에 등록하여 관리하기도 한다.

```
let @(매크로KEY) = (CTRL+r CTRL+r (매크로KEY))
```

.vimrc에 이렇게 만들어두면 마지막 저장해둔 매크로 동작들을 저장할 수 있습니다. ***CTRL+r CTRL+r (매크로KEY) 누르는 것은 반드시 입력모드 에서 동작해야 저장된 매크로를 불러 올 수 있습니다.***

---

> ## 학과 : 컴퓨터공학과 / 학번 : 20194301 / 이름 : 강정태 
> # Chosun_oss_20194301_report: 조선대학교 오픈소스소프트웨어 03분반 제 2차 과제 작성

이 문서는 오픈소스소프트웨어 과제를 제출하기 위한 README.md 파일입니다. 감사합니다.
