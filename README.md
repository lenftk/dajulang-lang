# DaJuLang

파이썬처럼 쉽고 C처럼 빠른 프로그래밍 언어.

```
func 인사(이름) {
    return "안녕, " + 이름 + "!"
}
print(인사("세계"))
```

## 다운로드

[Releases](https://github.com/lenftk/dajulang-lang/releases) 에서 OS에 맞는 파일을 받는다.

| OS | 파일 |
|----|------|
| Windows x64 | `dajulang-windows-x64.zip` |
| Linux x64 | `dajulang-linux-x64.tar.gz` (준비 중) |
| macOS (Apple Silicon) | `dajulang-macos-arm64.tar.gz` (준비 중) |
| macOS (Intel) | `dajulang-macos-x64.tar.gz` (준비 중) |

## 설치

Windows: 압축을 풀고 `install.ps1` 을 실행하면 `djl` 명령이 PATH에 등록된다.

```
powershell -ExecutionPolicy Bypass -File install.ps1
```

설치 없이 압축 안의 `djl.exe` 로 바로 실행해도 된다.

```
djl 프로그램.ju
```

## 예제

```
// hello.ju
print("Hello, DaJuLang")

let 숫자들 = [3, 1, 4, 1, 5]
print(숫자들.sorted())          // [1, 1, 3, 4, 5]

func 팩토리얼(n) {
    if n <= 1 { return 1 }
    return n * 팩토리얼(n - 1)
}
print(팩토리얼(5))               // 120
```

```
djl hello.ju
```

전체 문법은 [SYNTAX.md](SYNTAX.md) 참고.

## 패키지 매니저

```
jpm install colors     // 색상 출력
jpm install strings    // 문자열 유틸
jpm install lists      // 리스트 유틸
jpm install mathx      // 수학 유틸
```

## 베타 빌드 범위

의존성 없는 기본 빌드. 어떤 PC에서나 바로 실행된다.

- 언어 전체 기능: 변수, 함수, 클래스, 배열, 딕셔너리, 텐서, 파일/수학/문자열, f-string, 한글 이름
- 패키지 매니저 `jpm`
- 미포함(다음 빌드): Python 라이브러리 연동, AOT 네이티브 컴파일, GPU 가속

버그와 건의는 [Issues](https://github.com/lenftk/dajulang-lang/issues) 로 받는다.
