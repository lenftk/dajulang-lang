# DaJuLang

DaJuLang 은 간결한 문법과 네이티브 수준의 실행 성능을 목표로 하는 프로그래밍
언어이다. 본 저장소는 베타 배포본과 문서를 제공한다.

```
func 인사(이름) {
    return "안녕, " + 이름 + "!"
}
print(인사("세계"))
```

## 1. 다운로드

[Releases](https://github.com/lenftk/dajulang-lang/releases) 에서 운영체제에
맞는 배포본을 받는다.

| 운영체제 | 파일 |
|----------|------|
| Windows x64 | `dajulang-windows-x64.zip` |
| Linux x64 | `dajulang-linux-x64.tar.gz` (준비 중) |
| macOS (Apple Silicon) | `dajulang-macos-arm64.tar.gz` (준비 중) |
| macOS (Intel) | `dajulang-macos-x64.tar.gz` (준비 중) |

## 2. 설치

Windows 에서는 압축을 해제한 뒤 `install.ps1` 을 실행한다. 실행 파일이
사용자 PATH 에 등록되어 어느 위치에서나 `djl` 명령을 사용할 수 있다.

```
powershell -ExecutionPolicy Bypass -File install.ps1
```

설치 없이 압축 내부의 `djl.exe` 로 직접 실행할 수도 있다.

```
djl 프로그램.ju
```

## 3. 예제

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

전체 문법은 [SYNTAX.md](SYNTAX.md) 에 기술한다.

## 4. 패키지 관리

```
jpm install colors     // 색상 출력
jpm install strings    // 문자열 유틸리티
jpm install lists      // 리스트 유틸리티
jpm install mathx      // 수학 유틸리티
```

## 5. 베타 빌드 범위

본 배포본은 외부 의존성이 없는 기본 빌드이며, 별도 런타임 설치 없이 실행된다.

- 포함: 언어 전체 기능(변수, 함수, 클래스, 배열, 딕셔너리, 텐서, 파일·수학·문자열 처리, 문자열 보간, 유니코드 식별자), 패키지 관리자 `jpm`
- 미포함(후속 빌드 예정): Python 라이브러리 연동, AOT 네이티브 컴파일, GPU 가속

결함 보고와 제안은 [Issues](https://github.com/lenftk/dajulang-lang/issues) 로 접수한다.
