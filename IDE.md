# IDE
아래 사항들을 제외한 이외의 설정들은 자율에 맡긴다.

## Trailing comma
불필요한 code change를 줄이기 위해 trailing comma를 사용한다.
예를 들면, trailing comma를 쓰지 않은 클래스에 새로운 필드를 추가하려면 관련없는 위쪽 라인에 `,`를 추가해주어야 하는데 이러한 일을 피하기 위함이다.

### 설정 방법
- Preferences | Editor | Code Style | Kotlin | Other
- Use trailing comma 체크

```kotlin
// 설정 전
data class User(
    val name: String,
    val email: String
)

// 설정 후
data class User(
    val name: String,
    val email: String,
)
```

## Wildcard import 🚫
import가 꼬이는 현상을 방지하기 위해 Wildcard import 설정은 사용하지 않고,
single name import 설정만 사용한다

### 설정 방법
- Preferences | Editor | Code Style | Kotlin | Imports
- Use single name import 체크