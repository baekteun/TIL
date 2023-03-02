# Process
- 프로세스란 단순히 실행중인 프로그램이라고 할 수 있습니다.
- 작성한 프로그램이 운영체제에 의해 메모리 공간을 할당받아 실행 중인 것을 말합니다.
- 이러한 프로세스는 프로그램에 사용되는 데이터와 메모리 등의 자원 그리고 스레드로 이루어집니다.

# Thread
- 스레드는 프로세스 내에서 실행되는 흐름의 단위입니다.
- 스레드는 프로세스 내에서 실제로 작업을 수행하는 주체를 의미합니다.

# Task
- 실행 또는 작업의 단위를 의미합니다.

# 동시성 프로그래밍
코드를 작성할 때 별도의 처리를 하지 않으면 기본적으로 Main Thread에서 작업이 실행됩니다.

이 메인 스레드에 몰린 작업들을 다른 스레드에서도 동시에 작업하도록 하는 것을 동시성 프로그래밍이라고 합니다.

iOS에서 동시성 프로그래밍을 하는 방법은 GCD와 Swift Concurrency를 사용하는 방법으로 크게 2가지가 있습니다.

# GCD
> Grand Central Dispatch

GCD는 Dispatch Queue에 Task를 추가하면 작업에 맞게 스레드를 자동으로 생성해서 실행하고, 작업이 종료되면 스레드를 제거합니다.

## Operation
Operation은 GCD에 기반해서 여러가지 기능을 추가된 형태입니다.

- 동시에 실행할 수 있는 동작의 최대 개수를 지정할 수 있습니다.
- 해당 작업의 실행 상태(실행, 정지, 대기 등)을 알 수 있고, 이를 통해 Operation들을 취소 혹은 순서를 지정할 수 있습니다.
- GCD에 비해 구현이 더 복잡합니다.

# async
Task를 Queue에 넘기고 나서 바로 다음 Task를 실행합니다.

# sync
Task를 Queue에 넘기고 나서 끝날때 까지 기다린 후 다음 Task를 실행합니다.

## 비동기 처리 하는 이유?
만약 동기적으로 처리한다면, 하나의 작업이 끝날 때 까지 다음 작업을 실행할 수 없습니다.
하지만 비동기적으로 처리한다면, 하나의 작업이 끝나지 않아도 다음 작업을 실행할 수 있기에 시간 절약을 할 수 있습니다.

---

# Serial Queue
분산 처리 시킨 작업을 **다른 한개의 스레드**에서 처리하는 Queue입니다.

# Concurrent Queue
분산 처리 시킨 작업을 **다른 여러개의 스레드**에서 처리하는 Queue입니다.

---

- sync (동기)
- async (비동기)
- serial (직렬)
- concurrent (동시)

# async vs sync
작업을 **보내는 시점에서 기다릴지 말지**에 대해 다루는 것.

# Serial vs Concurrent
Queue로 보내는 작업들을 **한 개의 스레드**에서 처리할 것인지, **여러 개의 스레드**에서 처리할 것인지에 대해 다루는 것.

## Serial Queue.sync
queue에 넘긴 task가 끝날때까지 멈춰있고(sync), 넘겨진 task는 같은 스레드에 보내지기 때문에 먼저 담겨있던 작업들이 모두 끝나야 실행.

## Serial Queue.async
task가 queue에 넘기자마자 반환되고(async), 넘겨진 task는 같은 스레드에 보내지기 때문에 먼저 담겨있던 작업들이 모두 끝나야 실행.

## Concurrent Queue.sync
queue에 넘긴 task가 끝날때까지 멈춰있고(sync), 넘겨진 task는 다른 스레드에 보내지기 때문에 먼저 담겨있던 작업들이 모두 끝나지 않아도 실행.

## Concurrent Queue.async
task가 queue에 넘기자마자 반환되고(async), 넘겨진 task는 다른 스레드에 보내지기 때문에 먼저 담겨있던 작업들이 모두 끝나지 않아도 실행.

---

# DispatchQueue의 종류
- Main Queue
- Global Queue
- Custom Queue (Private Queue)

## Main Queue
- 오직 한 개만 존재
- Serial Queue (Main Thread는 오직 한 개만 존재)
- 할당된 Task는 모두 Main Thread에서 실행

