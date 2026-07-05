# DaJuLang 문법 명세

본 문서는 DaJuLang 언어의 구문(syntax)과 의미(semantics)를 기술한다.
모든 예시는 기본 빌드에서 검증되었다.

## 1. 어휘 구조

### 1.1 주석

행 주석은 `//` 로 시작하며 줄 끝까지 무시된다. 블록 주석은 지원하지 않는다.

```
// 이 줄은 주석이다
print(1)   // 문장 뒤에도 붙일 수 있다
```

### 1.2 리터럴

| 종류 | 예 |
|------|-----|
| 정수 | `42`, `-7` |
| 실수 | `3.14`, `2.0` |
| 문자열 | `"안녕"` |
| 불리언 | `true`, `false` |
| 널 | `null`, `empty` |
| 배열 | `[1, 2, 3]` |
| 딕셔너리 | `{"키": 값}` |

식별자는 유니코드를 허용하며, 한글 이름을 쓸 수 있다.

## 2. 변수

`let` 은 새 지역 변수를 선언한다. `let` 없는 대입은 기존 변수를 수정하며,
대상이 없으면 새로 만든다. 대입 연산자로 `=` 또는 `<-` 를 쓴다.

```
let name = "민주"
age = 20
score <- 95
```

함수 내부에서 `let` 없이 외부 변수를 대입하면 외부 변수가 변경된다.
지역 변수를 새로 만들려면 `let` 을 사용한다.

## 3. 연산자

### 3.1 산술

```
a + b       // 덧셈 (문자열은 연결)
a - b       // 뺄셈
a * b       // 곱셈
a / b       // 나눗셈
a % b       // 나머지
a ** b      // 거듭제곱 (우결합, 곱셈보다 우선순위 높음)
-a          // 부호 반전
```

`2 ** 3 ** 2` 는 `2 ** (3 ** 2) = 512` 로 평가된다.

### 3.2 비교와 논리

```
a == b      a != b
a < b       a <= b       a > b       a >= b
a is b      // == 의 대안

a and b     a or b       not a
```

배열과 딕셔너리의 `==` 는 원소별 값 비교이다.

### 3.3 복합 대입

```
x += 1      x -= 1      x *= 2      x /= 2      x %= 3
```

## 4. 제어 구조

### 4.1 조건

```
if age >= 20 {
    print("성인")
} else {
    print("미성년")
}
```

식(expression) 형태의 삼항 조건도 제공한다.

```
let grade = if score >= 60 then "합격" else "불합격"
```

### 4.2 분기 (match)

```
match x {
    when 1 { print("하나") }
    when 2 { print("둘") }
    else   { print("기타") }
}
```

### 4.3 반복

DaJuLang 은 여러 반복 구문을 제공하며, 모두 동등한 표현력을 가진다.

```
for i in range(0, 5) { print(i) }   // 0 1 2 3 4
for i in 0..5 { print(i) }          // 0 1 2 3 4

loop(3) { print("x") }              // 3회 반복
loop(1 ~ 5) as i { print(i) }       // i = 1 2 3 4
repeat 3 times { print("y") }       // 3회 반복
from 1 to 4 as i { print(i) }       // i = 1 2 3

while cond { ... }
```

`break` 로 반복을 중단하고, `continue` 로 다음 반복으로 넘어간다.

## 5. 함수

```
func add(a, b) { return a + b }
```

`func`, `fn`, `def` 를 함수 선언 키워드로 쓸 수 있다.
함수는 클로저를 형성하여 외부 변수를 포획한다.

```
func make_adder(n) {
    func adder(x) { return x + n }
    return adder
}
let add5 = make_adder(5)
add5(10)   // 15
```

익명 함수(람다)는 값으로 취급된다.

```
let double = func(x) { return x * 2 }
```

## 6. 클래스

```
class Counter {
    val
    func init(start) { self.val = start }
    func inc() { self.val = self.val + 1 }
    func get() { return self.val }
}

let c = Counter(5)
c.inc()
c.get()    // 6
```

`self` 또는 `this` 로 인스턴스를 참조한다. `init` 은 생성자이다.

## 7. 배열

```
let a = [3, 1, 4, 1, 5]

a[0]                // 3      첫 원소
a[-1]               // 5      마지막 원소
a[1:3]              // [1, 4] 부분 배열
a[:3]               // [3, 1, 4]
a[2:]               // [4, 1, 5]
a[::2]              // [3, 4, 5]  간격 2

a.sorted()          // 정렬된 사본
a.reverse()         // 뒤집은 사본
a.sum()             // 합
a.contains(4)       // 포함 여부
a.unique()          // 중복 제거
a.map(func(x) { return x * 2 })
a.filter(func(x) { return x > 2 })
a.reduce(func(acc, x) { return acc + x }, 0)
len(a)
```

