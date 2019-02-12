# Resource

## Layout
- `<WHAT>_<WHERE>`

### WHAT
| Prefix | 설명 |
| ------------- | ------------- |
| `activity_` | Activity에서 쓰이는 layout |
| `fragment_` | Fragment에서 쓰이는 layout |
| `dialog_` | Dialog에서 쓰이는 layout |
| `view_` | CustomView에서 쓰이는 layout |
| `item_` | RecyclerView, GridView, ListView등에서 ViewHolder에 쓰이는 layout |
| `layout_` | `<include/>`로 재사용되는 공통의 layout |
### 예시
- `activity_main`: MainActivity의 layout
- `fragment_request`: RequestFragment의 layout
- `dialog_contact`: 문의안내 Dialog의 layout
- `view_rating`: 커스텀으로 만든 RatingView의 layout
- `item_my_car`: 내차량 목록에서 사용되는 각각의 item의 layout
- `layout_dealer_review`: 재사용되는 딜러리뷰 layout

## ID
- `<WHAT>_<DESCRIPTION>`
- View의 대문자를 축약하여 `<WHAT>`의 Prefix로 사용한다.
- 아래 이름규칙을 적용한다.
1. Android의 View는 CamelCase의 대문자를 축약한 형태로 정한다.
</br>: `TextView -> tv_`
2. 만약 View의 이름이 Space, Switch와 같이 1개의 대문자만 존재한다면 모두 소문자인 아이디로 정한다.
</br>: `Switch -> switch_`
3. CustomView는 전체View의 이름을 snake case이름으로 정한다.
</br>: `MyCustomView -> my_custom_view`
</br>(만약 1개의 xml에 같은 여러 CustomView가 존재한다면 `<WHAT>_<DESCRIPTION>`의 형태로 정한다.)
4. 아래표에 해당 View의 Prefix가 정의되어 있지 않다면 팀에서 상의해서 이름을 정한뒤 추가한다.


### WHAT
| View | Prefix |
| ------------- | ------------- |
| TextView | `tv_` |
| ImageView | `iv_` |
| CheckBox | `cb_` |
| RecyclerView | `rv_` |
| EditText | `et_` |
| ProgressBar | `pb_` |
| FrameLayout | `fl_` |
| NestedScrollView | `nsv_` |
| Space | `space_` |
| Switch | `switch` |
| AbcDeFgh | `adf_` |
| Abcdef | `abcdef_` |
| MyCustomView | `my_custom_view` |
| YourView | `your_view` |


### 기타
- 해당 View를 특정기능과 상관없이 `VISIBLE/GONE`등의 View의 용도로 사용한다면 `view_xxx`로 사용하는것도 허용한다.
- 버튼기능을 위한 View는 ImageView, TextView로만 사용한다.
(Button, ImageButton은 존재의 의미가 없음)

### 예시
- `iv_close`: 닫기 ImageView
- `tv_select`: 선택 TextView
- `rv_car_list`: 자동차 목록 RecyclerView
- `view_etc_model`: 기타 모델 화면 LinearLayout

## Drawable
- `<WHAT>(_<WHERE>)_<DESCRIPTION>(_<SIZE>)`
- 이미지가 여러군데에서 활용될 경우, `<WHERE>`는 생략 가능하다.
- 이미지의 크기가 1개밖에 없는 경우, `<SIZE>`는 생략 가능하다.

### What
| Prefix | 설명 |
| ------------- | ------------- |
| `btn_` | 버튼으로 쓰이는 이미지 |
| `ic_` | 버튼이 아닌 화면에 보여지는 이미지 |
| `bg_` | 버튼이 아닌 화면에 보여지는 이미지 |
| `img_` | 실제사진이거나 아이콘형태가 아닌 일러스트형태의 이미지 |
| `div_` | divider로 활용되는 이미지 |

### Selector
- 배경이나 버튼에서 View의 상태에 따라서 drawable이 변해야 하는 경우에 대한 이름은 아래와 같다.

| 상태 | Suffix |
| ------------- | ------------- |
| Normal | `_normal` |
| Pressed | `_pressed` |
| Focused | `_focused` |
| Disabled | `_disabled` |
| Selected | `_selected` |

### Background
- 배경색이 pressed상태에 따라서 white -> sky_blue로 변하는 경우는 `bg_white_to_sky_blue.xml`로 한다.
- 배경이 white색의 24dp로 테두리를 그리는 경우는 `bg_white_radius_24dp.xml`로 한다.
- 배경이 투명하며 배경의 선만을 sky_blue색의 8dp로 테두리를 그리는 경우는 `bg_stroke_sky_blue_radius_8dp.xml`로 한다.