## Global Queue
- Concurrent Queue
- QoS(Quality of Service)에 따라 6종류로 나뉨

### QoS (Quality of Service)

- userInteractive
  - 사용자와 **직접 상호작용**하는 작업 (UI, 애니메이션 등)
  - 사용자의 행동에 대한 즉각적인 반응이 기대 되지만, 이를 메인 스레드에서 처리하면 많은 로드가 걸리는 작업들을 userIneractive에서 처리해서 바로 동작하는 것처럼 보이게 함.
- userInitiated
  - 클릭할 때 작업을 수행하는 것과 같은 **즉각적인 결과**가 필요한 작업. (ex. 저장된 문서 열기)
  - 하지만 userIneractive 보다는 조금 오래걸릴 수 있고 유저가 어느정도 이를 인지하고 있음.
- default
  - **일반**적인 작업
- utility
  - 보통 **Progress bar와 함께** 실행되는 작업 (ex. 파일 다운로드)
- background
  - 유저가 직접적으로 **인지하지 않는, 시간이 덜 중요한** 작업. (ex. 동기화 및 백업)
- unspecified (Legacy API)
  - QoS 정보가 없음을 나타냄. 거의 사용할 일이 없습니다.

우선순위가 더 높은 일에 더 많은 스레드를 배치합니다.

## Custom Queue
- 커스텀으로 만드는 Queue
- 디폴트로 Serial Queue, 하지만 Concurrent로 설정가능
- QoS 설정도 가능

DispatchQueue 생성할 때 `(label:)` 을 받는 initializer를 사용하여 생성하면 Custom Queue 사용 가능합니다.
attributes: 에는 queue의 타입(Serial, Concurrent)을 설정할 수 있습니다.
qos: 에는 QoS를 설정할 수 있습니다.

# 주의사항
## UI는 Main Thread에서만 처리한다.
UI 업데이트를 Main Thread에서 처리하지 않는다면 `Main Thread Checker` 경고가 뜹니다.

## Sync
1. 메인 큐에서 다른 큐로 Task를 보낼 때 sync를 사용하면 안된다.
   - sync로 보내게되면 다른 작업들이 끝날때까지 UI 업데이트가 지연되게 됩니다.
2. 현재와 같은 큐에 sync로 Task를 보내면 안된다.
   - 데드락에 걸립니다.
3. 메인 스레드에서 DispatchQueue.main.sync를 하면 안된다
   - 마찬가지로 데드락에 걸립니다.

## Closure 캡쳐
순환 참조가 생기지는 않지만, 스레드 클로져가 실행된 이후에 ViewController가 메모리에서 해제된다.


# Dispatch Group
여러 스레드로 분배된 작업들이 끝나는 시점을 하나로 그룹지어서 한 번에 파악하고 싶을 때 사용합니다.

ex) 모든 이미지 다운로드가 완료된 시점에 특정 행동을 해야할 때

## 사용법
1. Dispatch Group 생성

```swift
let group = DispatchGroup()
```

2. Queue에 async로 보낼때 group 파라미터에 생성한 그룹 추가

```swift
DispatchQueue.global().async(group: group) {
    // Task
}
```

task를 다른 큐로 보내더라도 같은 그룹으로 지정할 수 있습니다.

```swift
DispatchQueue.global().async(group: group) { 
  // Task 
}
DispatchQueue.global(qos: utility).async(group: group) { // Task }
```

3. `notify(queue:)`를 통해 notification block을 넘김
```swift
group.notify(queue: .main) {
    // Task
}
```

queue는 어디 스레드에서 notification block을 실행할지를 결정합니다.

`wait()`를 통해 그룹의 작업이 끝날 때까지 현재 스레드를 block시킬 수 있습니다.

`wait(timeout:)`을 통해 최대 얼마나 기다릴지를 설정할 수 있습니다.

`wait(timeout:)`는 `DispatchTimeoutResult`를 반환합니다. 이를 값을 통해 시간 내에 그룹 내 모든 task가 완료되었는지 확인할 수 있습니다.

`wait()`은 메인 스레드에서 사용하면 안됩니다. task가 끝날 때까지 메인 스레드가 block, 즉 앱이 멈추기 때문입니다.

