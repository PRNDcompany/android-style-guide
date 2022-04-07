# IDE
아래 사항들을 제외한 이외의 설정들은 자율에 맡긴다.

## Trailing comma
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
