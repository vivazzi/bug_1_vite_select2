# bug 1: usage jQuery as ES module with Vue 3 + Vite + Select2

This app is represention of bugs (see pull request https://github.com/godbasin/vue-select2/pull/61)

```
1. index.813ae237.js:1 ReferenceError: $ is not defined

2. Uncaught SyntaxError: The requested module '/node_modules/.pnpm/jquery@3.6.0/node_modules/jquery/dist/jquery.js?v=d0d02272' does not provide an export named 'default'
```

## Running

1. Clone this repo
2. `cd vite_select2`
3. `pnpm install`
4. `pnpm run dev` or `pnpm run build` and `pnpm run preview`

> Note: folder `bug dist` has build result (`pnpm run build`) on my machine. Maybe it will be useful for comparison.

## Bug description

In production code I see that jQuery was loaded to index.813ae237.js, but it seems component did not apply `window.jQuery = window.$ = jQuery;`. 


My all scenarios of running Select2:

1. If `Select.vue` has `import $ from 'jquery';` on line 8 (as in repo owner):

- 1.1. if I run `vite dev`, then I get error:

```
Uncaught SyntaxError: The requested module '/node_modules/.pnpm/jquery@3.6.0/node_modules/jquery/dist/jquery.js?v=d0d02272' does not provide an export named 'default'
```

- 1.2. if I run `vite build` and `vite preview`, then I get error:

```
index.6b32860a.js:1 TypeError: Bc(...).find(...).select2 is not a function
    at Proxy.mounted (index.6b32860a.js:31:4388)
    at en (index.6b32860a.js:1:12559)
    at St (index.6b32860a.js:1:12638)
    at Array.r.__weh.r.__weh (index.6b32860a.js:1:22610)
    at Lo (index.6b32860a.js:1:14082)
    at et (index.6b32860a.js:1:41980)
    at mount (index.6b32860a.js:1:31893)
    at Object.r.mount (index.6b32860a.js:1:53415)
    at index.6b32860a.js:31:5272
```

2. If `Select.vue` has `import * as jQuery from 'jquery';` on line 8 (as in my pull request):

- 2.1. if I run `vite dev`, my code works good.

- 2.2. if I run `vite build` and `vite preview`, then I get error:

```
index.813ae237.js:1 ReferenceError: $ is not defined
    at Proxy.mounted (index.813ae237.js:31:4347)
    at en (index.813ae237.js:1:12559)
    at St (index.813ae237.js:1:12638)
    at Array.Mr.r.__weh.r.__weh (index.813ae237.js:1:22610)
    at Lo (index.813ae237.js:1:14082)
    at et (index.813ae237.js:1:41980)
    at mount (index.813ae237.js:1:31893)
    at Object.r.mount (index.813ae237.js:1:53415)
    at index.813ae237.js:31:5271
```

AI try different ways to fix this bug, but all my attempts are failed. Has anybody ideas to decide this problem?

## Different info

About this problem: https://github.com/jquery/jquery/issues/4592