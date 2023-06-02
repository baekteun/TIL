# Map
- Returns an array containing the results of mapping the given closure over the sequence’s elements.
- sequence의 요소들에 주어진 클로저를 매핑한 결과를 담은 배열을 반환한다.

```swift
let numbers = [1, 2, 3, 4, 5]
let mappedNumbers = numbers.map { $0 * 2 }
print(mappedNumbers) // [2, 4, 6, 8, 10]
```

<br>

# CompactMap
- Returns an array containing the non-nil results of calling the given transformation with each element of this sequence.
- sequence의 요소들에 주어진 클로저를 매핑한 결과 중 nil이 아닌 것들을 담은 배열을 반환한다.

```swift
let numbers = ["1", "2", "3", "4", "5", "a", "b", "c"]
let mappedNumbers = numbers.compactMap { Int($0) }
print(mappedNumbers) // [1, 2, 3, 4, 5]
```

<br>

# FlatMap
- Returns an array containing the concatenated results of calling the given transformation with each element of this sequence.
- sequence의 요소들에 주어진 클로저를 매핑한 결과를 연결한 배열을 반환한다.

> flat : 평평한

고차원 배열을 하나 아래 차원의 배열로 바꿔준다.

```swift
let numbers = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
let mappedNumbers = numbers.flatMap { $0 }
print(mappedNumbers) // [1, 2, 3, 4, 5, 6, 7, 8, 9]
```