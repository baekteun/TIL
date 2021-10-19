TIL... 인가?

# Swift 알고리즘


## 기본
- Optional은 속도를 위해 강제 Unwrapping으로 처리한다 ( ex: readLine()! )
    - nil처리가 필요할 경우 if let, guard let 을 상황에 맞춰 사용한다.
- Swift에는 ++가 없다. 그러니 += 을 써야한다.
- type은 type(of: input) 으로 확인한다.
- _ = String(24, radix: 2) -> 24를 2진수로 변환
- _ = Int(100101, radix: 2) -> 2진수 100101를 10진수로 변환

## 입력
## readLine()
### 한줄만 입력
- readLine()!

### Int로 입력
- Int(readLine()!)!
    
### 기본 (String.SubSequence) 배열로 입력
- readLine()!.split(" ")
    - 공백기준(" ")으로 나눠서 입력 (String.SubSequence 배열)
   
### Int 배열로 입력
- readLine()!.split(" ").map{Int($0)!}
    - Int 배열
    
### String 배열로
- readLine()!.split(" ").map{String($0)}
    - String 배열

### 가끔나는 런타임 오류
- guard let read = readLine() else { return }
- if let read = readLine(){ }

- readLine() 을 할 때 쓰레기 값이 들어가면 에러가 뜨기도 하니 이러면 guard let 이나 if let을 사용하면 해결될 수도 있다.


## print
### 일반 출력
- print(content)

### 끝문자
- print(content, terminator: " ")
    - terminator를 사용하면 마지막에 들어갈 문자열을 바꿀 수 있다. (기본 줄바꿈)
    
    
## String
### 대문자
- str.uppercased()
    - 전체 대문자로 변경
    
### 소문자
- str.lowercased()
    - 전체 소문자로 변경
    
### 문자열 포함 여부
- str.contains(content)
    - 문자열이 포함되어 있는지 확인

### 문자열 변환
- str.replacingOccurrences(of: A, with: B)
    - str문자열의 of 문자열(A) 를 with 문자열(B) 로 변경
    - 원본에 영향이 아닌 변환된 문자열로 return된다
    
### 문자열 인덱스
- str[str.startIndex]
    - str의 첫번째 인덱스 문자열을 가져온다.
    - swift는 인덱스에 Int가 아닌 String.Index 타입이 들어감
    - str[str.index(name.startIndex, offsetBt: 2)]
        - 위가 str[2]와 같은 의미이다.
 
 ### 문자열 배열 합쳐서 문자열 하나 만들기       
- ["a", "b", "c"].joined()
    - 문자열 배열을 하나의 문자열로 만든다
    - joined(separator: " "), separator를 사용하면 문자열을 붙일때마다 separator가 들어간다

### 아스키코드로 변환
- Character(str).asciiValue!
    - Character로 변환된 str의 asciiValue를 반환


## Array
### 초기화
- var arr = [type]() -> 1차원 빈 배열
- var arr: [Int] = []

- var arr = [[Int]]() -> 2차원 빈 배열

- var arr = Array(repeating: n, count: m) -> m만큼의 크기에서 n으로 채워진 1치원 배열

- var arr = Array(repeating: Array(repeating: n, count: m), count, M) -> M x m 만큼의 크기의 n으로 채워진 2차원 배열
    - M만큼의 크기에 m 크기의 n으로 채워진 1차원 배열 채워짐

- var arr = Array(1...100) -> 1부터 100까지의 등차수열로 만들어진 1차원 배열

### 정렬
- arr.sort() -> 오름차순 정렬
- arr.sort(by: >) -> 내림차순 정렬

### 사용법
- arr.fitst -> arr의 첫번째 요소를 Optional로 반환 

- arr[index] -> arr배열의 index번째 원소

- arr.firstIndex(of: n) -> arr에서 n이라는 원소의 첫번째 인덱스를 찾는다

### 요소 추가
- arr.append(n) -> 배열의 가장 뒤에 n를 추가

- arr.insert(n, at: m) -> arr의 m번째 인덱스에 n을 삽입

### 배열 반전
- arr.reverse() -> arr을 반전시킨다.

- _ = arr.reversed() -> 반전된 arr을 반환

### 삭제
- arr.remove(at: n) -> arr의 n번째 인덱스의 원소를 삭제

