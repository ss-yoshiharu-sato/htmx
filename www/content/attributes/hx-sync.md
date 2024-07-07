+++
title = "hx-sync"
+++

`hx-sync` 属性を使うと、複数の要素間で AJAX リクエストを同期させることができます。

`hx-sync` 属性は同期する要素を示す CSS セレクタで構成され、その後にコロンが続き、オプションで同期戦略を指定します。利用可能なストラテジーは以下の通りです：

* `drop` - 既存のリクエストが飛行中であれば、このリクエストを落とす (無視する) (デフォルト)
* `abort` - 既存のリクエストが飛行中であれば、このリクエストをドロップ（無視）し、そうでない場合は、飛行中に別のリクエストが発生した場合、このリクエストを*中止*する。
* `replace` - 現在のリクエストがあれば中止し、このリクエストに置き換える。
* `queue` - このリクエストを、与えられたエレメントに関連付けられたリクエストキューに入れる。

`queue`修飾子には、どのようにキューに入れるかを示す追加の引数を取ることができる：

* `queue first` - リクエストの飛行中に表示される最初のリクエストをキューに入れる
* `queue last` - リクエストの飛行中に最後に表示されたリクエストをキューに入れる
* `queue all` - リクエストの飛行中に表示されるすべてのリクエストをキューに入れる

## メモ

* `hx-sync` は継承され、親要素に置くことができる。

この例では、フォームの送信リクエストと個々の入力の検証リクエストの間の競合状態を解決します。通常、`hx-sync` を使用しないと、入力フォームに入力してすぐに送信すると、`/validate` と `/store` への2つのリクエストが並行して実行されます。`hx-sync="closeform:abort"`を入力に使用すると、フォーム上のリクエストを監視し、フォームリクエストが存在するか、入力リクエストが処理中に開始された場合、入力のリクエストを中断します。

```html
<form hx-post="/store">
    <input id="title" name="title" type="text" 
        hx-post="/validate" 
        hx-trigger="change"
        hx-sync="closest form:abort">
    <button type="submit">Submit</button>
</form>
```

送信リクエストよりもバリデーションリクエストを優先させたい場合は、`drop` 戦略を使用します。この例では、バリデーションリクエストを送信リクエストよりも優先させ、バリデーションリクエストが送信中である場合はフォームを送信できないようにします。

```html
<form hx-post="/store">
    <input id="title" name="title" type="text" 
        hx-post="/validate" 
        hx-trigger="change"
        hx-sync="closest form:drop"
    >
    <button type="submit">Submit</button>
</form>
```

多くの入力を含むフォームを扱う場合、フォームタグの hx-sync `replace` ストラテジーを使って、すべての入力検証リクエストよりも送信リクエストを優先させることができます。これにより、実行中のバリデーションリクエストはすべてキャンセルされ、`hx-post="/store"`リクエストだけが発行されます。送信リクエストを中止して既存のバリデーションリクエストを優先したい場合は、フォームタグの `hx-sync="this:abort"` 戦略を使用します。

```html
<form hx-post="/store" hx-sync="this:replace">
    <input id="title" name="title" type="text" hx-post="/validate" hx-trigger="change" />
    <button type="submit">Submit</button>
</form>
```

アクティブ検索機能を実装する場合、hx-trigger 属性の `delay` 修飾子を使用することで、ユーザの入力をデバウンスし、ユーザがタイプしている間に複数のリクエストが行われるのを避けることができます。しかし、一度リクエストが行われると、ユーザーが再び入力を始めると、前のリクエストが処理を終えていなくても新しいリクエストが始まります。この例では、進行中のリクエストはすべてキャンセルされ、最後のリクエストのみが使用されます。検索入力がターゲット内に含まれている場合、このように `hx-sync` を使用することで、ユーザーが入力中に入力が置き換えられてしまう可能性を減らすこともできます。

```html
<input type="search" 
    hx-get="/search" 
    hx-trigger="keyup changed delay:500ms, search" 
    hx-target="#search-results"
    hx-sync="this:replace">
```
