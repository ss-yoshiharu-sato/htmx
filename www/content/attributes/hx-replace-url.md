+++
title = "hx-replace-url"
+++

`hx-replace-url`属性はブラウザの[ロケーション履歴](https://developer.mozilla.org/en-US/docs/Web/API/History_API)の現在のurlを置き換えることができます。

この属性で取り得る値は以下の通り：

1. `true`を指定すると、ブラウザのナビゲーションバーで取得したURLが置き換えられる。
2. `false`を指定すると、取得したURLが継承によって置換される場合、その置換を無効にする。
3. ロケーションバーに置き換えるURL。これは、[`history.replaceState()`](https://developer.mozilla.org/en-US/docs/Web/API/History/replaceState)に従って、相対的であっても絶対的であっても構いません。

例を挙げよう：

```html
<div hx-get="/account" hx-replace-url="true">
  Go to My Account
</div>
```

これにより、htmxは現在のDOMを`localStorage`にスナップショットし、ブラウザのロケーションバーにあるURL `/account' を置き換える。

別の例を挙げよう：

```html
<div hx-get="/account" hx-replace-url="/account/home">
  Go to My Account
</div>
```

これはブラウザのロケーションバーにあるURL「/account/home」を置き換える。

## メモ

* `hx-replace-url` は継承され、親要素に置くことができる。
* [`HX-Replace-Url`レスポンスヘッダ](@/headers/hx-replace-url.md)も同様の動作をし、この属性をオーバーライドすることができます。
* [`hx-history-elt`属性](@/attributes/hx-history-elt.md)は、履歴キャッシュに保存する要素を変更することができます。
* [`hx-push-url`属性](@/attributes/hx-push-url.md)は類似した、より一般的に使用される属性で、現在の履歴を置き換えるのではなく、新しい履歴エントリを作成します。
