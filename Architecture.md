# Architecture
- 코드의 Architecture는 MVP를 사용한다.


## Presenter
- Presenter클래스에는 Android관련 코드를 넣지않는다
: `android.aa.bb` 같은 코드들이 Presenter에 들어가있는지 확인
```
import android.content.Intent;
import android.net.Uri;
import android.support.v4.widget.NestedScrollView;
```
