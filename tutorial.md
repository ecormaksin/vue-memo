# Vue.jsのチュートリアルでのメモ

## [Declarative Rendering](https://vuejs.org/tutorial/#step-2)

Declarative Rendering: Vueの主要な機能  
JavaScriptの状態に基づいてHTMLを描画する。  
状態が変わるとHTMLも変わる。  
詳細は [別ページ](https://vuejs.org/guide/essentials/reactivity-fundamentals.html)

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
詳細は [別ページ](https://vuejs.org/guide/essentials/template-syntax.html)

```vue
<div v-bind:id="dynamicId"></div>
```

```vue
<div :id="dynamicId"></div>
```

## [Event Listeners](https://vuejs.org/tutorial/#step-4)

`v-on` ディレクティブでDOMイベントを監視できる。  
短縮記法として `@` のみを記述する。  
詳細は [別ページ](https://vuejs.org/guide/essentials/event-handling.html)

```vue
<button v-on:click="increment">{{ count }}</button>
```

```vue
<button @click="increment">{{ count }}</button>
```

## [Form Bindings](https://vuejs.org/tutorial/#step-5)

双方向バインディングのディレクティブ。  
イベント ハンドラーが不要になる。  
テキスト ボックスだけでなく、チェックボックス・ラジオ ボタン・セレクト ドロップダウンなどの他の入力型でも機能する。  
詳細は [別ページ](https://vuejs.org/guide/essentials/forms.html)

```vue
<input v-model="text">
```

## [Conditional Rendering](https://vuejs.org/tutorial/#step-6)

条件付きレンダリング
`v-else`, `v-else-if` も組み合わせて使う。
詳細は [別ページ](https://vuejs.org/guide/essentials/conditional.html)

```vue
<h1 v-if="awesome">Vue is awesome!</h1>
```

## [List Rendering](https://vuejs.org/tutorial/#step-7)

`v-for`: リストの要素を描画  
[特殊な `key` 属性](https://vuejs.org/api/built-in-special-attributes.html#key) をオブジェクトの `id` と紐づけることで、VueのモデルとHTMLの要素が連動する。  
詳細は [別ページ](https://vuejs.org/guide/essentials/list.html)

```vue<ul>
  <li v-for="todo in todos" :key="todo.id">
    {{ todo.text }}
  </li>
</ul>
```

リストを更新する2つの方法

1. [mutating methods](https://stackoverflow.com/questions/9009879/which-javascript-array-functions-are-mutating) (変更メソッド) の呼び出し

    ```javascript
    todos.value.push(newTodo)
    ```

2. 新しい配列で置き換える

    ```javascript
    todos.value = todos.value.filter(/* ... */)
    ```

## [Computed Property](https://vuejs.org/tutorial/#step-8)

[`computed()`](https://vuejs.org/guide/essentials/computed.html) により、他のリアクティブなデータ ソースに基づいて、対象の値を計算した参照を生成する。

