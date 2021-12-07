# Test

## 이름 짓기

### 테스트 케이스 이름
- JUnit5를 사용하는 경우에는 `@DisplayName`을 통해 테스트 케이스 이름을 정의하고 함수명은 중복되지 않으면서 최대한 유지보수가 필요없도록 만들어준다.
```kotlin
// Do
@DisplayName("1 더하기 2는 3이어야 한다")
@Test
fun add() { /* Test Code */ }

@DisplayName("1 더하기 2는 3이어야 한다")
@Test
fun test1() { /* Test Code */ }
```

```kotlin
// Do not
@DisplayName("1 더하기 2는 3이어야 한다")
@Test
fun `1 더하기 2는 3이어야 한다`() { /* Test Code */ }
```

- JUnit4를 사용하는 경우에는 선택의 여지가 없으므로 무조건 함수명으로 테스트 케이스 이름을 정의한다.
```kotlin
@Test
fun `1 더하기 2는 3이어야 한다`() { /**/ }
```

- 클래스명이나 함수명은 변경될 수 있으므로 테스트 케이스 이름에는 클래스명이나 함수명을 넣는 것을 최대한 지양한다.
```kotlin
// Do (recommended)
@Test
fun `1 더하기 2는 3이어야 한다`() { /**/ }
```

```kotlin
// Do not (optional)
@Test
fun `Calculator에서 add(1, 2)를 호출하면 3을 반환해야 한다`() { /**/ }
```
