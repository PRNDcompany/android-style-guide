# Architecture
- 코드의 Architecture는 MVVM + Clean Architecture를 사용한다.
- Clean Architecture의 기본적인 구조는 아래에 기반하고 프로젝트에 맞게 효율적인 구조로 만든다.
![](art/clean_architecture.png)


## ViewModel
- ViewModel(Presentation Layer)에는 안드로이드 프레임워크 관련 코드가 없어야함
- import android.* 코드가 없도록 유지(AAC관련 코드 제외, android.arch.*)
- https://medium.com/androiddevelopers/viewmodels-and-livedata-patterns-antipatterns-21efaef74a54
- 다만 데이터에 해당되는 `R.string.xxx`, `R.dimen.xxx`, `R.color.xxx`들은 사용할 수 있도록 함
 : (`R.id.xxx`, `R.layout.xxx`는 불가)


## UseCase
- 클래스는 각 한개의 usecase를 갖는다.
- 클래스명은 xxxUseCase 와 같이 명명한다.
- List를 가져오는 UseCase의 이름은 GetXXXListUseCase와 같이 정의한다
: 함수의 경우 getXXXs()로 정의되나 단수를 가져오는 UseCase와 혼동의 우려가 있기때문에 UseCase이름은 List를 붙인다



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