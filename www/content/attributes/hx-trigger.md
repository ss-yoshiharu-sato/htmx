+++
title = "hx-trigger"
+++

`hx-trigger`属性はAJAXリクエストのトリガーを指定します。トリガーの値は以下のいずれかです：

* イベント名（"click "や "my-custom-event "など）の後に、イベントフィルタとイベント修飾子のセットを続けます。
* ポーリング定義は、`every <タイミング宣言>`という形式
* イベントのカンマ区切りのリスト

### スタンダード・イベント

`click`のような標準的なイベントをトリガーとして指定することができます：

```html
<div hx-get="/clicked" hx-trigger="click">Click Me</div>
```

#### 標準イベントフィルター

イベントをフィルタリングするには、イベント名の後に角括弧でブーリアン・ジャバスクリプト式を囲みます。この式が `true` と評価されるとイベントが発生し、そうでなければ無視されます。

```html
<div hx-get="/clicked" hx-trigger="click[ctrlKey]">Control Click Me</div>
```

このイベントは、`event.ctrlKey`プロパティがtrueに設定されたクリックイベントがトリガーされた場合に発生します。

条件は、グローバル関数や状態を参照することもできます。

```html
<div hx-get="/clicked" hx-trigger="click[checkGlobalState()]">Control Click Me</div>
```

また、標準的なjavascriptの構文を使って組み合わせることもできる。

```html
<div hx-get="/clicked" hx-trigger="click[ctrlKey&&shiftKey]">Control-Shift Click Me</div>
```

**Note** 式の中で使われているすべてのシンボルが、トリガーとなるイベントに対して最初に解決されます。つまり、`myEvent[foo]` はまずイベント上の `foo` という名前のプロパティを探し、次に `foo` という名前のグローバルシンボルを探します。

#### 標準イベント修飾子

標準的なイベントには、その振る舞いを変更するモディファイアを付けることもできる。修飾子は以下の通りです：

