# Test

## 이름 짓기

### 테스트 케이스 이름
- JUnit5를 사용하는 경우에는 `@DisplayName`을 통해 테스트 케이스 이름을 정의하고 함수명은 중복되지 않으면서 최대한 유지보수가 필요없도록 만들어준다.

Do
```kotlin
@DisplayName("1 더하기 2는 3이어야 한다")
@Test
fun add() { /* Test Code */ }

@DisplayName("1 더하기 2는 3이어야 한다")
@Test
fun test1() { /* Test Code */ }
```

Do not
```kotlin
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

Do (recommended)
```kotlin
@Test
fun `1 더하기 2는 3이어야 한다`() { /**/ }
```

Do not (optional)
```kotlin
@Test
fun `Calculator에서 add(1, 2)를 호출하면 3을 반환해야 한다`() { /**/ }
```

### 테스트 클래스 이름
- IDE의 기본을 따라 `Calculator`에 대한 테스트 클래스는 `CalculatorTest`로 한다.
```kotlin
// Calculator.kt
class Calculator { /* ... */ }
```
```kotlin
// CalculatorTest.kt
class CalculatorTest { /* ... */ }
```

- top-level 함수만 모여있는 `CalculatorExtension.kt` 파일에 대한 테스트 클래스 이름은 `CalculatorExtensionTest.kt`로 한다.
```kotlin
// CalculatorExtension.kt
fun Calculator.foo() { /* ... */ }
fun Calculator.bar() { /* ... */ }
```
```kotlin
// CalculatorExtensionTest.kt
class CalculatorExtensionTest { /* ... */ }
```

> IDE에서는 `CalculatorExtension.kt` 파일에 대한 테스트 클래스를 기본적으로 `CalculatorExtensionKtTest.kt`로 인식한다.
> 그럼에도 불구하고 `CalculatorExtensionTest.kt`와 같이 사용하는 이유는 다음과 같다. 
> 
> - IDE 기능 때문에 `Kt`를 붙이는 것이 code smell로 여겨짐
> - IDE 기능을 쓰지 못한다고 해서 테스트 코드 작성에 치명적인 이슈는 되지 않음
