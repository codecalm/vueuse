# @vueuse/rxjs

[![NPM version](https://img.shields.io/npm/v/@vueuse/rxjs?color=a1b858)](https://www.npmjs.com/package/@vueuse/rxjs)

> This is an add-on of [VueUse](https://github.com/antfu), enables of a natural way the use of RxJS.

## 📦 Install

<pre class='language-bash'>
npm i <b>@vueuse/rxjs</b> rxjs
</pre>

## ⚡ Functions

<!--GENERATED LIST, DO NOT MODIFY MANUALLY-->
<!--FUNCTIONS_LIST_STARTS-->
  - [`from`](https://vueuse.js.org/rxjs/from/) — two wrappers around of the original functions to allow use ref objects
  - [`toObserver`](https://vueuse.js.org/rxjs/toObserver/) — sugar function to convert a ref in an observer
  - [`useObservable`](https://vueuse.js.org/rxjs/useObservable/) — use an Observable
  - [`useSubscription`](https://vueuse.js.org/rxjs/useSubscription/) — uses subscriptions without worry about unsubscribing to it or memory leaks


<!--FUNCTIONS_LIST_ENDS-->

## 📄 Example

```ts
import { fromEvent, from, useObservable } from '@vueuse/rxjs'
import { ref } from 'vue'
import { of, forkJoin } from 'rxjs'
import { ajax } from 'rxjs/ajax'
import { take, mergeMap, concatAll, pluck, map, scan } from 'rxjs/operators'

const BASE_URL = 'https://jsonplaceholder.typicode.com'
const button = ref<HTMLButtonElement>(null)

const posts = useObservable(
  fromEvent(button, 'click').pipe(
    mergeMap(() => ajax.getJSON(`${BASE_URL}/posts`).pipe(
      concatAll(),
      take(4),
      mergeMap(({ id, userId, title }) => forkJoin({
        id: of(id),
        comments: ajax.getJSON(`${BASE_URL}/posts/${id}/comments`).pipe(
          map(comments => comments.length)
        ),
        username: ajax.getJSON(`${BASE_URL}/users/${userId}`).pipe(
          pluck('username')
        )
      }), 2),
      scan((acc, curr) => [...acc, curr], [])
    ))
  )
)
```

## 📄 License

[MIT License](https://github.com/antfu/vueuse/blob/master/LICENSE) © 2019-PRESENT [Anthony Fu](https://github.com/antfu)
