# Compose

## Layout

### `Spacer()` vs `Modifier.padding()` 사용 기준
- `Column(),` `Row()`와 같이 Linear 형태의 Layout에서 margin 개념이면 `Spacer()`를 사용한다.
```kotlin
Column {
    Title()
    Spacer(modifier = Modifier.height(8.dp))
    Content()
}
```
- 그 외는 `Modifier.padding()`을 사용한다.