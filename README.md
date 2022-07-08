<img src="https://img.shields.io/badge/Netlify-00C7B7?style=for-the-badge&logo=netlify&logoColor=white">

두 개의 브랜치 생성, netlify를 통해 버전 관리된 제품을 배포할 수 있도록 세팅

* [master 브랜치](https://github.com/iamoki/starbusks-clone/tree/master)
* [signin 브랜치](https://github.com/iamoki/starbusks-clone/tree/signin)

[완성페이지바로가기](https://sunny-trifle-6ce7f9.netlify.app/)🏃‍♂️🏃‍♂️🏃‍♂️

# Starbucks 랜딩페이지 클론코딩 라이브러리 정리 🛠

## 🪛 **GSAP & ScrollToPlugin**
>### 요소들의 애니메이션 처리를 위해 사용. & 스크롤애니메이션을 위해 사용.

~~~javascript
// 요소 애니메이션
function floatingObject(selector, delay, size) {
    // gsap.to(요소, 지속시간, 옵션);
    gsap.to(
        selector, // 선택자
        random(1.5, 2.5), // 애니메이션 동작 시간
        { // 옵션들
            y: size,
            repeat: -1,
            yoyo: true,
            ease: Power1.easeInOut,
            delay: random(0, delay),
        }
    );
}
floatingObject('.floating1', 1, 15);
floatingObject('.floating2', .5, 15);
floatingObject('.floating3', 1.5, 20);
~~~

~~~javascript
// to-top선택시 페이지 최상단 이동
toTopEl.addEventListener('click', function() {
    gsap.to(window, .7, {
        scrollTo: 0,
    });
});
~~~
---
## 🪛 **Lodash**
>### 스크롤 할 때마다 불필요하게 이벤트가 발생하는 것을 방지하고자 지정한 시간마다 이벤트가 실행되도록 사용.(프로젝트의 규모가 클시 성능 개선에 유용)

~~~javascript
window.addEventListener('scroll', _.throttle(function () {
    if(window.scrollY > 500) {
        // gsap.to(요소, 지속시간, 옵션);
        // 배지 숨기기
        gsap.to(badgeEl, .6, {
            opacity: 0,
            display: 'none'
        });
        // to-top버튼 보이기
        gsap.to(toTopEl, .2, {
            x: 0,
            opacity: 1,
        });
    } else {
        // 배지 보이기
        gsap.to(badgeEl, .6, {
            opacity: 1,
            display: 'block'
        });
        // to-top버튼 숨기기
        gsap.to(toTopEl, .2, {
            x: 100,
            opacity: 0,
        });
    }
}, 300));
// _.throttle(함수,시간)
~~~
---
## 🪛 **Swiper**
>### 이미지 슬라이드를 편리하게 처리하고자 사용.
~~~javascript
new Swiper('.promotion .swiper', {
    slidesPerView: 3, // 슬라이드에 한번에 보여줄 개수
    spaceBetween: 10, // 슬라이드 사이 여백
    centeredSlides: true, // 1번 슬라이드가 가운데로 보여지기
    loop: true,
    // autoplay: {
    //     delay: 5000
    // },
    pagination: {
        el: '.promotion .swiper-pagination', // 페이지번호 요소 선택
        clickable: true, // 사용자의 페이지 번호 요소 제어
    },
    navigation: {
        prevEl: '.promotion .swiper-prev',
        nextEl: '.promotion .swiper-next',
    }
});
~~~
---
## 🪛 **ScrollMagic**
>### 스크롤과 요소의 상호작용을 위해 사용.
~~~javascript
const spyEls = document.querySelectorAll('section.scroll-spy');
spyEls.forEach(function(spyEl) {
    new ScrollMagic
        .Scene({
            triggerElement: spyEl, // 보여짐 여부를 감시할 요소를 지정
            triggerHook: .8,
        })
        .setClassToggle(spyEl, 'show')
        .addTo(new ScrollMagic.Controller());
});
~~~
---
## 🪛 **Youtube API**
>### API를 활용한 영상제어를 하기 위해 사용.
~~~javascript
var tag = document.createElement('script');
tag.src = "https://www.youtube.com/iframe_api";
var firstScriptTag = document.getElementsByTagName('script')[0];
firstScriptTag.parentNode.insertBefore(tag, firstScriptTag);

function onYouTubePlayerAPIReady() {
    new YT.Player('player', {
        videoId: 'An6LvWQuj_8', // 재생할 유튜브 영상 ID
        playerVars: {
            autoplay: true, // 자동 재생 유무
            loop: true, // 반복 재생 유무
            playlist: 'An6LvWQuj_8' // 반복 재생할 유튜브 영상 ID 목록
        },
        events: {
            // 영상이 준비되었을 때,
            onReady: function (event) {
                event.target.mute(); // 음소거!
            }
        }
    });
}
~~~
