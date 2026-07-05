# DaJuLang 문법

## 변수

```
let name = "민주"      // let 은 선택
age = 20
pi = 3.14
```

`let` 은 새 지역 변수를 선언한다. `let` 없는 대입은 이미 있는 변수를 수정하고,
없으면 만든다. 함수 안에서 `let` 없이 바깥 변수를 대입하면 바깥 변수가 바뀐다.

## 출력과 입력

```
print("안녕하세요")
print(age)
let x = input("이름: ")
```

## 산술 / 비교 / 논리

```
1 + 2 * 3        // 7
10 / 3           // 3.333...
10 % 3           // 1
2 ** 10          // 1024

3 < 5            // true
a == b           // 값 비교 (배열/딕셔너리는 원소별 비교)
a != b

a and b
a or b
not a
```

## 조건

```
if age >= 20 {
    print("성인")
} else {
    print("미성년")
}

// 인라인
let v = if 1 < 2 then 10 else 20
```

## 반복

```
for i in range(0, 5) { print(i) }   // 0 1 2 3 4
for i in 0..5 { print(i) }          // 0 1 2 3 4

loop(3) { print("x") }              // 3번
loop(1 ~ 5) as i { print(i) }       // 1 2 3 4

let i = 0
while i < 10 { i = i + 1 }

break       // 반복 중단
continue    // 다음 반복으로
```

## match

```
match x {
    when 1 { print("하나") }
    when 2 { print("둘") }
    else   { print("기타") }
}
```

## 함수

```
func add(a, b) { return a + b }
print(add(3, 4))                    // 7

// 클로저 (바깥 변수 참조)
func make_adder(n) {
    func adder(x) { return x + n }
    return adder
}
let add5 = make_adder(5)
print(add5(10))                     // 15

// 람다
let double = func(x) { return x * 2 }
```

## 클래스

```
class Counter {
    val
    func init(start) { self.val = start }
    func inc() { self.val = self.val + 1 }
    func get() { return self.val }
}

let c = Counter(5)
c.inc()
print(c.get())                      // 6
```

## 배열

```
let nums = [3, 1, 4, 1, 5]

nums.sorted()       // [1, 1, 3, 4, 5]
nums.sum()          // 14
nums.reverse()      // [5, 1, 4, 1, 3]
nums.contains(4)    // true
nums.map(func(x) { return x * 2 })
nums.filter(func(x) { return x > 2 })
nums.unique()
len(nums)

nums[0]             // 3     (첫 원소)
nums[-1]            // 5     (마지막 원소)
nums[1:3]           // [1, 4]  (슬라이스)
nums[::2]           // [3, 4, 5]  (2칸씩)
```

## 딕셔너리

```
let d = {"a": 1, "b": 2}
d["a"]              // 1
d["c"] = 3
d.keys()
d.values()
d.has("a")          // true
d.len()             // 3
```

## 문자열

```
let s = "Hello World"
s.upper()               // "HELLO WORLD"
s.lower()
s.len()
s.split(" ")            // ["Hello", "World"]
s.contains("World")     // true
s.replace("World", "DaJuLang")
s.starts_with("Hello")
s[0:5]                  // "Hello"  (슬라이스)

// f-string
let 이름 = "다줄랭"
let n = 1
print(f"{이름} v{n} 시작")
```

## 튜플 언패킹 / enumerate / zip

```
let a, b = 1, 2

for i, v in enumerate(["가", "나"]) { print(i, v) }   // 0 가 / 1 나
for x, y in zip([1, 2], [3, 4]) { print(x + y) }      // 4 / 6
```

## 예외 처리

```
try {
    throw "문제 발생"
} catch e {
    print(e)
}
```

## 내장 모듈

```
import math
math.sqrt(16)           // 4
math.factorial(5)       // 120
math.gcd(12, 18)        // 6
math.pi()

import crypto
crypto.sha256("비밀번호")
crypto.base64_encode("안녕")

import fs
fs.write("a.txt", "내용")
fs.read("a.txt")
```

## 텐서

배열/행렬 연산을 연산자로 직접 다룬다.

```
let a = tensor([1.0, 2.0, 3.0, 4.0], [2, 2])   // 2x2 행렬
let b = ones([2, 2])
let z = zeros([3])

a + b     a - b     a * b     a / b     // 원소별
a + 1     a * 2     10 - a                // 스칼라 브로드캐스트
a @ b                                     // 행렬곱
a > 0.5   a == b                          // 비교 (0/1 마스크)

a.sum()   a.mean()   a.shape()   a.T
a.relu()  a.sigmoid()  a.tanh()
```

## 패키지

```
import colors
import strings

print(colors.colored("빨강", colors.RED))
print(strings.pad_left("7", 3, "0"))    // "007"
```

`jpm install <이름>` 으로 패키지를 설치한다.
