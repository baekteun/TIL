# Swift Concurrency

## GCD
기존 Swift에서는 동시성 프로그래밍을 구현하기 위해 GCD API를 사용했습니다. 
GCD는 비동기로 실행하고자 하는 코드 블럭을 DispatchQueue라는 선입선출 Queue에 넣어 스레드에 작업을 할당하는 방식입니다. GCD는 escaping closure를 많이 사용합니다.

## Swift Concurrency
2021 WWDC에 발표된 동시성 프로그래밍 API입니다.
좀 더 쉽게 비동기 코드를 작성하기 위해서라고 WWDC에서 소개하고 있습니다. async로 비동기 코드임을 나타내고, await로 비동기 코드가 완료될 때까지 기다린다는 의미를 가집니다.
특징으로 GCD에 비해 적은 코드 수와 가독성의 차이가 큽니다.

Swift Concurrency는 
- 가독성 향상
- Race Condition 처리 용이
- 우선순위 관리 용이
- 스레드 관리 용이