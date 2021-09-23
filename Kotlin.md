# Kotlin
## 비교
- Boolean의 경우 `if (a?.b?.isTraded ?: false)` 보다는 `if (a?.b?.isTraded == true)` 와 같은 방식으로 구현한다.

## Custom accessor VS Function
- 행동을 나타내는 개념이면 function
- 상태나 값등 정보를 가져오는 개념이면 custom accessor

> [Kotlin: should I define Function or Property?](https://blog.kotlin-academy.com/kotlin-should-i-define-function-or-property-6786951da909)

## 개행
- 생성자, 함수에서 Parameter를 정의할때 한줄로 정의 가능하면 한줄, 그렇지 않으면 각 parameter별로 개행한다.

### LiveData
- xml에서 클릭시 사용되는 LiveData의 변수명은 xxxEvent로 선언: [Google blueprint 코드 참고](https://github.com/android/architecture-samples/blob/272cd63c8e6e37eecc0398a19415f7c4dc6950d5/app/src/main/java/com/example/android/architecture/blueprints/todoapp/taskdetail/TaskDetailViewModel.kt#L60)

## Statement
### when
- 한 줄에 들어가는 when 분기는 중괄호를 사용하지 않는다.
```kotlin
when (value) {
	0 -> return
	// ...
}
```

- 여러개의 조건을 동시에 사용하는 경우 `->`를 포함한 블록은 내려서 작성한다.
```kotlin
when (value) {
	foo -> // ...
	bar,
	baz
	-> return
}
```

- when statement를 enum class 또는 sealed class와 함께 쓰는 경우에는 `exhaustive` 확장 변수를 통해 강제로 when expression으로 변경하여 사용한다.
```kotlin
enum class Color {
    RED, BLUE, GREEN
}

when (color) {
    RED -> // ...
    BLUE -> // ...
    GREEN -> // ...
}.exhaustive
```

## 함수 이름
- ViewModel을 observe()할때 모아놓는 함수 이름
```kotlin
setupXXX()
```

- 서버에서 데이터를 불러올때 함수 이름
```kotlin
fetchXXX()
```

- 서버에 저장할때 함수 이름
```kotlin
saveXXX()
```

- Return이 있는 데이터를 불러올때 함수 이름
```kotlin
getXXX()
```

- 특정 객체를 찾는 함수이름
```
findXXX()
```

- 복수형을 가져올때는 뒤에 s를 붙인다
```kotlin
getBrands()      // O
getBrandList()   // X
```
