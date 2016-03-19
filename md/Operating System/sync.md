# 进程同步

- tags: os, sync

------

1. OS同步原语
  - mutex
    - 最大值为1的semaphore
  - semaphore
    - 进程间的互斥锁, 保证同一时刻有限个进程访问某个资源
    - 基本操作inc/dec
  - conditional variable
    - 简介
      - 进程等待某个条件发生, 当某个条件可能为真的时候进程被唤醒
      - 基本操作是wait/notify/notifyAll(java中Object的方法)
      - conditional variable可以使用(n+1)个semaphore实现, n为进程个数. 1个semaphore用作全局锁, 要改变condition variable中variable的值必须获取该semaphore, 剩余semaphore用于锁住每个等待该条件的进程. 当某个进程改变了条件后, 需要检查是否满足了条件, 如果满足条件, 则唤醒一个或全部进程.
      - 阻塞式conditional variable需要多一些semaphore, 用于锁住调用notify的进程.
      - 举例: 假设线程t0,t1,t2的操作是sum++,而线程t3则是在sum到达100的时候,打印出一条信息,并对sum清零.
      - 这种情况下,如果只用mutex, 则t3需要一个循环,每个循环里先取得lock_s,然后检查sum的状态,如果sum>=100,则打印并清零,然后unlock.如果sum<100,则unlock,并sleep()本线程合适的一段时间. 这样效率低
    - 分类
      - 阻塞notify和非阻塞notify
      - 对于阻塞式, wait进程被唤醒后条件一般是成立的
      - 对于非阻塞式, wait进程被唤醒后一定要检查条件是否仍然成立, 因为很可能从notify到wait被唤醒这个阶段有其他进程改变了条件.
  - monitor(管程,监视器)
    - semaphore和conditional variable的合体, 使在critical section中有有限个进程执行, 而且这些进程如果在critical section中等待monitor中的某个条件, 则自动解锁semaphore, 并且当条件发生时重新获得semaphore(进入critical section). 这样防止了进程在critical section中等待资源导致死锁.