## 8. 딕셔너리

```
let d = {"a": 1, "b": 2}

d["a"]              // 1
d["c"] = 3          // 추가/수정
d.keys()
d.values()
d.has("a")          // true
d.len()             // 3
```

## 9. 문자열

```
let s = "Hello World"

s.upper()               s.lower()
s.len()
s.split(" ")            // ["Hello", "World"]
s.contains("World")
s.replace("World", "DaJuLang")
s.starts_with("Hello")  s.ends_with("World")
s.char_at(0)            s.index_of("o")
s[0:5]                  // "Hello"
```

문자열 보간(f-string)은 `f"..."` 안에서 `{식}` 을 평가한다.

```
let name = "다줄랭"
let n = 1
print(f"{name} v{n}")   // 다줄랭 v1
```

## 10. 구조 분해와 순회 도우미

```
let a, b = 1, 2                 // 튜플 언패킹

for i, v in enumerate(["가", "나"]) { print(i, v) }
for x, y in zip([1, 2], [3, 4]) { print(x + y) }
```

## 11. 예외 처리

```
try {
    throw "오류 메시지"
} catch e {
    print(e)
}
```

## 12. 모듈

`import` 로 내장 모듈을 사용하며, `as` 로 별칭을 지정한다.

```
import math
import math as m

math.sqrt(16)       // 4
math.factorial(5)   // 120
math.gcd(12, 18)    // 6
math.pi()
m.sqrt(9)           // 3

import crypto
crypto.sha256("비밀번호")
crypto.base64_encode("안녕")

import fs
fs.write("a.txt", "내용")
fs.read("a.txt")
```

## 13. 텐서

텐서는 일급 값이며, 연산자로 직접 다룬다.

```
let a = tensor([1.0, 2.0, 3.0, 4.0], [2, 2])   // 2x2 행렬
let b = ones([2, 2])
let z = zeros([3])

a + b     a - b     a * b     a / b      // 원소별 연산
a + 1     a * 2     10 - a               // 스칼라 브로드캐스트
a @ b                                    // 행렬곱
a > 0.5   a == b                         // 비교 (0/1 마스크)

a.sum()   a.mean()   a.shape()   a.T
a.relu()  a.sigmoid()  a.tanh()
```

### 13.1 자동 미분

```
let w = tensor([2.0, 3.0], [2]).enable_grad()
let x = tensor([5.0, 7.0], [2])
let loss = w.mul(x).sum_tensor()
loss.backward()
w.grad()            // tensor([5, 7], shape=[2])
```

### 13.2 신경망

```
let x = tensor([1.0, 2.0, 3.0, 4.0], [4, 1])
let y = tensor([2.0, 4.0, 6.0, 8.0], [4, 1])

let model = nn {
    dense(1, 8, tanh)
    dense(8, 1, linear)
}
model.train(x, y)           // lr, epochs 는 생략 가능
model(x)                    // 예측
model.loss(x, y)            // 손실
```

활성화 함수로 `relu`, `leaky_relu`, `sigmoid`, `tanh`, `linear` 을 지원한다.

## 14. 데코레이터

함수 선언 앞에 `@이름` 을 붙일 수 있다.

```
@memo
func fib(n) {
    if n <= 1 { return n }
    return fib(n - 1) + fib(n - 2)
}
```

## 15. 매직 패키지 (문법 확장)

패키지 파일에 `alias 원문 => 대체` 를 선언하면, 그 패키지를 `import` 한
파일에 한하여 토큰이 재정의된다. 치환은 동시에 적용되므로 두 토큰을
맞바꿔도 충돌하지 않는다.

```
// mypkg 패키지 내부
alias 함수 => func
alias 출력 => print
```
```
import mypkg
함수 인사() { 출력("안녕") }
인사()
```

연산자와 키워드, 식별자를 모두 별칭 지정할 수 있다. 문자열 리터럴의
내용과, 해당 패키지를 `import` 하지 않은 파일은 영향을 받지 않는다.

## 16. 패키지 관리

```
jpm install <이름>      // 설치
jpm list                // 목록
jpm uninstall <이름>    // 제거
```

설치된 패키지는 `import <이름>` 으로 사용한다.
