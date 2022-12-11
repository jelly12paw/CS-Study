# 💻 CS Study 3.4 CPU 스케줄링 알고리즘

> `면접을 위한 CS 전공지식 노트` **3.4 CPU 스케줄링 알고리즘**
>
> `3.4.1 비선점형 방식`
>
> `3.4.2 선점형 방식`
>
<br>
<hr>
<br>

## **CPU 스케줄링 알고리즘**
<br>

> 한 번에 **여러 프로세스를 실행**하기 위해서 사용
> 
> 메모리에 있는 프로세스들 중 **어떤 프로세스를 실행할지 선택**하고 **CPU를 할당해주는 역할**
> 

> `CPU 스케쥴링의 목표`
> 
> CPU 이용률은 높게
>
> 주어진 시간에 많은 일을 처리
>
> 준비 큐에 있는 프로세스는 적게
>
> 응답 시간은 짧게 
>

<br>

1. 실행(running) 상태에서 대기(waiting) 상태로 전환(switching)될 때 ( ex : I/O 발생 )
2. 실행(running) 상태에서 준비(ready) 상태로 전환(switching)될 때 ( ex : intterupt 발생 )
3. 대기(waiting) 상태에서 준비(ready) 상태로 전환(switching)될 때 ( ex : I/O 완료 시 )
4. 종료(Terminated)될 때 


    **1번과 4번 상황에서만** 스케줄링이 발생하는 것을 `비선점형(non-preemptive) 스케줄링`

    **이 외의 모든 스케줄링**은 `선점형(preemptive) 스케줄링`


<br>

## 비선점형 방식

<br>

    -프로세스가 CPU를 점유하고 있다면 이를 뺐을 수 없는 방식
    - 필요한 문맥 교환만 일어나므로 오버헤드(overhead)가 상대적으로 적지만 프로세스의 배치에 따라 효율성 차이가 많이 난

<br>

### FCFS (First Come First Served)

- 가장 먼저 요청한 프로세스에 CPU를 할당해주는 방식이다.
- 작성이 간단하고 이해하기 쉽다.
- 평균 대기 시간(Average Waiting Time)이 길어질 수 있다.
- 응답 시간(Response Time)이 길어질 수 있다.
- 반환시간(Turnaround Time) 면에서는 좋을 수 있다.
- Convoy Effect(호위 효과)가 발생할 수 있다. 

![ex](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fcj1eAz%2FbtrwVseqDoP%2FkywQBfZVaeLRcEJ7nFNXk0%2Fimg.png)

<br>

### SJF(Shortest-Job-First)

- 다음 CPU burst time의 길이를 고려해서 스케줄링을 결정하는 알고리즘이다.
- 비선점형과 선점형이 따로 존재한다. 
- 비선점형에서는 실행되고 있는 프로세스는 끝까지 실행한다.
- 선점형에서는 현재 실행되고 있는 프로세스의 남은 시간보다 도착한 다음 프로세스가 더 빨리 끝날 수 있는 프로세스라면 다음 프로세스를 실행하도록 바꾸게 된다. SRTF(Shortest Remaining Time First)라고도 부른다. 
- SJF 스케줄링은 평균 대기 시간을 줄일 수 있다.
- 하지만 다음 프로세스의 CPU burst time을 예측하는 것이 어렵다는 문제가 존재한다.

비선점형 SJF
![ex](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FLvUVD%2FbtrwVsSWLbJ%2FoIOaF3SBtE9Gd87sWqjGWK%2Fimg.png)

선점형 SJF
![ex](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FL2iRd%2FbtrwXz49BtP%2FucHEyokTcjfydBSZdogOhK%2Fimg.png)

<br>

### 우선순위(Priority)

- 각각의 프로세스에 우선순위 넘버가 있다.
- 가장 높은 우선순위의 프로세스에 CPU를 할당한다.
- SJF도 Priority 스케줄링이라고 할 수 있다. 

![ex](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FA4IZf%2FbtrwVrs2Cux%2Fs1k5EWSxBkYRMgULlr4F70%2Fimg.png)

<br>

<hr>
<br>

## 선점형 방식

<br>

    - 프로세스가 CPU를 할당받아 실행 중이더라도 운영체제가 이를 강제로 뺐을 수 있는 방식
    - CPU 처리 시간이 매우 긴 프로세스의 CPU 사용 독점을 막을 수 있어 효율적인 운영 가능
    - 잦은 문맥 교환으로 오버헤드(Overhead)가 커질 수 있다. 

<br>

### 라운드 로빈(Round Robin)

- 각각의 프로세스에 동일한 CPU 할당 시간을 부여해서 해당 시간 동안만 CPU를 이용하게 한다.
- 할당 시간 내에 처리를 완료하지 못하면 다음 프로세스로 넘어가므로 선점형 방식이다.
- n개의 프로세스가 있을 때 할당 시간을 q로 설정하면, 어떤 프로세스도 (n-1)q 시간 이상을 기다리지 않아도 된다.
- 응답 시간을 빠르게 할 수 있다는 장점이 있다.
- q가 커진다면 FCFS처럼 작동한다. 
- q가 매우 작아지면 process sharing이라고 부른다. 이것은 n개의 프로세스가 프로세서 속도의 1/n 씩으로 작동함을 의미한다. 

![ex](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FoVKvq%2Fbtrw2NV85g2%2FymVM3yVGOHXr9GqSkkZPD0%2Fimg.png)

<br>

### 다단계 큐(Multilevel Queue)

![ex](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FXMWpH%2Fbtrw5DyJTF7%2FO0qPFx4uqpTJkWE0fD8kv0%2Fimg.png)

- 준비 큐가 여러 개의 큐들로 나뉜다.
- 각 큐는 각자의 스케줄링 알고리즘을 가지고 있다. 
- 각 큐 사이에서 프로세스들이 이동할 수 없다. 
- 일반적으로 Foreground 프로세스들은 Round Robin 방식을 사용하고, Background 프로세스는 FCFS를 사용한다.
- 보통 CPU 시간의 80%는 Foreground의 RR, 20%는 Background의 FCFS에 할당된다.

<br>