- arr.removeFirst() -> 배열의 첫번째 요소를 제거하고 제거된 값을 반환 -> 비어있을 시 Error

- arr.removeLast() -> 배열의 마지막 요소를 제거하고 제거된 값을 반환 -> 비어있을 시 Error
- arr.popLast() -> 배열의 마지막 요소를 제거하고 제거된 값을 Optional로 반환

- arr.removeAll() -> arr의 모든 원소 삭제

- arr.removeAll(where: {$0 % 2 == 0} ) -> 조건에 만족하는 원소 삭제
- arr.removeAll{$0 % 2 == 0} -> 위와 동일

### swap
- arr.swap(i, k) -> arr의 i번째 인덱스와 k번째 인덱스를 swap

### min, max
- arr.min() -> arr의 최솟값을 Optional로 반환

- arr.max() -> arr의 최댓값을 Optional로 반환

### map
- _ = arr.map{String($0)} -> arr의 모든 원소를 Stirng으로 변환시킨 배열 반환

### filter
- _ =  arr.filter{$0 % 2 == 0} -> arr의 원소중 2로 나눈 나머지가 2인것을 반환
- _ =  arr.filter{$0 % 2 == 0}.count -> arr의 원소중 2로 나눈 나머지가 2인것의 수를 반환


### reduce
- arr.reduce(0){ {(o1: Int, o2: Int) in n1+n2 }} -> arr(Int배열)의 요소를 0부터 시작해 모두 더한 값
- arr.reduce(0, +) -> arr(Int배열)의 요소를 0부터 시작해 모두 더한 값
- arr.reduce(0, -) -> arr(Int배열)의 요소를 0부터 시작해 모두 뺀 값
- arr.reduce(1, *) -> arr(Int배열)의 요소를 0부터 시작해 모두 곱한 값


## for
### 배열의 요소 담기 
- for i in arr{ } -> i안에 arr의 원소를 순차적으로 넣는다 

### for (index로)
- for i in 0..<arr.count {} -> 0부터 arr의 크기까지 i에 들어간다 
- for i in arr.indices {} -> 위와 동일

### enumrated()
- for (i,k) in arr.enumrated() {} -> i에는 인덱스가, k에는 값이 들어간다

### stride
- for i in stride(from: 0, to: 10, by: 2) {} -> 0부터 10까지 (10제외) 2만큼 += 되면서 i에 값이 들어가며 실행됨
- for i in stride(from: 0, through: 10, by: 2) {} -> 0부터 10까지 (10포함) 2만큼 += 되면서 i에 값이 들어가며 실행됨


## Dictionary
### 초기화
- var dict: [String:Int] = [:] -> String타입 key의 Int타입 값인 빈 빈 딕셔너리 생성
- var dict: [String:Int]() -> 위와 동일

### 생성
- var dict = ["a":1, "b":2]

### 수정
- dict.updateValue(2, forKey: "a") -> "a" 키의 값을 2로 수정
- dict["a"] = 2 -> "a" 키의 값을 2로 수정

### 추가
- dict["c"] = 3 -> "c" 키에 3이라는 값 추가
- dict.update(4, forKey: "c") -> "c"키가 있으면 값을 변경

### 삭제
- dict.removeValue(forKey: "a") -> "a" 키를 삭제
- dict.removeAll() -> 전체 삭제

### for
- for (i, k) in dict {} -> dict의 키(i)와 값(k)가 들어가며 실행됨 (순서 없음)

### 정렬
- _ = dict.sorted(by: {$0.key < $0.key}) -> key를 기준으로 정렬
- _ = dict.sorted(by: {$0.value < $0.value}) -> value를 기준으로 정렬

## 수학
### 최솟값
- min(x,y ... ) -> 요소중 최솟값을 반환

### 최댓값
- max(x,y ... ) -> 요소중 최댓값을 반환

### 절댓값
- abs(n) -> n의 절댓값을 반환

### 제곱근
- sqrt(n) -> n의 제곱근을 반환

### 제곱
- pow(n, 2.0) -> n의 2.0 제곱을 반환

### 올림 
- ceil(2.3) -> 2.3의 올림수를 반환

### 내림
- floor(2.8) -> 2.8의 내림수를 반환

### 반올림
- round(2.6) -> 2.6의 반올림수를 반환


## 종료
### exit
- exit(0) -> exit code 0으로 process 종료

