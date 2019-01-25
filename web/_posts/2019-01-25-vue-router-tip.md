---
layout: post
title: Vue.js에서 vue-router
description: >
    vue-router 사용법 및 팁
---

## 기본 사용법
~~~ js
import Vue from 'vue';
import VueRouter from 'vue-router';
import NewsView from '../views/NewsView.vue';

Vue.use(VueRouter);

export const router = new VueRouter({
    mode: 'history', // 이부분을 history로 처리해야 url로 인식이 되며 이걸 빼면 hash처리 된다
    routes: [
        // 여기에 원하는 방식의 url 과 페이지를 정의한다.
        { path: '/news', component: NewsView }
    ],
});
~~~

위에 mode: 'history' 는 그냥 기본으로 가져간다고 생각하면 될것 같다.


## url에서 값 받아오기
~~~ js
export const router = new VueRouter({
    mode: 'history',
    routes: [
        { path:'/news/:page', component: NewsView }
    ],
});
~~~
위와 같이 routes에서 처리해주면 NewsView라고 정의해둔 컴포넌트에서 this.$route.params.page로 값을 가져올 수 있다.


## url에서 값 받아올 때 제한두기

정해진 정해진 url이외의 페이지는 접근 불가능하도록 처리하기 위해 패턴을 적용할 수 있다.
~~~ js
export const router = new VueRouter({
    mode: 'history',
    routes: [
        { path:'/news/:page(10|[0-9])', component: NewsView }
    ],
});
~~~
위 코드를 작성할때 페이지가 10으로 제한되어있는 api를 사용중이어서 위와같은 코드를 적용했다.
하지만 이렇게만 적용할 경우 문제가 될수있다.
없는 페이지를 호출할 시 404 not found 페이지가 아닌 그냥 빈 페이지가 노출된다.


## NotFound 페이지 처리하기
~~~ js
...
import NotFound from '../views/NotFound.vue';

export const router = new VueRouter({
    mode: 'history',
    routes: [
        { path: '*', component: NotFound }
    ],
});
~~~

없는 페이지를 호출할때 미리 작성해둔 NotFound 뷰를 호출하도록 위와같이 설정하면 된다.


[vue-router 참고자료](https://router.vuejs.org/kr/)