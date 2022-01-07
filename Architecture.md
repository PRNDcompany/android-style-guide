# Architecture
- 코드의 Architecture는 MVVM + Clean Architecture를 사용한다.
- Clean Architecture의 기본적인 구조는 아래에 기반하고 프로젝트에 맞게 효율적인 구조로 만든다.
![](art/clean_architecture.png)


## ViewModel
- ViewModel(Presentation Layer)에는 안드로이드 프레임워크 관련 코드가 없어야함
- import android.* 코드가 없도록 유지(AAC관련 코드 제외, android.arch.*)
- https://medium.com/androiddevelopers/viewmodels-and-livedata-patterns-antipatterns-21efaef74a54
- 다만 데이터에 해당되는 `R.string.xxx`, `R.dimen.xxx`, `R.color.xxx`들은 사용할 수 있도록 함
  - (`R.id.xxx`, `R.layout.xxx`는 불가)
- `SavedStateHandle`은 생성자의 첫번째에 위치한다.

Do
```kotlin
@HiltViewModel
class XxxViewModel @Inject constructor(
  savedStateHandle: SavedStateHandle,
  private val getFooUseCase: GetFooUseCase,
) : ViewModel()
```
Do not
```kotlin
@HiltViewModel
class XxxViewModel @Inject constructor(
  private val getFooUseCase: GetFooUseCase,
  savedStateHandle: SavedStateHandle,
  private val getBarUseCase: GetBarUseCase,
) : ViewModel()

@HiltViewModel
class XxxViewModel @Inject constructor(
  private val getFooUseCase: GetFooUseCase,
  private val getBarUseCase: GetBarUseCase,
  savedStateHandle: SavedStateHandle,
) : ViewModel()
```

### Event
: [MVVM의 ViewModel에서 이벤트를 처리하는 방법 6가지](https://medium.com/prnd/mvvm%EC%9D%98-viewmodel%EC%97%90%EC%84%9C-%EC%9D%B4%EB%B2%A4%ED%8A%B8%EB%A5%BC-%EC%B2%98%EB%A6%AC%ED%95%98%EB%8A%94-%EB%B0%A9%EB%B2%95-6%EA%B0%80%EC%A7%80-31bb183a88ce)

이벤트 이름은 {행위}-{대상}-{결과} 순서의 이름 규칙을 가진다.
```kotlin
object ShowCarInfo: Event() // 행위: 보여준다, 대상: 차량 정보
object UploadImageSuccess: Event() // 행위: 업로드하다. 대상: 이미지, 결과: 성공
```
- Event의 의미에 따라 동사의 형태는 자유롭게 사용한다. (과거형, 현재형)
- Success, Complete와 같이 의미가 이중적일 때에는 기대하는 동작에 따라 적절한 이름을 선택한다.




## UseCase
- 클래스는 각 한개의 usecase를 갖는다.
- 클래스명은 xxxUseCase 와 같이 명명한다.
- List를 가져오는 UseCase의 이름은 GetXXXListUseCase와 같이 정의한다.
  - 함수의 경우 getXXXs()로 정의되나 단수를 가져오는 UseCase와 혼동의 우려가 있기때문에 UseCase이름은 List를 붙인다.

## XXXLocal
- 만약 Room DB를 사용하는 domain 클래스에 NonNull인 필드를 새로 추가하게 된다면 Local Class에서는 어쩔수없이 Nullable로 선언하고 mapping할때 default value를 지정하는 방법으로 구현해야 함
- 예)
```
- User에 email이 추가되어야함
- email이 NonNull이기때문에 UserLocal에 필드를 추가할때 email을 NonNull로 선언해야 할것 같지만
- 기존에 DB에 저장되어 있는 데이터에는 email 값이 없으므로 기존에 저장된 db를 toData()로 하려고 할때 문제가 발생함
- XXXLocal의 class는 새로 추가될때 항상 Nullable로 만들고 toData()로 mapping될때 기본값을 선언해줘야 함
```

## Model Mapping 정의/구조
- Model은 각각의 layer에 만들어져서 mapping되도록 구성한다
- 예) User라는 개념의 model에 대한 각각 layer에서의 정의

### Domain
```kotlin
data class User(){}
```
### Presentation
```kotlin
data class UserModel(){}
 
fun User.toPresentation(): UserModel
fun UserModel.toDomain(): User
```
### Data
```kotlin
data class UserEntity(){}
 
fun UserEntity.toDomain(): User
fun User.toData(): UserEntity
```
### Remote
```kotlin
data class UserResponse(){}
 
fun UserResponse.toData(): UserEntity
fun UserEntity.toRemote(): UserResponse
```
- 단, 데이터를 갱신할때 parameter로 사용되는 Param개념은 뒤에 Param으로 붙이도록 변경
: 또한 Remote에서의 해당 이름은 xxxxParamRequest로 정의
### Local
```kotlin
data class UserPref(){}
 
fun UserPref.toData(): UserEntity
fun UserEntity.toPref(): UserPref
```
- 단, 데이터를 갱신할때 parameter로 사용되는 Param개념은 뒤에 Param으로 붙이도록 변경
- 또한 Remote에서의 해당 이름은 xxxxParamRequest로 정의
