# DaJuLang 🚀

**파이썬처럼 쉽고 C처럼 빠른** 프로그래밍 언어.

```dajulang
func 인사(이름) {
    return "안녕, " + 이름 + "!"
}
print(인사("세계"))
```

## 다운로드 (베타)

[**Releases**](https://github.com/lenftk/dajulang-lang/releases) 에서 OS 에 맞는 파일을 받으세요:

| OS | 파일 |
|----|------|
| Windows x64 | `dajulang-windows-x64.zip` |
| Linux x64 | `dajulang-linux-x64.tar.gz` |
| macOS (Apple Silicon) | `dajulang-macos-arm64.tar.gz` |
| macOS (Intel) | `dajulang-macos-x64.tar.gz` |

## 설치

**Windows**: 압축을 풀고 `install.ps1` 을 우클릭 → PowerShell 로 실행.
그러면 `djl` 명령이 어디서나 동작합니다.

```powershell
powershell -ExecutionPolicy Bypass -File install.ps1
```

**직접 실행**: 압축 안의 `djl.exe` 로 바로 실행해도 됩니다.
```
djl 프로그램.ju
```

## 빠른 시작

```dajulang
// hello.ju
print("Hello, DaJuLang!")

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

## 특징

- **쉬운 문법** — 한글 변수/함수명, f-string, 딕셔너리, 람다, match
- **빠른 성능** — 바이트코드 VM + JIT (베타 빌드)
- **패키지 매니저** — `jpm install <패키지>` 로 라이브러리 설치

```
jpm install colors     # 색상 출력
jpm install strings    # 문자열 유틸
jpm install mathx      # 수학 유틸
```

## 이 베타 빌드에 대해

가볍고 의존성 없는 **기본 빌드**입니다 (어떤 PC 에서나 바로 실행).
- ✅ 언어 전체 기능 (변수/함수/클래스/텐서/파일·수학·문자열)
- ✅ 패키지 매니저 (jpm)
- ⏳ Python 라이브러리 연동, AOT 네이티브 컴파일, GPU 가속 — 다음 빌드 예정

버그 제보/피드백은 [Issues](https://github.com/lenftk/dajulang-lang/issues) 로 부탁드립니다. 🙏
