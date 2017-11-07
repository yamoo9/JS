# ScrollMagic API

스크롤 매직 인터랙션 자바스크립트 라이브러리.

- [Github 저장소](https://github.com/janpaepke/ScrollMagic)
- [Demo 페이지](http://scrollmagic.io/)
- [Documentation 문서](http://scrollmagic.io/docs/)

## Parallax Scroll Website Design

- [gitman.com](http://gitman.com)
- [primeit.pt](http://primeit.pt)
- [bonnemarque.se](http://bonnemarque.se)
- [oxfordhouse.nl](http://oxfordhouse.nl)
- [details.ch](http://details.ch)
- [exo-skills.com](http://exo-skills.com)
- [deadwater.fr](http://deadwater.fr)
- [dacdavynguyen.com](http://dacdavynguyen.com)
- [phive.pt](http://phive.pt)


---

### ScrollMagic 플러그인 설정

```html
<!-- ScrollMagic 플러그인 -->
<!-- https://cdnjs.cloudflare.com/ajax/libs/ScrollMagic/2.0.5/ScrollMagic.min.js -->
<script src="ScrollMagic.min.js"></script>

<!-- ScrollMagic 디버깅 인디케이터 플러그인 -->
<!-- https://cdnjs.cloudflare.com/ajax/libs/ScrollMagic/2.0.5/plugins/debug.addIndicators.min.js -->
<script src="debug.addIndicators.min.js"></script>
```

---

### [Controller 객체(`{}`) 생성](http://scrollmagic.io/docs/ScrollMagic.Controller.html#constructor)

```js
var controller = new ScrollMagic.Controller();
```

---

### [Scene 객체(`{}`) 생성 / 초기 설정](http://scrollmagic.io/docs/ScrollMagic.Scene.html#constructor)

```js
var scene = new ScrollMagic.Scene({
  'triggerElement': '#scene01' // '씬(Scene)을 설정할 컨테이너 요소 선택자'
});
```

---

### Scene 객체 메소드

- [`.setClassToggle('클래스 속성을 토글 설정 할 요소 선택자', '토글 선택자')`](http://scrollmagic.io/docs/ScrollMagic.Scene.html#setClassToggle)
- [`.addTo( 컨트롤러 )`](http://scrollmagic.io/docs/ScrollMagic.Scene.html#addTo)

```js
scene
  .setClassToggle('#scene01', 'fade-in')
  .addTo( controller );
```

---

### 디버깅 인디케이터 메소드 추가

- `.addIndicators()`

```js
scene
  .setClassToggle('#scene01', 'fade-in')
  .addIndicators() // 플러그인 `debug.addIndicators.min.js` 파일 필요
  .addTo( controller );
```

---

### 디버깅 인디케이터 설정

```js
scene
  .setClassToggle('#scene01', 'fade-in')
  .addIndicators({
    'name': '페이드',
    'indent': 10,
    'colorTigger': '#fe4940',
    'colorStart': '#34c0ff',
    'colorEnd': '#7eff28'
  })
  .addTo( controller );
```

##### [디버깅 인디케이터 옵션](http://scrollmagic.io/docs/debug.addIndicators.html#Scene.addIndicators)

- __`name`__ ─ 트리거 이름
- __`indent`__ ─ 트리거 안쪽으로 이동하는 위치
- __`colorTigger`__ ─ 트리거 색상
- __`colorStart`__ ─ 시작 색상
- __`colorEnd`__ ─ 끝 색상

---

### Scene 지속거리(`duration`) 설정

```js
var scene = new ScrollMagic.Scene({
  'triggerElement': '#scene01',
  'duration': 600, // [End Point] 설정된 클래스 속성이 유지되는 거리 (Start Point 로부터) e.g 420, '100%'
});
```

---

### Scene 트리거 훅(`triggerHook`) 설정

```js
var scene = new ScrollMagic.Scene({
  'triggerElement': '#scene01 img',
  'duration': '90%',
  'triggerHook': 0.9 // 트리거 훅 0 ~ 1 사이 실수 적용 e.g) 0.5, 0.9
});
```

---

### 리버스 애니메이션 컨트롤

- `reverse` ─ 애니메이션을 되돌려 다시 실행할지 유무 (기본 값: `true`)
  - `true`: 애니메이션 여러 번 반복 재생
  - `false`: 애니메이션 1회만 재생

```js
var scene = new ScrollMagic.Scene({
  'triggerElement': '#scene01 img',
  'reverse': false,
  'triggerHook': 0.9
});
```

---

### 멀티 애니메이션 컨트롤

각 요소마다 Scene 객체 생성 및 설정

```js
var scene1 = new ScrollMagic.Scene({
  'triggerElement': '#project01 img',
  'triggerHook': 0.6,
  'reverse': false
})
  .addTo(controller)
  .addIndicators({
    'name': '페이드',
    'indent': 10,
    'colorTigger': '#fe4940',
    'colorStart': '#34c0ff',
    'colorEnd': '#7eff28'
  })
  .setClassToggle('#project01', 'fade-in');

var scene2 = new ScrollMagic.Scene({
  'triggerElement': '#project02 img',
  'triggerHook': 0.6,
  'reverse': false
})
  .addTo(controller)
  .addIndicators({
    'name': '페이드',
    'indent': 10,
    'colorTigger': '#fe4940',
    'colorStart': '#34c0ff',
    'colorEnd': '#7eff28'
  })
  .setClassToggle('#project02', 'fade-in');

var scene3 = new ScrollMagic.Scene({
  'triggerElement': '#project03 img',
  'triggerHook': 0.6,
  'reverse': false
})
  .addTo(controller)
  .addIndicators({
    'name': '페이드',
    'indent': 10,
    'colorTigger': '#fe4940',
    'colorStart': '#34c0ff',
    'colorEnd': '#7eff28'
  })
  .setClassToggle('#project03', 'fade-in');
```

`for`문을 사용하여 반복 구문 처리

```js
var projects = document.querySelectorAll('.project'),
    project = null,
    i = 0,
    l = projects.length

for ( ; i<l; i++ ) {

  project = projects[i];

  var scene = new ScrollMagic.Scene({
    'triggerElement': project.querySelector('img'),
    'triggerHook': 0.6,
    'reverse': false
  });

  scene
    .addTo(controller)
    .addIndicators({
      'name': '페이드',
      'indent': 10,
      'colorTigger': '#fe4940',
      'colorStart': '#34c0ff',
      'colorEnd': '#7eff28'
    })
    .setClassToggle(project, 'fade-in');

}
```

`forEach`문을 사용하여 반복 구문 처리

```js
var projects = Array.from( document.querySelectorAll('.project') ); // Array 화

projects.forEach(function(project, idx){

  var scene = new ScrollMagic.Scene({
    'triggerElement': project.querySelector('img'),
    'triggerHook': 0.6,
    'reverse': false
  });

  scene
    .addTo(controller)
    .addIndicators({
      'name': '페이드',
      'indent': 10,
      'colorTigger': '#fe4940',
      'colorStart': '#34c0ff',
      'colorEnd': '#7eff28'
    })
    .setClassToggle(project, 'fade-in');

});
```

jQuery `.each()`를 사용한 예

```js
var $projects = $('.project');
$.each($projects, function(idx, project){

  var $project = $projects.eq(idx);
  var scene = new ScrollMagic.Scene({
    'triggerElement': $project.find('img')[0],
    'triggerHook': 0.6,
    'reverse': false
  });

  scene
    .addTo(controller)
    .addIndicators({
      'name': '페이드',
      'indent': 10,
      'colorTigger': '#fe4940',
      'colorStart': '#34c0ff',
      'colorEnd': '#7eff28'
    })
    .setClassToggle(project, 'fade-in');

});
```

---

### 핀(Pin, 고정) 설정

#### 고정 예시

1. `duration` 속성이 설정 된 `Scene`의 `pin`은 `duration`에 설정된 픽셀 값만큼 고정(`fixed`)되었다가 고정 해제된다.
1. `duration` 속성이 설정 되지 않은 `Scene`의 `pin`은 `trigger` 위치를 지나도, 뒤 따르는 핀 요소가 없을 경우 고정 해제 되지 않음.

```js
// 핀 설정
var pin = new ScrollMagic.Scene({
  'triggerElement': '#intro',
  'triggerHook': 0,
  'location': '35%'
});

pin
  .setPin('#intro', {'pushFollowers': false})
  .addTo(controller);
```

#### 푸쉬 팔로워 설정

첫 번째 핀은 다음 요소를 아래로 밀어(push down) 냅니다. 그 간격은 `Scene`에 설정된 `duration` 만큼이다.<br>
`pushFollowers` 옵션을 `false`로 설정할 경우 이를 비활성화 할 수 있다.

> `duration` 설정이 0인 `Scene`의 경우, `pushFollowers` 항상 비활성화

---

### 핀(Pin, 고정) → 언핀(UnPin, 비고정) → 핀(Pin, 고정)

- [Simple Pinning DEMO](http://scrollmagic.io/examples/basic/simple_pinning.html)
- [setPin - Scene Control Methods](http://scrollmagic.io/docs/ScrollMagic.Scene.html?#setPin)

```js
var pin1 = new ScrollMagic.Scene({
  'triggerElement': '#intro',
  'triggerHook': 0,
  'location': '35%'
});

pin1
  .setPin('#intro')
  // .setPin('#intro', {'pushFollowers': false})
  .addTo(controller);

// 핀 추가
var pin2 = new ScrollMagic.Scene({
  'triggerElement': '#project01',
  'triggerHook': 0.4
});

pin2
  .setPin('#intro', {'pushFollowers': false})
  .addTo(controller);
```

---

### Parallax

#### CDN 설정

```html
<!-- GreenSock TweenMax -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/1.18.2/TweenMax.min.js"></script>

<!-- ScrollMagic GreenSock Plugin -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/ScrollMagic/2.0.5/plugins/animation.gsap.js"></script>
```

#### 메서드

- `setTween()`

#### 설정 코드

```js
var parallaxTl = new TimelineMax();

parallaxTl
  .from('.content-wrapper', 0.4, { autoAlpha: 0, easse: Power0.easeNone }, 0.4)
  .from('.bcg', 2, { y: '-50%', easse: Power0.easeNone }, 0);

var slideParallaxScene = new ScrollMagic.Scene({
  triggerElement: '.bcg-parallax',
  triggerHook: 1,
  duration: '100%'
})
.setTween(parallaxTl)
.addTo(controller);
```

#### Scroll Magic 영상 강의 링크 (1주일만 공개)

- [ScrollMagic 01](https://youtu.be/ZCBw6cW9Pmc)
- [ScrollMagic 02](https://youtu.be/eY4yolrt_RI)
- [ScrollMagic 03](https://youtu.be/p5pzIG0DOLY)
- [ScrollMagic 04](https://youtu.be/mMg64hyApcw)
- [ScrollMagic 05](https://youtu.be/68uf7MRzea0)
- [ScrollMagic 06](https://youtu.be/5MjCXEz55CU)