* `once` - イベントが一度だけトリガーされる(例えば最初のクリック)
* `changed` - 要素の値が変更された場合のみイベントが変更されます。`change`はイベントの名前、`changed`はモディファイアの名前であることに注意してください。
* `delay:<timing declaration>` - イベントがリクエストをトリガーする前に遅延が発生する。そのイベントが再び現れると、遅延はリセットされる。
* `throttle:<timing declaration>` - スロットルはイベントがリクエストをトリガーした後に発生します。ディレイが完了する前にイベントが再び現れた場合、それは無視され、ディレイの最後にエレメントがトリガーされます。
* `from:<Extended CSS selector>` - リクエストのトリガーとなるイベントが、ドキュメント内の別の要素から来るようにする (例えば、ホットキーをサポートするために、ボディ上のキーイベントをリッスンする)
  * 標準的なCSSセレクタは、そのセレクタにマッチするすべての要素を解決する。したがって、`from:input`はページ上のすべての入力をリッスンすることになる。
  * ここでの拡張CSSセレクタは、以下の非標準CSS値を許容する：
    * `document` - ドキュメントのイベントを待機
    * `window` - ウィンドウのイベントを待機
    * `closest <CSS selector>` - 与えられたcssセレクタにマッチする、[最も近い](https://developer.mozilla.org/docs/Web/API/Element/closest)祖先要素、またはそれ自身を見つけます。
    * `find <CSS selector>` - 与えられたcssセレクタに最も近い子を見つけます
    * `next` [element.nextElementSibling](https://developer.mozilla.org/docs/Web/API/Element/nextElementSibling)を解決します。
    * `next <CSS selector>` 与えられた CSS セレクタにマッチする最初の要素を DOM 前方から探します。(例: `next .error` は `error` クラスを持つ最も近い兄弟要素をターゲットにします)
    * `previous` [element.previousElementSibling](https://developer.mozilla.org/docs/Web/API/Element/previousElementSibling)を解決します。
    * `previous <CSS selector>` 与えられた CSS セレクタにマッチする最初の要素を DOM を後方にスキャンします。(例: `previous .error` は `error` クラスを持つ最も近い兄弟要素をターゲットにします)
* `target:<CSS selector>` - イベントのターゲットをCSSセレクタでフィルタリングできる。これは、初期化の時点でDOMにない要素からのトリガーをリッスンしたい場合に便利です。例えば、ボディをリスニングしているが、子要素をターゲット・フィルターとするなど。
* `consume` - このオプションが含まれる場合、イベントは親に対する (あるいは親をリッスンしている要素に対する) 他の htmx リクエストをトリガーしません。
* `queue:<queue option>` - 別のイベントのリクエストが処理中にイベントが発生した場合に、イベントがどのようにキューに入れられるかを決定する。オプションは以下の通り：
  * `first` - 最初のイベントをキューに入れる
  * `last` - 最後のイベントをキューに入れる（デフォルト）
  * `all` - すべてのイベントをキューに入れる（イベントごとにリクエストを発行する）
  * `none` - 新しいイベントをキューに入れない

以下は、`keyup`で検索する検索ボックスの例であるが、検索値が変更され、ユーザーが1秒間何も新しいものを入力していない場合にのみ検索する：

```html
<input name="q"
       hx-get="/search" hx-trigger="keyup changed delay:1s"
       hx-target="#search-results"/>
```

検索結果のレスポンスは `/search` url の `div` に `search-results` という id で追加されます。

### 非標準イベント

htmxがサポートする非標準のイベントもいくつかある：

* `load` - ロード時にトリガーされる（何かをダラダラロードするのに便利）
* `revealed` - 要素がビューポートにスクロールされたときにトリガーされます（遅延ロードにも便利です）。css で `overflow` を `overflow-y: scroll` のように使う場合は、`revealed` の代わりに `intersect once` を使うべきです。
* `intersect` - 要素が最初にビューポートと交差したときに一度だけ発生する。これは2つの追加オプションをサポートしています：
    * `root:<selector>` - 交差するルート要素のCSSセレクタ
    * `threshold:<float>` - 0.0から1.0の間の浮動小数点数で、どの程度の交差点でイベントを発生させるかを示します。

### `HX-Trigger`ヘッダーによるトリガー

`<code>HX-Trigger</code>`レスポンスヘッダからイベントを発生させようとしている場合、`from:body`モディファイアを使いたいでしょう。  例えば、`<code>HX-Trigger: my-custom-event</code>`のようなヘッダをレスポンスと一緒に送信する場合、要素は次のようになります：

```html
  <div hx-get="/example" hx-trigger="my-custom-event from:body">
    Triggered by HX-Trigger header...
  </div>
```

順番に発射する

これは、ヘッダーが、トリガーさせたい要素とは異なるDOM階層でイベントをトリガーする可能性が高いためです。同様の理由で、ボディからのホットキーをリッスンすることもよくある。

### ポーリング

`every<timing declaration>`という構文を使うことで、エレメントに定期的にポーリングさせることができる：

```html
<div hx-get="/latest_updates" hx-trigger="every 1s">
  Nothing Yet!
</div>
```

この例では、毎秒 `/latest_updates` URL に `GET` を発行し、その結果をこの div の innerHTML に入れ替えます。

ポーリングにフィルタを追加したい場合は、ポーリング宣言の後に追加する必要があります：

```html
<div hx-get="/latest_updates" hx-trigger="every 1s [someConditional]">
  Nothing Yet!
</div>
```

### 複数のトリガー

複数のトリガーをカンマで区切って指定することができる。それぞれのトリガーは独自のオプションを持ちます。

```html
  <div hx-get="/news" hx-trigger="load, click delay:1s"></div>
```

この例では、`/news`はページロード時に即座にロードされ、クリックされるたびに1秒遅れて再度ロードされる。

### JavaScript経由

AJAXリクエストはJavaScript [`htmx.trigger()`](@/api.md#trigger) でもトリガーできる。

## メモ

* `hx-trigger` は継承されない。
* `hx-trigger`はAJAXリクエストなしで使うことができ、その場合は`htmx:trigger`イベントのみが発生する。
* 空白を含む CSS セレクタ (例 `form input`) を `from`- または `target` 修飾子に指定します。合格するためには、セレクタを括弧で囲む（例：`from:(フォーム入力)`、`from:nearest (フォーム入力)`）。

