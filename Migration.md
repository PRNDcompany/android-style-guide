# Migration
유지보수를 진행하며 마이그레이션이 필요한 상황에 대한 컨벤션을 정의

---


### A/B 테스트
A/B 테스트가 확정된 피쳐에 대해 `A` `B`를 아래와 같이 정의한다.
- `A` : 대조군, 기존 코드 
- `B` : 실험군, 새로 추가하는 코드

작업을 시작하기 전 `A`안의 코드를 레거시로 변경한다.
- Kotlin : LegacyXXX
- Resource : xxx_legacy
```xml
SampleActivity.kt --> LegacySampleActivity.kt
activity_sample.xml --> activity_sample_legacy.xml
```

새로 추가되는 `B`안의 코드를 원래 `A`안의 이름으로 추가한다.
```
// B 안
SampleActivity.kt
activity_sample.xml

// A 안
LegacySampleActivity.kt
activity_sample_legacy.xml
```

이후 B안이 확정되면 Legacy 코드를 삭제하는 작업을 진행한다. 
- B안(개선안)이 상대적으로 확정될 가능성이 높다.
- 이 방법을 통해 B안의 코드는 추가적인 수정을 하지 않아도 된다.
