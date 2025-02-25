---
category: Sensors
---

# useIntersectionObserver

> Detects that a target element's visibility.

## Usage

```html
<div ref="target">
  <h1>Hello world</h1>
</div>
```

```js
import { ref } from 'vue'
import { useIntersectionObserver } from '@vueuse/core'

export default {
  setup() {
    const target = ref(null)
    const targetIsVisible = ref(false)

    const { stop } = useIntersectionObserver(
      target,
      ([{ isIntersecting }], observerElement) => {
        targetIsVisible.value = isIntersecting
      },
    )

    return {
      target,
      targetIsVisible,
    }
  },
}
```

[IntersectionObserver MDN](https://developer.mozilla.org/en-US/docs/Web/API/IntersectionObserver/IntersectionObserver)


<!--FOOTER_STARTS-->
## Type Declarations

```typescript
export interface IntersectionObserverOptions extends ConfigurableWindow {
  /**
   * The Element or Document whose bounds are used as the bounding box when testing for intersection.
   */
  root?: MaybeRef<Element | null | undefined>
  /**
   * A string which specifies a set of offsets to add to the root's bounding_box when calculating intersections.
   */
  rootMargin?: string
  /**
   * Either a single number or an array of numbers between 0.0 and 1.
   */
  threshold?: number | number[]
}
/**
 * Detects that a target element's visibility.
 *
 * @see   {@link https://vueuse.js.org/useIntersectionObserver}
 * @param target
 * @param callback
 * @param options
 */
export declare function useIntersectionObserver(
  target: MaybeRef<Element | null | undefined>,
  callback: IntersectionObserverCallback,
  options?: IntersectionObserverOptions
): {
  isSupported: boolean | undefined
  stop: () => void
}
```

## Source

[Source](https://github.com/antfu/vueuse/blob/master/packages/core/useIntersectionObserver/index.ts) • [Demo](https://github.com/antfu/vueuse/blob/master/packages/core/useIntersectionObserver/demo.vue) • [Docs](https://github.com/antfu/vueuse/blob/master/packages/core/useIntersectionObserver/index.md)


<!--FOOTER_ENDS-->