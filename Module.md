# Module

## ui module vs feature module
- `:ui-xxx` module
  - 공통 UI 컴포넌트를 가진 모듈
  - 특정 도메인을 의존하지 않는다
  - ex. `:ui-image`, `:ui-carNumber`
- `:feature-xxx` module
  - feature에 대한 UI, ViewModel을 가진 모듈
  - 특정 도메인을 의존한다
  - ex. `:feature-carHistory`, `:feature-market`