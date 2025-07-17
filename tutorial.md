# Vue.jsのチュートリアルでのメモ

## [Declarative Rendering](https://vuejs.org/tutorial/#step-2)

Declarative Rendering: Vueの主要な機能
JavaScriptの状態に基づいてHTMLを描画する。
状態が変わるとHTMLも変わる。

`reactive()`
  リアクティブな状態を宣言できる。
  `reactive()` で作成されたオブジェクトは、JavaScriptの [プロキシ](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Proxy)
  オブジェクトのみに作用する（配列や `Map`, `Set` のようなビルトイン型も含む ）。

`ref()`
  `reactive()` と違ってどのようなデータ型でも使える。
  `.value` プロパティで内部の値を公開するオブジェクトを作成できる。

`<script setup>` ブロックで宣言されたリアクティブな状態は、テンプレートで直接使える。
口ひげ構文（`mustaches syntax`, `{{  }}`）を使って状態を動的に描画できる。

## [Attribute Bindings](https://vuejs.org/tutorial/#step-3)

`{{ }}` はテキストの埋め込みのみに使える。
属性に動的な値を紐づける場合は、`v-bind` ディレクティブを使う。
短縮記法として `:` のみを記述する。

```vue
<div v-bind:id="dynamicId"></div>
```

```vue
<div :id="dynamicId"></div>
```

## [Event Listeners](https://vuejs.org/tutorial/#step-4)

`v-on` ディレクティブでDOMイベントを監視できる。
短縮記法として `@` のみを記述する。

```vue
<button v-on:click="increment">{{ count }}</button>
```

```vue
<button @click="increment">{{ count }}</button>
```
