---
layout: post
title: vue에서 fontawesome 사용하기
description: >
    
---

개발 진행중 fontawesome 아이콘을 사용하는 경우가 종종 발생하는데 직접 붙이는 방법도 있지만 이왕 vue를 사용해보는거 제대로 붙여보자 싶어 적용방법을 알아보았다.

## Vue프로젝트에 Font Awesome 설치하기
fontawesome 사이트에서 보면   
~~~
$ npm i --save @fortawesome/fontawesome-svg-core \
  npm i --save @fortawesome/free-solid-svg-icons \
  npm i --save @fortawesome/vue-fontawesome  
~~~
위처럼 설치하라고 나오는데 저렇게 넣었다가 npm이랑 i라는거까지 죄다 설치됬었다...   
본인이 아는 안전한 방법으로 설치하도록 합시다 ㅎㅎ...
~~~
$ npm i --save @fortawesome/fontawesome-svg-core @fortawesome/free-solid-svg-icons @fortawesome/vue-fontawesome  
~~~

위 명령어는 기본으로 필요한 fontawesome-svg-core, vue-fontawesome, 직접적인 아이콘 free-solid-svg-icons를 선택하여 설치하는 경우다. 

패키지 설치시 사용하려는 아이콘이 속한 패키지를 fontawesome 사이트에서 직접 확인하여 알맞는 패키지를 설치하면 된다.

- Solid free: @fortawesome/free-solid-svg-icons
- Regular free: @fortawesome/free-regular-svg-icons
- Brands free: @fortawesome/free-brands-svg-icons

[Fontawesome](https://fontawesome.com/how-to-use/on-the-web/using-with/vuejs) vue 적용 참고페이지  


## 설치 후 적용방법

src/main.js
~~~ javascript
import Vue from 'vue'
import App from './App.vue'

import { library } from '@fortawesome/fontawesome-svg-core'
import { faCoffee } from '@fortawesome/free-solid-svg-icons'
import {} from '@fortawesome/free-regular-svg-icons'
import { faJs, faVuejs } from '@fortawesome/free-brands-svg-icons'
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'

library.add(faCoffee, faJs, faVuejs)

Vue.component('font-awesome-icon', FontAwesomeIcon)

Vue.config.productionTip = false

new Vue({
  render: h => h(App),
}).$mount('#app')
~~~
src/App.vue
~~~ html
<template>
    <div>
        <font-awesome-icon icon="coffee" />
        <font-awesome-icon :icon="['fab', 'js']" />
        <font-awesome-icon :icon="['fab', 'vuejs']" />
    </div>
</template>

<script>
esport default {
    name: 'app'
}
</script>
~~~

위처럼 적용하면 각 아이콘을 확인할 수 있다.   
기본 아이콘이 fas로 적용되는지 prefix가 fas인 아이콘은 명만 넣어도 적용되었지만 fab나 far의 경우는 
~~~html
<font-awesome-icon :icon="['fab', 'js']" />
~~~
이와같은 형식으로 넣어야 적용이 가능하다.



## 설치 및 스타일링 참고자료
https://blog.logrocket.com/full-guide-to-using-font-awesome-icons-in-vue-js-apps-5574c74d9b2d