### 기타

- `img_xxx`의 경우 파일의 크기가 큰경우가 많으므로 [tinypng](https://tinypng.com/)에서 파일크기를 줄인뒤에 추가 해주어야 한다.


### 예시
- `btn_call_normal.png`: 전화걸기 버튼 이미지
- `btn_call_pressed.png`: 전화걸기 버튼 눌렸을때의 이미지
- `btn_call.xml`: 전화걸기 버튼 이미지의 selector xml
- `ic_dealer_gift.png`: 딜러가 보내준 기프티콘을 보여줄때 표시되는 이미지
- `img_splash_chart.png`: 스플래시 화면에서 보여지는 차트 이미지
-

## Dimension
- `<WHERE>_<DESCRIPTION>_<WHAT>`

### Margin/Padding
- 대부분의 `margin/padding`은 아래 정의된 `space_xxx`로만 사용되도록 한다.
```xml
<dimen name="space_x_small">8dp</dimen>  
<dimen name="space_small">12dp</dimen>  
<dimen name="space_median">16dp</dimen>  
<dimen name="space_s_large">18dp</dimen>  
<dimen name="space_large">20dp</dimen>  
<dimen name="space_x_large">24dp</dimen>
```
- 그외에 특정 화면에서 위의 값을 따르지 않는경우, `<WHERE>_<DESCRIPTION>_<WHAT>`의 규칙으로 만든다.
```xml
<dimen name="register_car_item_car_model_start_padding">40dp</dimen>  
<dimen name="register_car_item_grade_start_padding">56dp</dimen>  
<dimen name="register_car_item_car_detail_start_padding">72dp</dimen>
```
- 2번이상 쓰이는경우는 dimen에 정의해주는 것을 강제하고 1번만 쓰이는경우에는 xml코드에 넣어도 괜찮은것으로 한다.

### Height/Size
- 높이만 지정할때는 `height`, 1:1 비율로 같은 값이 들어갈때는 `size`로 한다.
```xml
<dimen name="toolbar_height">56dp</dimen>
<dimen name="register_input_view_default_height">280dp</dimen>  
<dimen name="register_input_view_collapse_height">200dp</dimen>
<dimen name="dealer_profile_image_size">48dp</dimen>
```


## String
-  `<WHERE>_<DESCRIPTION>`
- 특정화면에서 쓰이는 텍스트 아니라 여러군데에서 공통으로 재사용될 텍스트라면 `all_<DESCRIPTION>`로 이름을 짓는다

### 예시
- `permission_dialog_camera_title`: 카메라권한을 요구하는 Dialog의 제목
-  `permission_dialog_camera_description`: 카메라권한을 요구하는 Dialog의 설명내용
- `all_yes`: 네
- `all_ok_understand`: 여러 Dialog에서 `네, 알겠습니다`로 쓰이는 공통의 텍스트

### 문단
- 문단형태의 긴 문자열로 개행(`\n`)이 필요한 경우, `\n`을 다음줄의 앞에 쓴다.
```xml
 <string name="sample">문단 첫번째줄
        \n문단 두번째줄
        \n문단 세번째줄</string>
````


## Theme/Style
- Theme는 `theme.xml`, Style은 `style.xml`에 추가한다.
- 1번만 쓰이는 경우에는 style을 만들지 않는다.
(단, 앞으로 재사용될 가능성이 높은 경우에는 가능)
- 모든 style은 parent를 갖는다.

### Naming
- style의 이름은 parent의 이름패턴과 맞춘다
```xml
<style name=”Widget.HeyDealer.Button” parent=”@style/Widget.AppCompat.Button”>
...
</style>
```
- parent에서 일부 내용만 수정하고자 하는경우, parent이름 뒤에 달라진 내용의 내용을 추가해준다
```xml
<style name="Theme.HeyDealer.Transparent" parent="Theme.HeyDealer">
...
</style>
```

## Attribute
- Attribute이름은 `camelCase`로 한다.
```xml
<attr name="numStars" format="integer" />
```

- 기존에 정의되어있는 `android:xxx`와 같은 동작을 유도하는 경우, 이 tag를 재사용한다.
```xml
<declare-styleable name="SpannedGridLayoutManager">  
 <attr name="android:orientation" />  
...
</declare-styleable>
```

## 기타
- `android:xxxLeft/android:xxxRight` 대신 `android:xxxStart/android:xxxEnd`로 사용한다.(기타 Left/Right로 사용하는 부분 모두)
