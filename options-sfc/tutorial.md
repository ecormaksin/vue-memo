# Vue.jsのチュートリアルでのメモ

## [Declarative Rendering](https://vuejs.org/tutorial/#step-2)

Declarative Rendering: Vueの主要な機能  
JavaScriptの状態に基づいてHTMLを描画する。  
状態が変わるとHTMLも変わる。  

リアクティブな状態を `data` コンポーネント オプションを使って宣言できる。  
オブジェクトを返す関数を指定する。

```vue
export default {
  data() {
    return {
      message: 'Hello World!'
    }
  }
}
```

## Attribute Bindings

Composition APIと同じ。

## [Event Listeners](https://vuejs.org/tutorial/#step-4)

Composition APIとの違い  
- 関数を `methods` オプションに定義する。
- コンポーネント インスタンスに `this` でアクセスする。
