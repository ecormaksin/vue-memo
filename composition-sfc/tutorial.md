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

## [Lifecycle and Template Refs](https://vuejs.org/tutorial/#step-9)

[特殊な `ref` 属性](https://vuejs.org/api/built-in-special-attributes.html#ref)  
テンプレート内で要素の参照を指定する。  

```vue
<p ref="pElementRef">hello</p>
```

参照へアクセスするために、同じ名前で参照を宣言する必要がある。  

```vue
const pElementRef = ref(null)
```

`null` で初期化されているのは、 `<script setup>` が実行された時に要素がまだ存在していないため。  
テンプレートの参照は、要素が **マウントされた後** にのみアクセス可能になる。  
マウント後にコードを実行するために、 `onMounted()` を使う。

```vue
import { onMounted } from 'vue'

onMounted(() => {
  // component is now mounted.
})
```

この仕組みをライフサイクル フック（lifecycle hook）と呼ぶ。  
`onUpdated` や `onUnmounted` のような他のフックもある。  
詳細は [別ページ](https://vuejs.org/guide/essentials/lifecycle.html#lifecycle-diagram)

## [Watchers](https://vuejs.org/tutorial/#step-10)

副作用のある処理をリアクティブに実行する必要がある場合に、ウォッチャー(watcher)を使う。  
詳細は [別ページ](https://vuejs.org/guide/essentials/watchers.html)

## [Components](https://vuejs.org/tutorial/#step-11)

Vueのアプリケーションは、典型的に入れ子になった複数のコンポーネントで作成される。  
親のコンポーネントは、他のコンポーネントをテンプレート内で子のコンポーネントとしてレンダリングされる。  
子のコンポーネントを使うには、まずインポートする必要がある。  

```vue
import ChildComp from './ChildComp.vue'
```

そして、テンプレート内で対象のコンポーネントを次のように使える。

```vue
<ChildComp />
```

## [Props](https://vuejs.org/tutorial/#step-12)

子のコンポーネントは、**props**を介して親から入力を受け取ることができる。  
まず、子のコンポーネント側で、受け取るpropsを宣言する必要がある。

```vue:ChildComp.vue
<script setup>
const props = defineProps({
  msg: String
})
</script>
```

`defineProps()` はコンパイル時のマクロなので、インポートは不要。  
`defineProps()` の戻り値オブジェクトへJavaScriptを介してアクセスできる。

親コンポーネントは、子コンポーネントへ属性のようにpropsを渡せる。  
動的な値を渡すためには、`v-bind`構文を使える。

```vue
<ChildComp :msg="greeting" />
```

## [Emits](https://vuejs.org/tutorial/#step-13)

propsを受け取るのに加えて、子のコンポーネントは親へイベントを発行できる。  

```vue:ChildComp.vue
<script setup>
// declare emitted events
const emit = defineEmits(['response'])

// emit with argument
emit('response', 'hello from child')
</script>
```

`emit()` の第1引数はイベント名  
追加の引数はイベント リスナーへ渡される。  

親のコンポーネントは、子のコンポーネントが発行したイベントを `v-on` ディレクティブを使って監視できる。ハンドラーは、子が発行したイベントから追加の引数を受け取り、ローカルの状態変数へ割り当てる。

```vue
<ChildComp @response="(msg) => childMsg = msg" />
```

## [Slots](https://vuejs.org/tutorial/#step-14)

propsでデータを受け渡せることに加えて、親のコンポーネントから子のコンポーネントへ **slots** を介してテンプレートの断片を渡せる。  

```vue
<ChildComp>
  This is some slot content!
</ChildComp>
```

子のコンポーネントでは、 `<slot/>` 要素を通じて親のコンポーネントからの内容をレンダリングする。

