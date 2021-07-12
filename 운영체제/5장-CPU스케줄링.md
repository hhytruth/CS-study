https://core.ewha.ac.kr/publicview/C0101020140328151311578473?vmode=f   
https://core.ewha.ac.kr/publicview/C0101020140401134252676046?vmode=f   

### 성능 척도
- CPU utilization: keep the CPU as busy as possible
- Throughput: N of processes that complete their execution per time unit
- Turnaround time: amount of time to execute a particular process
- Waiting time: amount of time a process has been waiting in the ready queue
- Response time: amount of time it takes from when a request was submitted until the first response is produced, not output

### 스케줄링 알고리즘
- FCFS(First-Come-First-Served)
  + convoy effect: 소요시간이 긴 프로세스가 먼저 도달하여 시간을 잡아먹고 있는 부정적인 현상
- SJF(Shortest-Job-First): CPU burst time이 가장 짧은 프로세스를 제일 먼저 스케쥴
  + Nonpreemptive: 일단 CPU를 잡으면 이번 CPU burst가 완료될 때까지 CPU를 선점당하지 않음
  + Preemptive: SRTF(Shortest-Remaining-Time-First)라고도 부름
  + 주어진 프로세스들에 대해 minimum average waiting time을 보장(preemptive 버전)
  + priority scheduling
  + 문제점: Starvation(기아 현상) - low priority process may never execute
  + 해결방안: Aging as time progresses increase the priority of the process

### 다음 CPU Burst Time의 예측   
![image](https://user-images.githubusercontent.com/28378553/125228024-f1296000-e30e-11eb-8e4f-2fe7dae0abd1.png)   
![image](https://user-images.githubusercontent.com/28378553/125228103-2170fe80-e30f-11eb-9ef8-0fa0491234ea.png)   
- α와 (1-α)가 둘다 1 이하이므로 후속 term이 선행 term보다 더 적은 가중치 값을 가짐

### Round Robin(RR)
- 각 프로세스는 동일한 크기의 할당 시간(time quantum)을 가짐
- 성능
  + q large->FCFS
  + q small-> context switch 오버헤드가 커진다
- 일반적으로 SJF보다 average turnaround time이 길지만 response time이 더 짧다

### Multilevel Queue
- Ready queue를 여러 개로 분할
- 각 큐는 독립적인 스케줄링 알고리즘을 가짐(foreground-RR, background-FCFS)
- 큐에 대한 스케줄링이 필요
  + Fixed priority scheduling
    - serve all from foreground then from background
    - Possibility of starvation
  + Time slice: 각 큐에 CPU time을 적절한 비율로 할당   
![image](https://user-images.githubusercontent.com/28378553/125228698-38fcb700-e310-11eb-8dae-c982e21a8c59.png)

### Multilevel Feedback Queue   
![image](https://user-images.githubusercontent.com/28378553/125228966-bc1e0d00-e310-11eb-92ac-b4bf5ffa02f5.png)
- 프로세스가 다른 큐로 이동 가능

### Multiple-Processor Scheduling
- CPU가 여러 개인 경우 스케줄링은 더욱 복잡해짐
- Homogeneous processor인 경우: 큐에 한 줄로 세워서 각 프로세서가 알아서 꺼내가게 할 수 있다
- Load Sharing: 일부 프로세서에 job이 몰리지 않도록 부하를 적절히 공유하는 메커니즘 필요
- Symmetric Multiprocessing(SMP): 각 프로세서가 각자 알아서 스케줄링 결정
- Asymmetric multiprocessing: 하나의 프로세서가 시스템 데이터의 접근과 공유를 책임지고 나머지 프로세서는 거기에 따름

### Realtime Scheduling

### Thread Scheduling
- Local Scheduling: User level thread의 경우 사용자 수준의 스레드 라이브러리에 의해 어떤 스레드를 스케줄할지 결정
- Global Scheduling: Kernel level thread의 경우 일반 프로세스와 마찬가지로 커널의 단기 스케줄러가 어떤 스레드를 스케줄할지 결정

### Algorithm Evaluation
- 구현&성능 측정
- 시뮬레이션
- Queueing models: 확률 분포로 주어지는 arrival rate와 service rate 등을 통해 각종 performance index값을 계산