또한 그룹 내의 task는 `wait()`가 실행되고 있는 현재의 스레드로 할당이 되어선 안됩니다. task가 끝날때까지 스레드가 멈춰있을 텐데 그곳으로 task가 할당되면 데드락에 걸리기 때문입니다.

## dispatchGroup.enter() & dispatchGroup.leave()
Dispatch Group으로 묶이는 Task안에 비동기 작업이 포함되어 있다면, 해당 작업을 보낼 때와 끝날 때 `enter()`와 `leave()`를 호출해야 합니다.

`enter()`와 `leave()`는 서로 짝지어 쓰이면서 task reference cound를 적절히 관리하는데, enter()는 count를 +1, leave()는 count를 -1 해줍니다.

이 count가 0이 되는 시점이 그룹의 모든 task가 끝난 시점입니다.

# DispatchWorkItem
DispatchWorkItem은 Dispatch Queue에 보내는 Task를 추상화한 것입니다.
closure를 통해 보내던 방식을 캡슐화한 class입니다.

DispatchWorkItem을 생성할 때, qos 파라미터를 통해 작업의 우선순위도 설정할 수 있습니다.

DispatchWorkItem은 DispatchQueue에 async(execute:)로 큐에 보낼 수 있습니다.
```swift
DispatchQueue.global().async(execute: group)
```

혹은 perform을 통해 sync하게 큐에 보낼 수도 있습니다.
```swift
group.perform()
```

## 취소 기능
DispatchWorkItem은 `cancel()`을 통해 취소할 수 있습니다.

- 작업 실행 전에 cancel()을 호출하면, 작업이 제거됩니다.
- 작업 실행 중에 cancel()을 호출하면, 작업이 취소되지는 않고 isCancelled 프로퍼티가 true가 됩니다.

`notify(queue:execute:)`를 통해 작업 A가 끝난 후 작업 B가 특정 큐에서 실행되도록 지정할 수 있습니다.

# Dispatch Semaphore
공유 자원에 접근할 수 있는 작업의 수를 제한하는 기능을 제공합니다.

```swift
let semaphore = DispatchSemaphore(value: 2)
```
(value:)를 통해 공유 자원에 접근 가능한 task 수를 명시하고, 임계 구역에 들어갈 때 semaphore의 wait()을 호출하고, 임계 구역을 빠져나올 때 signal()을 호출합니다.

`wait()`은 semaphore를 -1 해주고, `signal()`은 semaphore를 +1 해줍니다.

작업의 수를 제한하는 기능이 아닌 두 스레드가 특정 이벤트의 완료 상태를 동기화 하는 경우에도 사용할 수 있습니다.

예를 들어 스레드 A가 작업 A를 실행 중이고, 스레드 B는 작업 A가 끝난 후에 무언가를 실행하려고 할 때, 사용할 수 있습니다.

해당 용도롤 사용하기 위해서는 DispatchSemaphore의 value를 0으로 설정합니다.

이 상황에서 스레드 B는 작업을 기다리기 위해 wait()을 호출하고, 스레드 A는 작업이 끝났음을 알리기 위해 signal()을 호출합니다.

# Concurrency 문제
1. Race Condition
2. Deadlock
3. Priority Inversion

## Race Condition
공유 자원에 대해 여러 개의 스레드가 동시에 접근할 때, 예상치 못한 결과를 가져오는 것을 의미합니다.

## Deadlock
두 개 이상의 스레드가 서로가 가진 자원을 기다리면서 무한정 대기하는 상태를 의미합니다.

## Priority Inversion
high priority task가 필요한 자원을 low priority task 가 잠그고 있는 경우입니다.

- Serial Queue에서 high priority task가 low priority task의 뒤에 보내지는 경우
- Operation에서 high priority task가 low priority task에 의존하는 경우

등의 환경에서 Priority Inversion이 발생할 수 있습니다.

사실 high priority task가 필요한 자원을 low priority task 가 배타적으로 사용하고 있는 경우에 발생하는 Priority Inversion 문제는 GCD 자체적으로 우선 순위 조정을 통해 문제를 해결합니다. (자원을 점유하고 있는 task의 우선순위를 높여서 처리)