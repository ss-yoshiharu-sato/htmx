+++
title = "hx-push-url"
+++

`hx-push-url`属性はブラウザの[ロケーション履歴](https://developer.mozilla.org/en-US/docs/Web/API/History_API)にURLをプッシュすることができます。
これにより、新しい履歴エントリーが作成され、ブラウザの戻るボタンと進むボタンでナビゲートできるようになります。
htmxは現在のDOMをスナップショットして履歴キャッシュに保存し、ナビゲーション時にこのキャッシュから復元します。

この属性で取り得る値は以下の通り：

1. `true`は、取得したURLを履歴にプッシュする。
2. `false`を指定すると、継承や[`hx-boost`](/attributes/hx-boost)によって取得したURLがプッシュされる場合、プッシュを無効にします。
3. ロケーションバーにプッシュされるURL。これは、[`history.pushState()`](https://developer.mozilla.org/en-US/docs/Web/API/History/pushState)に従って、相対的であっても絶対的であっても構いません。

例を挙げよう：

```html
<div hx-get="/account" hx-push-url="true">
  Go to My Account
</div>
```

これにより、htmxは現在のDOMを`localStorage`にスナップショットし、URL `/account'をブラウザのロケーションバーにプッシュする。

別の例を挙げよう：

```html
<div hx-get="/account" hx-push-url="/account/home">
  Go to My Account
</div>
```

これは、`/account/home'というURLをロケーション履歴にプッシュする。

## メモ

* `hx-push-url` は継承され、親要素に置くことができます。
* [`HX-Push-Url` レスポンスヘッダ](@/headers/hx-push-url.md)も同様の動作をし、この属性をオーバーライドすることができます。
* [`hx-history-elt` 属性](@/attributes/hx-history-elt.md)は、履歴キャッシュに保存する要素を変更することができます。
