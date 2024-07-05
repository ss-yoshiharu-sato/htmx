+++
title = "資料"
[extra]
custom_classes = "wide-content"
+++
<div class="row">
<div class="2 col nav">

**目次**

<div id="contents">

* [導入](#introduction)
* [インストール](#installing)
* [AJAX](#ajax)
  * [トリガー](#triggers)
    * [トリガー修飾子](#trigger-modifiers)
    * [トリガーフィルター](#trigger-filters)
    * [特別イベント](#special-events)
    * [ポーリング](#polling)
    * [ロードポーリング](#load_polling)
  * [表示器](#indicators)
  * [ターゲット](#targets)
  * [交換](#swapping)
  * [同期](#synchronization)
  * [CSSトランジション](#css_transitions)
  * [帯域外交換](#oob_swaps)
  * [パラメータ](#parameters)
  * [確認](#confirming)
* [継承](#inheritance)
* [ブースト](#boosting)
* [Web SocketとSSE](#websockets-and-sse)
* [履歴](#history)
* [リクエストと回答](#requests)
* [検証](#validation)
* [アニメーション](#animations)
* [拡張](#extensions)
* [イベントとロギング](#events)
* [デバック](#debugging)
* [スクリプティング](#scripting)
  * [hx-on 属性](#hx-on)
* [サードパーティとの統合](#3rd-party)
  * [ウェブコンポーネント](#web-components)
* [キャッシング](#caching)
* [セキュリティ](#security)
* [設定](#config)

</div>

</div>
<div class="10 col">

## htmxの概要 {#introduction}

htmxは、javascriptを使用するのではなく、HTMLから直接モダンブラウザの機能にアクセスできるライブラリです。

htmxを理解するために、まずアンカータグを見てみよう：

```html
<a href="/blog">Blog</a>
```

このアンカータグはブラウザに以下の内容を伝える：

> ユーザーがこのリンクをクリックしたら、'/blog'にHTTP GETリクエストを発行し、レスポンスの内容をブラウザ・ウィンドウにロードする。

それを念頭に置いて、次のHTMLを考えてみよう：

```html
<button hx-post="/clicked"
    hx-trigger="click"
    hx-target="#parent-div"
    hx-swap="outerHTML"
>
    Click Me!
</button>
```

これはhtmxに以下の内容を伝えている：

> ユーザーがこのボタンをクリックしたら、'/clicked'にHTTP POSTリクエストを発行し、レスポンスの内容を使ってDOM内のid`parent-div`の要素を置き換える。

htmxは、ハイパーテキストとしてのHTMLの核となる考え方を拡張し、一般化することで、言語内で直接、より多くの可能性を広げている。：

* アンカーやフォームだけでなく、あらゆる要素がHTTPリクエストを発行できるようになりました。
* クリックやフォーム送信だけでなく、あらゆるイベントがリクエストのトリガーになります。
* [HTTP 動詞](https://en.wikipedia.org/wiki/HTTP_Verbs) は、`GET` と `POST` だけでなく、どのようなものでも使用できます。
* ウィンドウ全体だけでなく、どの要素もリクエストによる更新の対象とすることができる。

__Note__ htmxを使用している場合、サーバー側では通常、*JSON*ではなく*HTML*で応答する。これによって、そのコンセプトを本当に理解する必要さえなく、[アプリケーション状態のエンジンとしてのハイパーテキスト](https://en.wikipedia.org/wiki/HATEOAS)を使って、[オリジナル・ウェブ・プログラミング・モデル](https://www.ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm)の中にしっかりと収まることができる。

もしお望みなら、htmxを使うときに[`data-`](https://html.spec.whatwg.org/multipage/dom.html#attr-data-*)という接頭辞を使うことができるということは言っておく価値がある：

```html
<a data-hx-post="/click">Click Me!</a>
```

最後に、htmxの[バージョン1](https://v1.htmx.org)はまだサポートされており、IE11をサポートしています。

## 1.x から 2.x への移行ガイド

[htmx 1.x](https://v1.htmx.org)からhtmx 2.xに移行する場合は、[htmx 1.x移行ガイド](@/migration-guide-htmx-1.md)を参照してください。

`intercooler.js`から`htmx`に移行する場合は、[intercooler移行ガイド](@/migration-guide-intercooler.md)を参照してください。

## インストール {#installing}

Htmxは依存関係のない、ブラウザ指向のjavascriptライブラリです。つまり、ドキュメントヘッドに`<script>`タグを追加するだけで、簡単に使用することができます。ビルドシステムも必要ありません。

### CDN(unpkg.comなど)を使う

htmxを使い始める最も早い方法は、CDN経由で読み込むことです。以下をheadタグに追加するだけで、すぐに始めることができます：

```html
<script src="https://unpkg.com/htmx.org@2.0.0" integrity="sha384-wS5l5IKJBvK6sPTKa2WZ1js3d947pvWXbPJ1OmWfEuxLgeHcEbjUUA5i9V5ZkpCw" crossorigin="anonymous"></script>
```

デバッグ用に最小化されていないバージョンも用意されています：

```html
<script src="https://unpkg.com/htmx.org@2.0.0/dist/htmx.js" integrity="sha384-Xh+GLLi0SMFPwtHQjT72aPG19QvKB8grnyRbYBNIdHWc2NkCrz65jlU7YrzO6qRp" crossorigin="anonymous"></script>
```

CDNのアプローチは極めてシンプルだが、[本番でCDNを使わない](https://blog.wesleyac.com/posts/why-not-javascript-cdn)ことを検討したほうがいいかもしれない。

### コピーをダウンロードして使う

htmxをインストールする最も簡単な方法は、プロジェクトにコピーすることです。

`htmx.min.js`を [unpkg.comから](https://unpkg.com/htmx.org/dist/htmx.min.js) ダウンロードし、プロジェクトの適切なディレクトリに追加し、必要に応じて`<script>`タグでインクルードする：

```html
<script src="/path/to/htmx.min.js"></script>
```

### npmを使う

npmスタイルのビルドシステムでは、[npm](https://www.npmjs.com/)を使ってhtmxをインストールできます：

```sh
npm install htmx.org
```

インストール後、`node_modules/htmx.org/dist/htmx.js`（または `.min.js`）を使用するために適切なツールを使用する必要があります。
例えば、htmxにいくつかの拡張機能やプロジェクト固有のコードをバンドルすることができる。

### Webpackを使う

webpackを使ってjavascriptを管理している場合：

* お気に入りのパッケージマネージャ（npm や yarn など）を使って `htmx` をインストールする。
* `index.js`にimportを追加する。

```js
import 'htmx.org';
```

グローバル変数 `htmx` を使いたい場合（推奨）、ウィンドウスコープに注入する必要があります：

* カスタムJSファイルの作成
* このファイルを `index.js` にインポートする（ステップ2のインポートの下）。

```js
import 'path/to/my_custom.js';
```

* そして、次のコードをファイルに追加する：

```js
window.htmx = require('htmx.org');
```

* 最後に、バンドルを再構築します。

## AJAX(Asynchronous JavaScript + XML) {#ajax}

htmxの中核は、HTMLから直接AJAXリクエストを発行できるようにする属性のセットです：

| 属性                                    | 説明                                          |
|----------------------------------------|----------------------------------------------|
| [hx-get](@/attributes/hx-get.md)       | 与えられたURLに`GET`リクエストを発行する。         |
| [hx-post](@/attributes/hx-post.md)     | 与えられたURLに`POST`リクエストを発行する。        |
| [hx-put](@/attributes/hx-put.md)       | 与えられたURLに`PUT`リクエストを発行する。         |
| [hx-patch](@/attributes/hx-patch.md)   | 与えられたURLに`PATCH`リクエストを発行する。       |
| [hx-delete](@/attributes/hx-delete.md) | 与えられたURLに対して`DELETE`リクエストを発行する。 |

これらの各属性は、AJAXリクエストを発行するURLを取ります。要素が[triggered](#triggers)されると、指定されたURLに対して指定されたタイプのリクエストを発行します：

```html
<button hx-put="/messages">
    Put To Messages
</button>
```

以下をブラウザに伝える：

> ユーザーがこのボタンをクリックしたら、URL /messagesにPUTリクエストを発行し、そのレスポンスをボタンにロードする。

### リクエストのトリガー {#triggers}

デフォルトでは、AJAXリクエストは要素の"natural"イベントによってトリガーされる：

* `input`、`textarea`、`select` は `change`イベントでトリガーされる。
* `form`は`submit`イベントでトリガーされる。
* それ以外はすべて `click` イベントによってトリガーされる。

異なる動作をさせたい場合は、[hx-trigger](@/attributes/hx-trigger.md) 属性を使って、どのイベントがリクエストを引き起こすかを指定することができます。

以下はマウスが入ると`/mouse_entered`にポストする`div`要素：

```html
<div hx-post="/mouse_entered" hx-trigger="mouseenter">
    [Here Mouse, Mouse!]
</div>
```

#### トリガー・モディファイア {#trigger-modifiers}

トリガーは、その動作を変更するいくつかの追加修飾子を持つこともできます。例えば、あるリクエストを一度だけ発生させたい場合、トリガーに `once` 修飾子を使うことができます：

```html
<div hx-post="/mouse_entered" hx-trigger="mouseenter once">
    [Here Mouse, Mouse!]
</div>
```

トリガーに使えるその他の修飾語は以下の通り：

* `changed` - 要素の値が変更された場合にのみリクエストを発行する。
* `delay:<time interval>` - リクエストを発行する前に、指定された時間（例えば `1s`）待つ。イベントが再度トリガーされると、カウントダウンはリセットされる。
* `throttle:<time interval>` - リクエストを発行する前に、与えられた時間 (例えば `1s`) を待つ。`delay` とは異なり、制限時間に達する前に新しいイベントが発生した場合、そのイベントは破棄されるので、リクエストは制限時間の終了時にトリガーされる。
* `from:<CSS Selector>` - 別の要素のイベントをリッスンします。これは、キーボードショートカットなどに使えます。

これらの属性を使用して、[Active Search](@/examples/active-search.md)のような多くの一般的なUXパターンを実装することができます：

```html
<input type="text" name="q"
    hx-get="/trigger_delay"
    hx-trigger="keyup changed delay:500ms"
    hx-target="#search-results"
    placeholder="Search..."
>
<div id="search-results"></div>
```

この入力は、入力が変更された場合、キーアップイベントの500ミリ秒後にリクエストを発行し、結果を `search-results` という id で `div` に挿入します。

[hx-trigger](@/attributes/hx-trigger.md)属性では、カンマ区切りで複数のトリガーを指定することができます。

#### トリガーフィルター {#trigger-filters}

イベント名の後に角括弧を使用し、評価されるjavascript式を囲むことで、トリガーフィルタを適用することもできます。その式が `true`と評価されればイベントはトリガされ、そうでなければトリガされません。

以下は、Controlキーを押しながら要素をクリックしたときのみトリガーする例です。

```html
<div hx-get="/clicked" hx-trigger="click[ctrlKey]">
    Control Click Me
</div>
```

`ctrlKey`のようなプロパティは、まずトリガーとなるイベントに対して解決され、次にグローバルスコープに対して解決される。`this`シンボルは現在の要素に設定される。

#### 特別イベント {#special-events}

htmxは、[hx-trigger](@/attributes/hx-trigger.md)で使用するいくつかの特別なイベントを提供します：

* `load` - 要素が最初にロードされたときに一度だけ発生する
* `revealed` - 要素が最初にビューポートにスクロールしたときに一度だけ発生する。
* `intersect` - 要素が最初にビューポートと交差したときに一度だけ発生する。これは2つの追加オプションをサポートしています：
    * `root:<selector>` - 交差するルート要素のCSSセレクタ
    * `threshold:<float>` - 0.0から1.0の間の浮動小数点数で、どの程度の交差点でイベントを発生させるかを示す。

また、高度なユースケースがある場合は、カスタムイベントを使用してリクエストをトリガーすることもできます。

#### ポーリング {#polling}

イベントを待つのではなく、指定したURLにポーリング(定期的な問い合わせ)させたい場合は、[`hx-trigger`](@/attributes/hx-trigger.md)属性と一緒に`every`構文を使うことができます：

```html
<div hx-get="/news" hx-trigger="every 2s"></div>
```

これはhtmxに次のように伝える。

> 2秒ごとに`/news`にGETを行い、レスポンスを`div`にロードする。

サーバーのレスポンスからポーリングを停止したい場合は、HTTPレスポンスコード[`286`](https://en.wikipedia.org/wiki/86_(term))で応答すると、その要素はポーリングをキャンセルします。

#### ロード・ポーリング {#load_polling}

htmxでポーリングを実現するために使用できるもう1つのテクニックは「ロードポーリング」であり、要素は遅延とともに`load`トリガーを指定し、自身をレスポンスに置き換える：

```html
<div hx-get="/messages"
    hx-trigger="load delay:1s"
    hx-swap="outerHTML"
>
</div>
```

もし`/messages`エンドポイントがこのように設定された`div`を返し続けると、毎秒URLに"ポーリング"し続ける。

ロード・ポーリングは、ユーザーに[プログレス・バー](@/examples/progress-bar.md)を表示するときなど、ポーリングが終了する`終点`がある場合に便利です。

### リクエスト表示器 {#indicators}

AJAXリクエストが発行されたとき、ブラウザは何もフィードバックしないので、何かが起こっていることをユーザーに知らせた方がよいことがよくあります。htmxでは `htmx-indicator`クラスを使うことでこれを実現できます。

`htmx-indicator`クラスは、このクラスを持つ要素の不透明度がデフォルトで`0`になるように定義されています。

htmx がリクエストを発行すると、`htmx-request` クラスを要素 (リクエスト元の要素か、指定されていれば別の要素) に付けます。`htmx-request`クラスは `htmx-indicator`クラスを持つ子要素の不透明度を`1`に遷移させ、インジケータを表示します。

```html
<button hx-get="/click">
    Click Me!
    <img class="htmx-indicator" src="/spinner.gif">
</button>
```

ここにボタンがあります。これがクリックされると、`htmx-request`クラスが追加され、スピナーgif要素が現れます。(最近は[SVG spinners](http://samherbert.net/svg-loaders/)が好きです)。

`htmx-indicator`クラスは不透明度を使って進捗インジケーターを隠したり見せたりしていますが、もし別の仕組みを使いたい場合は、このように独自のCSSトランジションを作成することができます：

```css
.htmx-indicator{
    display:none;
}
.htmx-request .htmx-indicator{
    display:inline;
}
.htmx-request.htmx-indicator{
    display:inline;
}
```

もし`htmx-request`クラスを別の要素に追加したい場合は、[hx-indicator](@/attributes/hx-indicator.md) 属性と CSSセレクタを使って追加することができます：

```html
<div>
    <button hx-get="/click" hx-indicator="#indicator">
        Click Me!
    </button>
    <img id="indicator" class="htmx-indicator" src="/spinner.gif"/>
</div>
```

ここでは、idで明示的にインジケータを呼び出している。親である `div`にクラスを配置しても同じ効果が得られることに注意してほしい。

[hx-disabled-elt](@/attributes/hx-disabled-elt.md)属性を使うことで、リクエストの間、要素に[`disabled`属性](https://developer.mozilla.org/en-US/docs/Web/HTML/Attributes/disabled)を追加することもできます。

### ターゲット {#targets}

リクエストを行った要素以外の別の要素にレスポンスを読み込ませたい場合は、CSSセレクタを取る[hx-target](@/attributes/hx-target.md)属性を使うことができます。Live Searchの例を見てみましょう：

```html
<input type="text" name="q"
    hx-get="/trigger_delay"
    hx-trigger="keyup delay:500ms changed"
    hx-target="#search-results"
    placeholder="Search..."
>
<div id="search-results"></div>
```

検索結果はinputタグではなく、`div#search-results`に読み込まれることがわかります。

#### 拡張CSSセレクタ {#extended-css-selectors}

`hx-target` と CSSセレクタのほとんどの属性は、"拡張"CSS 構文をサポートしています：

* `this`キーワードを使うことができる。これは `hx-target`属性が指定された要素がターゲットであることを示します。
* 最も近い`<CSSセレクタ>`構文は、与えられたCSSセレクタにマッチする[最も近い](https://developer.mozilla.org/docs/Web/API/Element/closest)祖先要素またはそれ自身を見つけます。(例: `closest tr` は要素に最も近いテーブル行をターゲットにします)
* `next <CSSセレクタ>`構文は、与えられたCSSセレクタにマッチするDOM内の次の要素を見つけます。
* `previous<CSSセレクタ>`構文は、指定されたCSSセレクタのDOM内の前の要素を探します。
* `find<CSSセレクタ>`は、与えられたCSSセレクタにマッチする最初の子の子孫要素を見つけます。(例えば、 `find tr` は、その要素の最初の子の子孫行をターゲットにします)

さらに、CSSセレクタは `<` と `/>` 文字で囲むことができ、ハイパースクリプトの [クエリーリテラル](https://hyperscript.org/expressions/query-reference/) 構文を模倣しています。

このような相対ターゲットは、DOMをたくさんの`id`属性で埋め尽くすことなく、柔軟なユーザーインターフェースを作成するのに便利です。


### スワッピング(置換方法) {#swapping}

htmx は、返された HTML を DOM に入れ替えるためのいくつかの異なる方法を提供します。デフォルトでは、コンテンツはターゲット要素の`innerHTML`を置き換えます。これを変更するには、[hx-swap](@/attributes/hx-swap.md) 属性に以下の値を指定します：

| Name | Description
|------|-------------
| `innerHTML` | デフォルト。コンテンツはターゲット要素の中に置かれます。
| `outerHTML` | ターゲット要素全体を返された内容で置き換えます。
| `afterbegin` | ターゲット内の最初の子の前にコンテンツを追加します。
| `beforebegin` | ターゲットの親要素でターゲットの前にコンテンツを追加する。
| `beforeend` | ターゲット内の最後の子の後に内容を追加する。
| `afterend` | ターゲットの親要素でターゲットの後にコンテンツを追加する。
| `delete` | レスポンスに関係なく、ターゲット要素を削除する。
| `none` | レスポンスの内容を追加しない([帯域外スワップ](#oob_swaps)と[レスポンスヘッダ](#response-headers)は処理される)

#### モーフスワップ {#morphing}

上記の標準的なスワップ機構に加えて、htmxは拡張機能によって*morphing*スワップもサポートしています。モーフィングスワップは、新しいコンテンツを単に置き換えるのではなく、既存の DOM にマージしようとします。スワップ操作の間に既存のノードをインプレースで変異させることで、フォーカスやビデオ状態などのようなものをよりよく保存することができます。

以下のエクステンションは、モーフスタイルのスワップに使用できます：

* [Idiomorph](https://github.com/bigskysoftware/idiomorph#htmx) - htmxの開発者によって作られたモーフィングアルゴリズム。
* [Morphdom Swap](https://github.com/bigskysoftware/htmx-extensions/blob/main/src/morphdom-swap/README.md) - オリジナルのDOMモーフィングライブラリである[morphdom](https://github.com/patrick-steele-idem/morphdom)に基づいています。
* [Alpine-morph](https://github.com/bigskysoftware/htmx-extensions/blob/main/src/alpine-morph/README.md) - [alpine morph](https://alpinejs.dev/plugins/morph)プラグインをベースにしたもので、alpine.jsと組み合わせて使用します。

#### トランジションを見る {#view-transitions}

新しい、実験的な[View Transitions API](https://developer.mozilla.org/en-US/docs/Web/API/View_Transitions_API)は、異なるDOM状態間のアニメーション遷移を作成する方法を開発者に提供します。このAPIはまだ開発中であり、すべてのブラウザで利用できるわけではありませんが、htmxはこの新しいAPIで動作する方法を提供しています。

この新しいAPIは、以下の方法で試すことができる：

* すべてのスワップにトランジションを使用するには、`htmx.config.globalViewTransitions`設定変数を`true`に設定する。
* `hx-swap`属性で`transition:true`オプションを使用する。
* 上記のどちらかの設定によって要素の入れ替えが行われようとしている場合、`htmx:beforeTransition`イベントをキャッチし、`preventDefault()`を呼び出すことで、要素の入れ替えをキャンセルすることができます。

ビューの遷移は、[Chromeのドキュメント](https://developer.chrome.com/docs/web-platform/view-transitions/#simple-customization)で説明されているように、CSSを使用して設定できます。

[アニメーションの例](/examples/animations#view-transitions)のページで、ビュー遷移の例を見ることができます。

#### スワップ・オプション {#swap-options}

[hx-swap](@/attributes/hx-swap.md)属性は、htmxのスワップ動作を調整するための多くのオプションをサポートしています。例えば、デフォルトでは、htmxは新しいコンテンツのどこかで見つかったtitleタグのタイトルを入れ替えます。`ignoreTitle`モディファイアをtrueに設定することで、この動作をオフにすることができます：

```html
    <button hx-post="/like" hx-swap="outerHTML ignoreTitle:true">Like</button>
```

`hx-swap`で使用できる修飾子は以下の通りである：

| オプション      | 説明                                                                                        |
|---------------|---------------------------------------------------------------------------------------------|
| `transition`  | `true`または`false`で、このスワップにビュー遷移APIを使うかどうかを指定する。                          |
| `swap`        | 古いコンテンツがクリアされてから新しいコンテンツが挿入されるまでのスワップ遅延時間（例：`100ms`）。        |
| `settle`      | 新しいコンテンツが挿入されてから決済されるまでの遅延時間（例：`100ms`）。                              |
| `ignoreTitle` | `true`に設定すると、新しいコンテンツで見つかったタイトルは無視され、ドキュメントのタイトルは更新されない。   |
| `scroll`      | `top`または`bottom`は、ターゲット要素を上端または下端にスクロールする。                               |
| `show`        | `top`または`bottom`は、対象要素の上端または下端をスクロールして表示する。                             |

すべてのスワップ修飾子は、スワップ・スタイルを指定した後に現れ、コロンで区切られる。

これらのオプションの詳細については、[hx-swap](@/attributes/hx-swap.md) ドキュメントを参照してください。

### 同期 {#synchronization}

2つのエレメント間のリクエストを調整したいことがよくある。例えば、あるエレメントからのリクエストを他のエレメントのリクエストに優先させたい場合や、他のエレメントのリクエストが終わるまで待ちたい場合などです。

htmxはこれを実現するために[`hx-sync`](@/attributes/hx-sync.md)属性を提供しています。

このHTMLの中で、フォーム送信と個々の入力のバリデーション要求の間の競合条件を考えてみよう：

```html
<form hx-post="/store">
    <input id="title" name="title" type="text"
        hx-post="/validate"
        hx-trigger="change">
    <button type="submit">Submit</button>
</form>
```

`hx-sync`を使用しない場合、入力フォームに入力してすぐに送信すると、 `/validate`と`/store`への2つの並列リクエストがトリガーされる。

`hx-sync="closest form:abort"`を入力に使うと、フォーム上のリクエストを監視し、フォームリクエストが存在するか、入力リクエストが処理中に開始した場合、入力のリクエストを中止します：

```html
<form hx-post="/store">
    <input id="title" name="title" type="text"
        hx-post="/validate"
        hx-trigger="change"
        hx-sync="closest form:abort">
    <button type="submit">Submit</button>
</form>
```

これにより、2つのエレメント間の同期が宣言的な方法で解決される。

htmx はプログラム的にリクエストをキャンセルする方法もサポートしています: 処理中のリクエストをキャンセルするために `htmx:abort`イベントを要素に送ることができます：

```html
<button id="request-button" hx-post="/example">
    Issue Request
</button>
<button onclick="htmx.trigger('#request-button', 'htmx:abort')">
    Cancel Request
</button>
```

より多くの例と詳細は、[`hx-sync` 属性のページ](@/attributes/hx-sync.md) を参照してください。

### CSSトランジション {#css_transitions}

htmxを使えば、javascriptを使わずに[CSS Transitions](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Transitions/Using_CSS_transitions)を簡単に使うことができます。以下のHTMLコンテンツを考えてみましょう：

```html
<div id="div1">Original Content</div>
```

このコンテンツがAjaxリクエストによってhtmxに置き換えられ、新しいコンテンツになると想像してほしい：

```html
<div id="div1" class="red">New Content</div>
```

２つのことに注意してほしい：

* この`div`は、元のコンテンツでも新しいコンテンツでも同じidを持つ。
* 新しいコンテンツに `red` クラスが追加された。

この状況を考えると、古い状態から新しい状態への遷移をCSSで記述することができる：

```css
.red {
    color: red;
    transition: all ease-in 1s ;
}
```

htmxがこの新しいコンテンツを入れ替えるとき、CSSのトランジションが新しいコンテンツに適用されるような方法で行われ、新しい状態へのスムーズな移行を実現します。

つまり、CSSのトランジションを使うために必要なことは、リクエスト間で要素の`id`を安定させることです！

[アニメーションの例](@/examples/animations.md)に詳細とライブ・デモンストレーションがあります。

#### 詳細 {#details}

CSSトランジションがhtmxで実際にどのように機能するのかを理解するには、htmxが使用するスワップ＆セトリングモデルを理解する必要があります。

1. サーバーから新しいコンテンツを受信すると、そのコンテンツが入れ替えられる前に、ページの既存のコンテンツが`id`属性によって一致する要素がないか調べられます。
2. 新しいコンテンツの要素に一致するものが見つかった場合、入れ替えが行われる前に古いコンテンツの属性が新しい要素にコピーされます。
3. その後、新しいコンテンツは*古い*属性値と入れ替えられます。
4. 最後に、"settle"遅延（デフォルトでは20ミリ秒）の後、新しい属性値がスワップされる。

少しクレイジーですが、これによって開発者がjavascriptを使わなくてもCSSのトランジションが動作するようになります。

### アウト・オブ・バンド・スワップ {#oob_swaps}

もし`id`属性を使ってレスポンスの内容を直接 DOMに入れ替えたい場合は、*response* html の[hx-swap-oob](@/attributes/hx-swap-oob.md) 属性を使うことができます：

```html
<div id="message" hx-swap-oob="true">Swap me directly!</div>
Additional Content
```

このレスポンスでは、`div#message`はマッチするDOM要素に直接スワップされ、追加コンテンツは通常の方法でターゲットにスワップされる。
は通常の方法でターゲットにスワップされます。

このテクニックを使って、他のリクエストにアップデートを"ピギーバック(便乗)"させることができる。

#### 厄介なテーブル {#Troublesome Tables}

表要素は、帯域外のスワップと組み合わせると問題になることがあります。HTMLの仕様では、表要素の多くはDOMの中で自立することができないからです（例：`<tr>`や`<td>`）。

この問題を避けるために、`template`タグを使ってこれらの要素をカプセル化することができます：

```html
<template>
  <tr id="message" hx-swap-oob="true"><td>Joe</td><td>Smith</td></tr>
</template>
```

#### 交換するコンテンツの選択

レスポンスのHTMLのサブセットを選択してターゲットに入れ替えたい場合は、[hx-select](@/attributes/hx-select.md) 属性を使うことができます。この属性はCSSセレクタを受け取り、レスポンスからマッチする要素を選択します。

また、[hx-select-oob](@/attributes/hx-select-oob.md)属性を使うことで、帯域外交換のためにコンテンツの断片を選び出すことができます。

#### スワップ中のコンテンツの保存

もし、入れ替えが発生しても保存しておきたいコンテンツがある場合（例えば、入れ替えが発生しても再生しておきたいビデオプレーヤーなど）、保存しておきたい要素に[hx-preserve](@/attributes/hx-preserve.md)属性を使うことができます。

### パラメータ {#parameters}

デフォルトでは、リクエストを発生させる要素に値がある場合、その値が含まれます。要素がフォームの場合は、その中のすべての入力の値が含まれます。

HTMLフォームと同様に、入力の`name`属性は htmx が送るリクエストのパラメータ名として使われます。

さらに、その要素が `GET`ではないリクエストを引き起こす場合、最も近いフォームのすべての入力値が含まれます。

他の要素の値も含めたい場合は、[hx-include](@/attributes/hx-include.md)属性に、リクエストに含めたい値を持つ全ての要素をCSSセレクタで指定します。

いくつかのパラメータを除外したい場合は、[hx-params](@/attributes/hx-params.md) 属性を使うことができます。

最後に、プログラムでパラメータを変更したい場合は、[htmx:configRequest](@/events.md#htmx:configRequest)イベントを使うことができます。

#### ファイルのアップロード {#files}

htmxリクエストでファイルをアップロードしたい場合は、[hx-encoding](@/attributes/hx-encoding.md) 属性を `multipart/form-data` に設定してください。これにより、`FormData`オブジェクトを使ってリクエストが送信され、ファイルが適切にリクエストに含まれるようになります。

サーバーサイドの技術によっては、このタイプのボディコンテンツを持つリクエストの扱い方を大きく変えなければならないかもしれないことに注意してください。

htmxはアップロード中に標準の`progress`イベントに基づいて定期的に`htmx:xhr:progress`イベントを発生させることに注意してください。

[プログレスバー](@/examples/file-upload.md)や[エラー処理](@/examples/file-upload-input.md)など、より高度なフォームパターンについては、[examples](@/examples/_index.md)を参照してください。

#### エクストラ・バリュー

[hx-vals](@/attributes/hx-vals.md)(JSON形式の名前式ペア)と[hx-vars](@/attributes/hx-vars.md)属性(動的に計算されるカンマ区切りの名前式ペア)を使って、リクエストに追加の値を含めることができます。

### リクエストの確認 {#confirming}

リクエストを出す前にアクションを確認したいことがよくある。htmxは[`hx-confirm`](@/attributes/hx-confirm.md)属性をサポートしており、シンプルなjavascriptダイアログを使ってアクションを確認することができます：

```html
<button hx-delete="/account" hx-confirm="本当にアカウントを削除しますか？">
    Delete My Account
</button>
```

イベントを使うことで、より洗練された確認ダイアログを実装することができます。[confirm example](@/examples/confirm.md)は、htmxアクションの確認のために[sweetalert2](https://sweetalert2.github.io/)ライブラリを使用する方法を示しています。

#### イベントを使ったリクエストの確認

[`htmx:confirm`イベント](@/events.md#htmx:confirm)イベントで確認を行うこともできます。このイベントは(`hx-confirm`属性を持つ要素だけでなく)、リクエストの*すべての*トリガーで発生し、リクエストの非同期確認を実装するために使用することができます。

以下は、`confirm-with-sweet-alert='true'`属性を持つ要素に[sweet alert](https://sweetalert.js.org/guides/)を使う例です：

```javascript
document.body.addEventListener('htmx:confirm', function(evt) {
  if (evt.target.matches("[confirm-with-sweet-alert='true']")) {
    evt.preventDefault();
    swal({
      title: "Are you sure?",
      text: "Are you sure you are sure?",
      icon: "warning",
      buttons: true,
      dangerMode: true,
    }).then((confirmed) => {
      if (confirmed) {
        evt.detail.issueRequest();
      }
    });     
  }
});
```

## 属性の継承 {#inheritance}

htmxのほとんどの属性は継承されます。これによって、コードの重複を避けるために、属性をDOMに"上げる"ことができます。次のhtmxを考えてみましょう：

```html
<button hx-delete="/account" hx-confirm="Are you sure?">
    Delete My Account
</button>
<button hx-put="/account" hx-confirm="Are you sure?">
    Update My Account
</button>
```

ここでは `hx-confirm` 属性が重複しています。この属性は親要素にぶら下げることができます：

```html
<div hx-confirm="Are you sure?">
    <button hx-delete="/account">
        Delete My Account
    </button>
    <button hx-put="/account">
        Update My Account
    </button>
</div>
```

この `hx-confirm` 属性は、その中にあるすべての htmx-powered 要素に適用されます。

この継承を取り消したいと思うこともあるだろう。このグループにキャンセルボタンがあるが、確定させたくない場合を考えてみよう。このように`unset`ディレクティブを追加することができます：

```html
<div hx-confirm="Are you sure?">
    <button hx-delete="/account">
        Delete My Account
    </button>
    <button hx-put="/account">
        Update My Account
    </button>
    <button hx-confirm="unset" hx-get="/">
        Cancel
    </button>
</div>
```

上の2つのボタンは確認ダイアログを表示するが、下のキャンセルボタンは表示しない。

要素ごと、属性ごとに継承を無効にするには、[`hx-disinherit`](@/attributes/hx-disinherit.md) 属性を使います。

属性の継承を完全に無効にしたい場合は、`htmx.config.disableInheritance`設定変数を`true`に設定します。これにより、デフォルトで継承が無効になり、[`hx-inherit`](@/attributes/hx-inherit.md) 属性で継承を明示的に指定できるようになります。

## ブースト {#boosting}

Htmxは、[hx-boost](@/attributes/hx-boost.md)属性で、通常のHTMLアンカーとフォームの「ブースト（body部分を全体的に更新）」をサポートしています。この属性は、すべてのアンカータグとフォームを、デフォルトではページの本文をターゲットとするAJAXリクエストに変換します。

例を挙げます：

```html
<div hx-boost="true">
    <a href="/blog">Blog</a>
</div>
```

このdivのアンカータグは`/blog`にAJAX `GET`リクエストを発行し、そのレスポンスを`body`タグに入れ替える。

### プログレッシブ・エンハンスメント {#progressive_enhancement}

`hx-boost`の特徴は、javascriptが有効でない場合、優雅にデグレードすることです：リンクやフォームは動作し続けますが、ajaxリクエストを使用しません。これは[プログレッシブ・エンハンスメント](https://developer.mozilla.org/en-US/docs/Glossary/Progressive_Enhancement)として知られており、より多くのユーザーがあなたのサイトの機能を利用できるようになります。

他のhtmxパターンも同様にプログレッシブ・エンハンスメントを達成するために適応させることができるが、より多くの考えが必要になるだろう。

[アクティブ検索](@/examples/active-search.md)の例を考えてみましょう。javascriptを有効にしていない人はこの機能を使うことができません。例をできるだけ簡潔にするためにそのように記述されています。

しかし、htmxで強化された入力をform要素でラップすることもできます：

```html
<form action="/search" method="POST">
    <input class="form-control" type="search"
        name="search" placeholder="Begin typing to search users..."
        hx-post="/search"
        hx-trigger="keyup changed delay:500ms, search"
        hx-target="#search-results"
        hx-indicator=".htmx-indicator">
</form>
```

このようにすれば、javascriptが有効なクライアントには、アクティブ検索という素晴らしいUXが提供されるが、javascriptが有効でないクライアントは、エンターキーを押しても検索ができるようになる。さらに良いのは、「検索」ボタンも追加できることです。
その場合、`hx-post`でフォームを更新し、`action`属性を反映させるか、`hx-boost`を使用する必要があります。

サーバー側で `HX-Request` ヘッダーをチェックして、htmx駆動のリクエストと通常のリクエストを区別し、クライアントに何をレンダリングするかを正確に判断する必要がある。

アプリケーションのプログレッシブ・エンハンスメントのニーズを達成するために、他のパターンも同様に適応させることができます。

おわかりのように、これはより多くの思考と作業を必要とする。また、いくつかの機能は完全に範囲外になります。このようなトレードオフは、開発者であるあなた自身が、プロジェクトの目標や利用者を考慮して行わなければなりません。

[アクセシビリティ](https://developer.mozilla.org/en-US/docs/Learn/Accessibility/What_is_accessibility)はプログレッシブ・エンハンスメントと密接に関連する概念です。`hx-boost`のようなプログレッシブ・エンハンスメントのテクニックを使うことで、あなたのhtmxアプリケーションは多くのユーザーにとってよりアクセスしやすくなります。

htmxはHTML指向なので、tmxベースのアプリケーションは、通常の非AJAX駆動のWebアプリケーションと非常によく似ている。

そのため、通常のHTMLアクセシビリティ勧告が適用されます。例えば:

* できるだけセマンティックなHTMLを使う（つまり、適切なものに適切なタグを使う）
* フォーカス状態が明確に見えるようにする
* すべてのフォーム・フィールドにテキスト・ラベルを関連付ける
* 適切なフォント、コントラストなどを用いて、アプリケーションの可読性を最大化する。

## Web SocketとSSE {#websockets-and-sse}

Web SocketsとServer Sent Events(SSE)は拡張機能によってサポートされています。詳しくは[SSE extension](https://github.com/bigskysoftware/htmx-extensions/blob/main/src/sse/README.md)と[WebSocket extension](https://github.com/bigskysoftware/htmx-extensions/blob/main/src/ws/README.md)のページをご覧ください。

## 履歴サポート {#history}

Htmxは、[ブラウザ履歴API](https://developer.mozilla.org/en-US/docs/Web/API/History_API)と相互作用するためのシンプルなメカニズムを提供します：

与えられた要素に、そのリクエストURLをブラウザのナビゲーションバーにプッシュし、ブラウザの履歴にページの現在の状態を追加したい場合、[hx-push-url](@/attributes/hx-push-url.md) 属性を含めます：

```html
<a hx-get="/blog" hx-push-url="true">Blog</a>
```

ユーザーがこのリンクをクリックすると、htmxは現在のDOMをスナップショットし、/blogへのリクエストを行う前にそれを保存する。その後、スワップを行い、新しい場所を履歴スタックにプッシュします。

ユーザーが戻るボタンを押すと、htmxはストレージから古いコンテンツを取得し、以前の状態に「戻る」ことをシミュレートして、ターゲットに戻します。キャッシュにその場所が見つからない場合、htmxはヘッダ `HX-History-Restore-Request` をtrueに設定して、指定された URL に ajax リクエストを行い、ページ全体に必要な HTML を返します。あるいは、`htmx.config.refreshOnHistoryMiss`設定変数がtrueに設定されている場合、ブラウザのハードリフレッシュを行います。

**NOTE:** URLを履歴にプッシュした場合、そのURLに移動して全ページを取得できなければならない！ユーザーはURLをコピーしてメールや新しいタブに貼り付けることができます。さらに、htmxは履歴キャッシュにページがない場合、履歴を復元する際にページ全体を必要とします。

### 履歴スナップショット要素の指定

デフォルトでは、htmx は `body` からヒストリのスナップショットを取得してリストアします。通常はこれが正しいのですが、スナップショットにもっと狭い要素を使いたい場合は、[hx-history-elt](@/attributes/hx-history-elt.md) 属性を使って別の要素を指定することができます。

注意：この要素はすべてのページに必要で、さもなければ履歴からの復元は確実に機能しない。

### サードパーティライブラリによるDOM変更の取り消し

サードパーティライブラリを使用していて、htmxの履歴機能を使用したい場合、スナップショットを取得する前にDOMをクリーンアップする必要があります。select要素をよりリッチなユーザーエクスペリエンスにする[Tom Select](https://tom-select.js.org/)ライブラリについて考えてみましょう。Tom Selectをセットアップして、`.tomselect`クラスを持つ入力要素をリッチなselect要素に変えてみましょう。

まず、新しいコンテンツでクラスを持つ要素を初期化する必要がある：

```javascript
htmx.onLoad(function (target) {
    // find all elements in the new content that should be
    // an editor and init w/ TomSelect
    var editors = target.querySelectorAll(".tomselect")
            .forEach(elt => new TomSelect(elt))
});
```

これにより、`.tomselect`クラスを持つすべての入力要素に対してリッチセレクタが作成されます。なぜなら、TomSelectは履歴の内容が画面に読み込まれたときに再初期化されるからです。

これに対処するには、`htmx:beforeHistorySave`イベントをキャッチして、TomSelectの変異に対して`destroy()`を呼び出して、TomSelectの変更を一掃する必要がある：

```javascript
htmx.on('htmx:beforeHistorySave', function() {
    // find all TomSelect elements
    document.querySelectorAll('.tomSelect')
            .forEach(elt => elt.tomselect.destroy()) // and call destroy() on them
})
```

これはDOMを元のHTMLに戻し、クリーンなスナップショットを可能にします。

### 履歴スナップショットの無効化

[hx-history](@/attributes/hx-history.md)属性を `false` に設定することで、URLの履歴スナップショットを無効にすることができます。これは、機密データが localStorage キャッシュに入るのを防ぐために使用できます。履歴ナビゲーションは期待通りに動作しますが、復元時にURLはローカルの履歴キャッシュではなくサーバーからリクエストされます。

## リクエストと回答 {#requests}

Htmxは、AJAXリクエストに対するレスポンスがHTMLであることを期待します。一般的にはHTMLの断片です（[hx-select](@/attributes/hx-select.md)タグでマッチされた完全なHTMLドキュメントも便利ですが）。Htmxは返されたHTMLを、指定されたターゲットで、指定されたスワップ戦略でドキュメントにスワップします。

スワップでは何もせず、クライアント側のイベントをトリガーしたい場合もあるでしょう（[後述](#response-headers)）。

このような場合、デフォルトでは `204 - No Content` 応答コードを返すことができ、htmx は応答の内容を無視します。

サーバーからのエラーレスポンス(例えば404や501)があった場合、htmxは[`htmx:responseError`](@/events.md#htmx:responseError)イベントをトリガーします。

接続エラーが発生すると、`htmx:sendError`イベントが発生する。

### レスポンス処理の設定 {#response-handling}

htmxの上記の動作は、`htmx.config.responseHandling` 配列を変更または置き換えることで設定できる。このオブジェクトは次のように定義されたJavaScriptオブジェクトの集まりです：

```js
    responseHandling: [
        {code:"204", swap: false},   // 204 - No Content by default does nothing, but is not an error
        {code:"[23]..", swap: true}, // 200 & 300 responses are non-errors and are swapped
        {code:"[45]..", swap: false, error:true}, // 400 & 500 responses are not swapped and are errors
    ]
```

htmx がレスポンスを受信すると、`htmx.config.responseHandling` 配列を順番に繰り返し、与えられたオブジェクトの `code` プロパティが正規表現として扱われたときに、現在のレスポンスにマッチするかどうかをテストします。エントリが現在のレスポンスコードにマッチする場合、レスポンスが処理されるかどうか、またどのように処理されるかを決定するために使用されます。

この配列のエントリーのレスポンス処理設定に使用できるフィールドは以下のとおりです：

* `code` - 応答コードに対してテストされる正規表現を表す文字列。
* `swap` - レスポンスがDOMにスワップされる場合は `true` 、そうでない場合は `false` 。
* `error` - htmx がこの応答をエラーとして扱う場合は `true` とする。
* `ignoreTitle` - htmxがレスポンスのタイトルタグを無視する場合は`true`。
* `select` - レスポンスからコンテンツを選択するために使用するCSSセレクタ。
* `target` - レスポンスの代替ターゲットを指定するCSSセレクタ。
* `swapOverride` - 代替スワップ・メカニズム

#### レスポンス処理の設定例 {#response-handling}

この設定の使い方の例として、バリデーションエラーが発生したときに、サーバーサイドフレームワークが [`422 - Unprocessable Entity`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/422) レスポンスを返す場合を考えてみましょう。デフォルトでは、htmxはこのレスポンスを無視します。なぜなら、このレスポンスは正規表現`[45]...`にマッチするからです。

[meta config](#configuration-options) メカニズムを使ってresponseHandlingを設定すると、次のようになる：

```html
<meta name="htmx-config" content='{code:"204", swap: false},   // 204 - No Content by default does nothing, but is not an error
                                  {code:"[23]..", swap: true}, // 200 & 300 responses are non-errors and are swapped
                                  {code:"422", swap: true}, // 422 responses are swapped
                                  {code:"[45]..", swap: false, error:true}, // 400 & 500 responses are not swapped and are errors'>
```

HTTPレスポンスコードに関係なく、すべてを交換したい場合は、この設定を使うことができる：

```html
<meta name="htmx-config" content='{code:".*", swap: true}, // all responses are swapped'>
```

最後に、[Response Targets](https://github.com/bigskysoftware/htmx-extensions/blob/main/src/response-targets/README.md)エクステンションを使うことを検討する価値があります。このエクステンションでは、属性によってレスポンスコードの振る舞いを宣言的に設定することができます。

### CORS

クロスオリジンコンテキストでhtmxを使用する場合、クライアント側でhtmxヘッダーが見えるように、Access-Controlヘッダーを設定するようにウェブサーバーを設定することを忘れないでください。

- [Access-Control-Allow-Headers (for request headers)](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Access-Control-Allow-Headers)
- [Access-Control-Expose-Headers (for response headers)](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Access-Control-Expose-Headers)

[See all the request and response headers that htmx implements.](@/reference.md#request_headers)

### リクエスト・ヘッダ

htmxはリクエストに多くの有用なヘッダを含みます：

| ヘッダー                      | 説明                                                         |
|------------------------------|-------------------------------------------------------------|
| `HX-Boosted`                 | [hx-boost](@/attributes/hx-boost.md)を使った要素経由のリクエストでを示します。
| `HX-Current-URL`             | ブラウザの現在のURL
| `HX-History-Restore-Request` | ローカル履歴キャッシュにミスがあった後の履歴復元リクエストであれば "true"
| `HX-Prompt`                  | [hx-prompt](@/attributes/hx-prompt.md)に対するユーザーの応答。
| `HX-Request`                 | 常に "真"
| `HX-Target`                  | ターゲット要素が存在すれば、その`id`を指定する。
| `HX-Trigger-Name`            | トリガーされた要素が存在する場合、その要素の `name` を指定する。
| `HX-Trigger`                 | トリガーされた要素の `id` が存在する場合、それを指定する。

### レスポンス・ヘッダ {#response-headers}

htmx はいくつかの htmx 固有のレスポンスヘッダをサポートしています：

* [`HX-Location`](@/headers/hx-location.md) - これにより、全ページのリロードを行わないクライアントサイドのリダイレクトが可能になる。
* [`HX-Push-Url`](@/headers/hx-push-url.md) - 新しいurlを履歴スタックにプッシュする。
* `HX-Redirect` - クライアント側で新しい場所にリダイレクトすることができる。
* `HX-Refresh` - "true"に設定された場合、クライアント側はページの完全な更新を行う。
* [`HX-Replace-Url`](@/headers/hx-replace-url.md) - ロケーションバーの現在のURLを置き換える。
* `HX-Reswap` - レスポンスがどのようにスワップされるかを指定することができます。指定できる値については [hx-swap](@/attributes/hx-swap.md) を参照してください。
* `HX-Retarget` - コンテンツ更新のターゲットをページ上の別の要素に更新するCSSセレクタ。
* `HX-Reselect` - レスポンスのどの部分を入れ替えるかを選択できるCSSセレクタです。既存の[`hx-select`](@/attributes/hx-select.md)を上書きします。
* [`HX-Trigger`](@/headers/hx-trigger.md) - クライアント側のイベントをトリガーできる。
* [`HX-Trigger-After-Settle`](@/headers/hx-trigger.md) - これにより、決済ステップの後にクライアントサイドのイベントをトリガーすることができます。
* [`HX-Trigger-After-Swap`](@/headers/hx-trigger.md) - スワップ・ステップの後にクライアント側イベントをトリガーすることができる。

`HX-Trigger` ヘッダについては、[`HX-Trigger` レスポンスヘッダ](@/headers/hx-trigger.md) を参照してください。

htmx経由でフォームを送信すると、[Post/Redirect/Getパターン](https://en.wikipedia.org/wiki/Post/Redirect/Get)が不要になるという利点があります。
サーバー上でPOSTリクエストの処理に成功した後、[HTTP 302 (リダイレクト)](https://en.wikipedia.org/wiki/HTTP_302)を返す必要はありません。新しいHTMLフラグメントを直接返すことができます。

### リクエストにおける操作の順 {#request-operations}

htmxリクエストにおける操作の順序は以下の通りである：

* エレメントはトリガーされ、リクエストを開始する。
  * リクエストに対して値が集められる。
  * `htmx-request`クラスは適切な要素に適用される。
  * リクエストは、AJAXを介して非同期に発行されます。
    * レスポンスを受け取ると、ターゲット要素は `htmx-swapping` クラスでマークされる。
    * オプションでスワップ遅延が適用されます（[hx-swap](@/attributes/hx-swap.md) 属性を参照）。
    * 実際のコンテンツ交換は
        * `htmx-swapping`クラスはターゲットから削除される。
        * 新しいコンテンツには `htmx-added` クラスが追加される。
        * `htmx-settling`クラスがターゲットに適用される。
        * 決済遅延が行われる（デフォルト：20ms）
        * DOMに決着
        * `htmx-settling`クラスはターゲットから削除される。
        * 新しいコンテンツからは `htmx-added` クラスが削除される。

`htmx-swapping`クラスと`htmx-settling`クラスを使って、ページ間の[CSSトランジション](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Transitions/Using_CSS_transitions)を作成することができます。

## 検証 {#Validation}

Htmxは[HTML5 Validation API](https://developer.mozilla.org/en-US/docs/Learn/Forms/Form_validation)と統合しており、バリデーション可能な入力が無効な場合、フォームのリクエストを発行しません。これはAJAXリクエストにもWebSocket送信にも当てはまります。

Htmxはバリデーションに関連したイベントを発生させ、カスタムのバリデーションやエラー処理をフックするために使用できます：

* `htmx:validation:validate` - 要素の `checkValidity()` メソッドが呼ばれる前に呼び出される。カスタムのバリデーションロジックを追加するために使用することができる。
* `htmx:validation:failed` - `checkValidity()`がfalseを返したときに呼び出される。
* `htmx:validation:halted` - バリデーションエラーのためにリクエストが発行されなかったときに呼び出される。具体的なエラーは `event.detail.errors` オブジェクトで確認できます。

フォーム以外の要素は、デフォルトではリクエストの前にバリデーションを行わない。しかし、[`hx-validate`](@/attributes/hx-validate.md) 属性を "true"に設定することで、バリデーションを有効にすることができます。

### 検証例

以下は、[`hx-on`](/attributes/hx-on) 属性を使用して、`htmx:validation:validate` イベントをキャッチし、入力に値 `foo` があることを要求する入力の例です：

```html
<form id="example-form" hx-post="/test">
    <input name="example"
           onkeyup="this.setCustomValidity('') // reset the validation on keyup"
           hx-on:htmx:validation:validate="if(this.value != 'foo') {
                    this.setCustomValidity('Please enter the value foo') // set the validation error
                    htmx.find('#example-form').reportValidity()          // report the issue
                }">
</form>
```

クライアント側のバリデーションは、常にバイパスされる可能性があるため、すべてサーバー側でやり直す必要があることに注意してください。

## アニメーション {#animations}

Htmxでは、HTMLとCSSだけを使って、多くの場面で[CSSトランジション](#css_transitions)を使うことができます。

利用可能なオプションの詳細については、[アニメーションガイド](@/examples/animations.md)を参照してください。

## 拡張 {#extensions}

Htmxには、ライブラリの動作をカスタマイズできる拡張メカニズムがある。
拡張機能は[javascript](https://github.com/bigskysoftware/htmx-extensions/tree/main?tab=readme-ov-file#defining-an-extension)で定義され、[`hx-ext`](@/attributes/hx-ext.md)属性を通して使用されます：

```html
<div hx-ext="debug">
    <button hx-post="/example">This button used the debug extension</button>
    <button hx-post="/example" hx-ext="ignore:debug">This button does not</button>
</div>
```

htmxに独自の拡張機能を追加することに興味がある場合は、[拡張機能のドキュメントを参照](https://github.com/bigskysoftware/htmx-extensions/tree/main?tab=readme-ov-file#defining-an-extension)。

## イベントとログ {#events}

Htmxは、ロギングシステムを兼ねた、広範な[イベントメカニズム](@/reference.md#events)を持っています。

指定されたhtmxイベントに登録したい場合は、次のようにします。

```js
document.body.addEventListener('htmx:load', function(evt) {
    myJavascriptLib.init(evt.detail.elt);
});
```

あるいは、次のようなhtmxヘルパーを使うこともできる：

```javascript
htmx.on("htmx:load", function(evt) {
    myJavascriptLib.init(evt.detail.elt);
});
```

`htmx:load` イベントは htmx によって要素が DOM に読み込まれるたびに発生し、実質的に通常の `load` イベントに相当します。

htmxイベントの一般的な使い方としては、以下のようなものがある：

### イベントでサードパーティライブラリを初期化する {#init_3rd_party_with_events}

`htmx:load`イベントを使用してコンテンツを初期化することは非常に一般的なので、htmxはヘルパー関数を提供している：

```javascript
htmx.onLoad(function(target) {
    myJavascriptLib.init(target);
});
```

これは最初の例と同じことをするが、少しすっきりしている。

### イベントを使ってリクエストを構成する {#config_request_with_events}

[`htmx:configRequest`](@/events.md#htmx:configRequest)イベントを処理することで、AJAXリクエストが発行される前に修正することができます：

```javascript
document.body.addEventListener('htmx:configRequest', function(evt) {
    evt.detail.parameters['auth_token'] = getAuthToken(); // add a new parameter into the request
    evt.detail.headers['Authentication-Token'] = getAuthToken(); // add a new header into the request
});
```

ここでは、送信前にリクエストにパラメータとヘッダーを追加する。

### イベントによるスワッピング動作の変更 {#modifying_swapping_behavior_with_events}

htmxのスワップ動作を変更するために、[`htmx:beforeSwap`](@/events.md#htmx:beforeSwap)イベントを扱うことができる：

```javascript
document.body.addEventListener('htmx:beforeSwap', function(evt) {
    if(evt.detail.xhr.status === 404){
        // alert the user when a 404 occurs (maybe use a nicer mechanism than alert())
        alert("Error: Could Not Find Resource");
    } else if(evt.detail.xhr.status === 422){
        // allow 422 responses to swap as we are using this as a signal that
        // a form was submitted with bad data and want to rerender with the
        // errors
        //
        // set isError to false to avoid error logging in console
        evt.detail.shouldSwap = true;
        evt.detail.isError = false;
    } else if(evt.detail.xhr.status === 418){
        // if the response code 418 (I'm a teapot) is returned, retarget the
        // content of the response to the element with the id `teapot`
        evt.detail.shouldSwap = true;
        evt.detail.target = htmx.find("#teapot");
    }
});
```

ここでは、通常htmxではスワップを行わないいくつかの[400レベルエラー応答コード](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status#client_error_responses)を扱っています。

### イベント名 {#event_naming}

すべてのイベントは2つの異なる名前で発生することに注意してください。

* キャメルケース
* ケバブ・ケース

例えば、`htmx:afterSwap` や `htmx:after-swap` を listen することができる。これにより、他のライブラリとの相互運用が容易になる。例えば[Alpine.js](https://github.com/alpinejs/alpine/)はkebab caseを必要とする。

### ロギング {#Logging}

`htmx.logger` でロガーを設定すると、すべてのイベントがログに記録される。これはトラブルシューティングに非常に便利です：

```javascript
htmx.logger = function(elt, event, data) {
    if(console) {
        console.log(event, elt, data);
    }
}
```

## デバッグ {#debugging}

htmx（または他の宣言型言語）を使った宣言型プログラミングやイベント駆動型プログラミングは、素晴らしく生産性の高い活動になりえますが、命令型アプローチと比較した場合の欠点として、デバッグが難しくなることがあります。

例えば、何かが起きない理由を突き止めるのは、トリックを知らなければ難しいことだ。

さて、そのコツはこうだ：

最初に使えるデバッグツールは `htmx.logAll()` メソッドです。これは htmx がトリガーするすべてのイベントをログに記録し、ライブラリが何をしているかを正確に見ることができます。

```javascript
htmx.logAll();
```

もちろん、なぜhtmxが*何も*していないのか、それはわかりません。また、トリガーとして使用するために、DOM要素が発火している*どんな*イベントかわからないかもしれません。これに対処するには、ブラウザのコンソールで利用できる [`monitorEvents()`](https://developers.google.com/web/updates/2015/05/quickly-monitor-events-from-the-console-panel) メソッドを使います：


```javascript
monitorEvents(htmx.find("#theElement"));
```

これは、`theElement`というidを持つ要素で発生しているすべてのイベントをコンソールに吐き出し、その要素で何が起こっているかを正確に見ることができる。

**Note** これはコンソールからしか動作しないので、ページのスクリプトタグに埋め込むことはできない。

最終的には、最小化されていないバージョンをロードして、`htmx.js`をデバッグすることもできる。約2500行のjavascriptなので、それほど膨大なコード量ではない。`issueAjaxRequest()`メソッドと`handleAjaxResponse()`メソッドにブレークポイントを設定して、何が起こっているのかを確認したい。

助けが必要なら、いつでも気軽に[Discord](https://htmx.org/discord)に飛び込んでくれ。

### デモの作成

時には、バグを実証したり、使い方を明確にするために、[jsfiddle](https://jsfiddle.net/)のようなjavascriptのスニペットサイトを利用できると良いでしょう。簡単にデモを作成するために、htmxはインストールするデモスクリプトサイトをホストしています：

* htmx
* hyperscript
* a request mocking library

以下のスクリプト・タグをあなたのdemo/fiddle/whateverに追加するだけです：

```html
<script src="https://demo.htmx.org"></script>
```

このヘルパーは `template` タグに `url` 属性でどのURLかを指定することで、モックレスポンスを追加することができます。そのURLに対するレスポンスはテンプレートのinnerHTMLになるので、簡単にモックレスポンスを構築することができる。`delay`属性は遅延させるミリ秒数を示す整数でなければなりません。

単純な式を`${}`構文でテンプレートに埋め込むことができます。

**Note** これはデモにのみ使用されるべきで、常に最新バージョンのhtmxとhyperscriptを取得するため、長期間の動作は保証されていないことに注意してください！

#### デモの例

以下はコードの例である：

```html
<!-- load demo environment -->
<script src="https://demo.htmx.org"></script>

<!-- post to /foo -->
<button hx-post="/foo" hx-target="#result">
    Count Up
</button>
<output id="result"></output>

<!-- respond to /foo with some dynamic content in a template tag -->
<script>
    globalInt = 0;
</script>
<template url="/foo" delay="500"> <!-- note the url and delay attributes -->
    ${globalInt++}
</template>
```

## スクリプト {#scripting}

htmxはウェブアプリケーションを構築するためのハイパーメディアアプローチを推奨していますが、クライアントのスクリプティングのための多くのオプションを提供しています。スクリプティングは、ウェブアーキテクチャのREST-fullの記述に含まれています：[Code-On-Demand](https://www.ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm#sec_5_1_7)を参照してください。可能な限り、ウェブアプリケーションのスクリプティングには[ハイパーメディアフレンドリー](/essays/hypermedia-friendly-scripting)なアプローチを推奨します：

* [Respect HATEOAS](/essays/hypermedia-friendly-scripting#prime_directive)
* [Use events to communicate between components](/essays/hypermedia-friendly-scripting#events)
* [Use islands to isolate non-hypermedia components from the rest of your application](/essays/hypermedia-friendly-scripting#islands)
* [Consider inline scripting](/essays/hypermedia-friendly-scripting#inline)

htmxとスクリプトソリューションの主な統合ポイントは、htmxが送信し、応答できる[event](#events)です。イベントを介してJavaScriptライブラリをhtmxと統合するための良いテンプレートは、[3rd Party Javascript](#3rd-party)セクションのSortableJSの例を参照してください。

htmxと相性の良いスクリプト・ソリューションには次のようなものがある：

* [VanillaJS](http://vanilla-js.com/) - htmxが発するイベントに応答するイベントハンドラをフックするために、JavaScriptの組み込み機能を使うだけで、スクリプティングは非常にうまくいきます。これは非常に軽量で、ますます人気のあるアプローチです。
* [AlpineJS](https://alpinejs.dev/) - Alpine.jsは、非常に軽量でありながら、リアクティブプログラミングのサポートを含む、洗練されたフロントエンドのスクリプトを作成するための豊富なツールセットを提供します。Alpineは、私たちがhtmxと相性が良いと感じている「インラインスクリプト」のアプローチを推奨しています。
* [jQuery](https://jquery.com/) - jQueryは古く、一部では評判になっているが、特にすでにjQueryが多く使われている古いコードベースでは、htmxとの相性は非常に良い。
* [hyperscript](https://hyperscript.org) - Hyperscriptは、htmxを作成した同じチームによって作成された実験的なフロントエンドスクリプト言語です。HTMLにうまく埋め込み、イベントに応答し、イベントを作成するように設計されており、htmxと非常によく組み合わされます。

[私たちの本](https://hypermedia.systems)には、["クライアントサイドスクリプティング"](https://hypermedia.systems/client-side-scripting/)という章があり、htmxベースのアプリケーションにスクリプティングをどのように統合できるかを見ています。

### <a name="hx-on"></a>[The `hx-on*` Attributes](#hx-on)

HTMLでは、`onClick`などの[`onevent`プロパティ](https://developer.mozilla.org/en-US/docs/Web/Events/Event_handlers#using_onevent_properties)を使ってインラインスクリプトを埋め込むことができます：

```html
<button onclick="alert('あなたは私をクリックした!')">
    Click Me!
</button>
```

この機能により、スクリプティングのロジックを、そのロジックが適用されるHTML要素と同位置に置くことができ、良好な[Locality of Behaviour (LoB)](/essays/locality-of-behaviour)を与えることができます。残念ながら、HTMLは決まった数の[特定のDOMイベント](https://www.w3schools.com/tags/ref_eventattributes.asp)(例えば`onclick`)に対してのみ`on*`属性を許可しており、要素上の任意のイベントに応答するための一般化されたメカニズムを提供していません。

この欠点に対処するために、htmxは [`hx-on*`](/attributes/hx-on) 属性を提供しています。これらの属性により、標準の `on*`プロパティの LoB を保持したまま、任意のイベントに応答することができます。

hx-on`属性を使って`click`イベントに反応させたい場合は、次のように書きます：

```html
<button hx-on:click="alert('あなたは私をクリックした!')">
    Click Me!
</button>
```

つまり、`hx-on`という文字列の後にコロン（またはダッシュ）、そしてイベント名を続ける。

もちろん `click` イベントでは、標準の `onclick` 属性を使用することを推奨します。しかし、htmx で動作するボタンが `htmx:config-request` イベントを使用してリクエストにパラメータを追加したいとします。これは標準の `on*` プロパティでは不可能ですが、`hx-on:htmx:config-request` 属性を使えば可能です：

```html
<button hx-post="/example"
        hx-on:htmx:config-request="event.detail.parameters.example = 'Hello Scripting!'">
    Post Me!
</button>
```

ここでは、`example` パラメータは `POST` リクエストが発行される前に、'Hello Scripting!を追加されます。

hx-on*`属性は一般化された組み込みスクリプトのための非常に単純なメカニズムです。これはAlpineJSやhyperscriptのような、より完全に開発されたフロントエンドのスクリプティングソリューションに取って代わるものではありません。しかし、VanillaJS ベースの htmx アプリケーションのスクリプティングのアプローチを補強することができます。

**Note** HTML属性は大文字と小文字を区別しません。これは、残念ながら、大文字/小文字に依存するイベントには応答できないことを意味します。キャメルケースのイベントをサポートする必要がある場合は、AlpineJS や hyperscript のような、より完全に機能するスクリプトソリューションを使用することをお勧めします。htmx は、このような理由から、すべてのイベントをキャメルケースとケバブケースの両方でディスパッチします。

### サードパーティとの統合 {#3rd-party}

Htmxはサードパーティライブラリとかなりうまく統合できます。ライブラリがDOM上でイベントを発生させる場合、htmxからのリクエストをトリガーするためにそれらのイベントを使用することができます。

この良い例が、[SortableJS demo](@/examples/sortable.md)です：

```html
<form class="sortable" hx-post="/items" hx-trigger="end">
    <div class="htmx-indicator">Updating...</div>
    <div><input type='hidden' name='item' value='1'/>Item 1</div>
    <div><input type='hidden' name='item' value='2'/>Item 2</div>
    <div><input type='hidden' name='item' value='2'/>Item 3</div>
</form>
```

Sortableでは、ほとんどのjavascriptライブラリと同様に、ある時点でコンテンツを初期化する必要があります。

jqueryでは次のようにする：

```javascript
$(document).ready(function() {
    var sortables = document.body.querySelectorAll(".sortable");
    for (var i = 0; i < sortables.length; i++) {
        var sortable = sortables[i];
        new Sortable(sortable, {
            animation: 150,
            ghostClass: 'blue-background-class'
        });
    }
});
```

htmxでは、代わりに`htmx.onLoad`関数を使い、ドキュメント全体ではなく、新しく読み込まれたコンテンツだけを選択することになる：

```js
htmx.onLoad(function(content) {
    var sortables = content.querySelectorAll(".sortable");
    for (var i = 0; i < sortables.length; i++) {
        var sortable = sortables[i];
        new Sortable(sortable, {
            animation: 150,
            ghostClass: 'blue-background-class'
        });
    }
})
```

これにより、htmxによって新しいコンテンツがDOMに追加されると、ソート可能な要素が適切に初期化されるようになる。

javascriptがhtmx属性を持つコンテンツをDOMに追加する場合、このコンテンツが`htmx.process()`関数で初期化されていることを確認する必要があります。

例えば、`fetch` APIを使ってデータをフェッチしてdivに入れ、そのHTMLにhtmx属性があった場合、次のように`htmx.process()`の呼び出しを追加する必要がある：

```js
let myDiv = document.getElementById('my-div')
fetch('http://example.com/movies.json')
    .then(response => response.text())
    .then(data => { myDiv.innerHTML = data; htmx.process(myDiv); } );
```

サードパーティのライブラリの中には、HTMLのテンプレート要素からコンテンツを作成するものがある。例えば、Alpine JSはテンプレートの `x-if`属性を使用して、条件付きでコンテンツを追加します。このようなテンプレートは初期状態ではDOMの一部ではなく、htmx属性を含んでいる場合は、ロード後に `htmx.process()`を呼び出す必要があります。次の例では、Alpineの`$watch`関数を使用して、条件付きコンテンツのトリガーとなる値の変化を探します：

```html
<div x-data="{show_new: false}"
    x-init="$watch('show_new', value => {
        if (show_new) {
            htmx.process(document.querySelector('#new_content'))
        }
    })">
    <button @click = "show_new = !show_new">Toggle New Content</button>
    <template x-if="show_new">
        <div id="new_content">
            <a hx-get="/server/newstuff" href="#">New Clickable</a>
        </div>
    </template>
</div>
```

#### ウェブコンポーネント {#web-components}

htmxとウェブコンポーネントを統合する方法については、[ウェブコンポーネントの例](@/examples/web-components.md)のページを参照してください。

## キャッシング {#caching}

htmxは、標準的な[HTTPキャッシュ](https://developer.mozilla.org/en-US/docs/Web/HTTP/Caching)メカニズムですぐに動作します。

サーバーがあるURLのレスポンスに[`Last-Modified`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Last-Modified) HTTPレスポンスヘッダを追加すると、ブラウザは同じURLへの次のリクエストに[`If-Modified-Since`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/If-Modified-Since) リクエストHTTPヘッダを自動的に追加します。もしサーバーが他のヘッダによって同じURLに対して異なるコンテンツをレンダリングできる場合、[`Vary`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Caching#vary) レスポンスHTTPヘッダを使う必要があることに注意してください。例えば、`HX-Request`ヘッダが無いか `false` のときは完全な HTML をレンダリングし、`HX-Request: true` のときはその HTML の断片をレンダリングする場合、`Vary: HX-Request` を追加する必要があります。そうすることで、キャッシュはレスポンスのURLと `HX-Request` リクエストヘッダの合成に基づいてキーが設定されます。

もし`Vary`ヘッダを使うことができない (または使いたくない) 場合は、代わりに `getCacheBusterParam` という設定パラメータを `true`に設定することができます。この設定変数が設定されると、htmx は`GET`リクエストにキャッシュバスターパラメータを含めるようになり、ブラウザが htmx ベースのレスポンスと非 htmx ベースのレスポンスを同じキャッシュスロットにキャッシュすることを防ぎます。

htmx は [`ETag`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/ETag) でも期待通りに動作します。サーバーが同じ URL に対して異なるコンテンツをレンダリングできる場合 (例えば `HX-Request` ヘッダーの値によって)、サーバーはそれぞれのコンテンツに対して異なる `ETag` を生成する必要があることに注意してください。

## セキュリティ {#security}

htmxでは、DOMに直接ロジックを定義することができます。これには多くの利点があり、最大の利点は[Locality of Behavior](@/essays/locality-of-behaviour.md)です。

htmxはHTMLの表現力を高めるので、悪意のあるユーザーがアプリケーションにHTMLを注入することができれば、htmxの表現力を悪意のある目的のために利用することができる。

### ルール1：すべてのユーザーコンテンツから逃れる

HTMLベースのウェブ開発の最初のルールは、常にこうだ：*ユーザーからの入力を信用しないこと。サイトに注入されるサードパーティの信頼できないコンテンツは、すべてエスケープする必要があります。これは、とりわけ[XSS攻撃](https://en.wikipedia.org/wiki/Cross-site_scripting)を防ぐためです。

優れた[OWASPウェブサイト](https://owasp.org/www-community/attacks/xss/)には、[クロスサイトスクリプティング防止チートシート](https://cheatsheetseries.owasp.org/cheatsheets/Cross_Site_Scripting_Prevention_Cheat_Sheet.html)を含め、XSSとその防止方法に関する広範な文書があります。

良いニュースは、これは非常に古く、よく理解されているトピックであり、サーバーサイドのテンプレート言語の大部分は、まさにこのような問題を防ぐために、コンテンツの[自動エスケープ](https://docs.djangoproject.com/en/4.2/ref/templates/language/#automatic-html-escaping)をサポートしているということです。

とはいえ、もっと危険なHTMLを注入することを選択する場合もあります。多くの場合、テンプレート言語にある種の `raw()` メカニズムを使う。これは正当な理由によるものだが、もし注入されるコンテンツがサードパーティから来たものであれば、`hx-`や`data-hx`で始まる属性や、インラインの`<script>`タグなどの削除も含めて、洗浄し*なければならない*。

生のHTMLを注入し、独自のエスケープを行う場合、ベストプラクティスは、許可しないものをブラックリストに入れるのではなく、許可する属性やタグを*ホワイトリスト*に入れることである。

### htmxセキュリティツール

もちろん、バグは起こりますし、開発者も完璧ではありません。ですから、Webアプリケーションのセキュリティに対して重層的なアプローチをとることは良いことです。

それでは見てみよう。

#### `hx-disable`

アプリケーションの安全性を高めるために htmx が提供する最初のツールは [`hx-disable`](/attributes/hx-disable) 属性です。この属性は、与えられた要素やその中のすべての要素に対して、すべての htmx 属性の処理を防ぎます。したがって、例えば、テンプレートに生のHTMLコンテンツを含める場合（これも推奨されません！）、`hx-disable`属性でコンテンツを囲むdivを配置することができます：

```html
<div hx-disable>
    <%= raw(user_content) %>
</div>
```

また、htmx はそのコンテンツで見つかった htmx 関連の属性や機能を処理しません。要素の親階層のどこかに `hx-disable` 属性がある場合、htmx はその属性を処理しません。

#### `hx-history`

もうひとつのセキュリティ上の考慮点は htmx の履歴キャッシュです。ユーザーの `localStorage` キャッシュに保存されたくない機密データを含むページがあるかもしれません。 [`hx-history`](/attributes/hx-history)属性をページの任意の場所に記述し、その値を `false` に設定することで、特定のページを履歴キャッシュから省くことができます。

#### 設定オプション {#configuration-options}

htmxはセキュリティに関する設定オプションも提供している：

* `htmx.config.selfRequestsOnly` - `true`に設定すると、現在のドキュメントと同じドメインへのリクエストのみが許可される。
* `htmx.config.allowScriptTags` - htmxは新しいコンテンツを読み込んだときに見つかった `<script>` タグを処理します。この動作を無効にしたい場合はこの設定変数を `false` に設定してください。
* `htmx.config.historyCacheSize` - `0` に設定すると、HTMLを `localStorage` キャッシュに保存しない。
* `htmx.config.allowEval` - `false` に設定すると、eval に依存する htmx のすべての機能を無効にすることができる：
  * イベントフィルター
  * `hx-on:`属性
  * `hx-vals`に`js:`接頭辞をつける
  * `hx-headers`に`js:`接頭辞をつける

**Note** `eval()`を無効にすることで削除されるすべての機能は、あなた自身のカスタムjavascriptとhtmxイベントモデルを使用して再実装することができます。

#### イベント

現在のホスト以外のドメインへのリクエストを許可したいが、完全にオープンな状態にはしたくない場合は、`htmx:validateUrl`イベントを使用することができます。このイベントでは `detail.url` スロットにリクエストURLと `sameHost` プロパティを指定することができます。

これらの値を検査し、リクエストが有効でなければ、イベントに対して `preventDefault()` を呼び出して、リクエストが発行されないようにすることができる。

```javascript
document.body.addEventListener('htmx:validateUrl', function (evt) {
  // only allow requests to the current server as well as myserver.com
  if (!evt.detail.sameHost && evt.detail.url.hostname !== "myserver.com") {
    evt.preventDefault();
  }
});
```

### CSPオプション

ブラウザはまた、ウェブアプリケーションをより安全にするためのツールも提供しています。最も強力なツールは[Content Security Policy](https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP)です。CSPを使うことで、例えば、オリジンでないホストへのリクエストを発行しない、インラインスクリプトタグを評価しない、などをブラウザに指示することができます。

以下は`meta`タグ内のCSPの例である：

```html
    <meta http-equiv="Content-Security-Policy" content="default-src 'self';">
```

これはブラウザに「オリジナル(ソース)ドメインへの接続のみを許可する」ことを伝えます。これは`htmx.config.selfRequestsOnly`と冗長ですが、アプリケーションのセキュリティを扱う場合、セキュリティに対する階層的なアプローチは正当であり、実際、理想的です。

CSPについての完全な議論はこのドキュメントの範囲を超えているが、[MDN Article](https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP) はこのトピックを探求するための良いジャンプ・ポイントを提供してくれる。

## htmxの設定 {#config}

Htmxには、プログラム的または宣言的にアクセスできるいくつかの設定オプションがあります。以下にその一覧を示します：

<div class="info-table">

| 設定変数                               | インフォメーション                                       |
|---------------------------------------|-------------------------------------------------------|
| `htmx.config.historyEnabled`          | デフォルトは `true` で、テストにしか使えない。
| `htmx.config.historyCacheSize`        | デフォルトは 10
| `htmx.config.refreshOnHistoryMiss`    | デフォルトは `false` で、`true` に設定すると htmx は AJAX リクエストを使わず、履歴が消えたときに全ページを更新する。
| `htmx.config.defaultSwapStyle`        | デフォルトは `innerHTML`
| `htmx.config.defaultSwapDelay`        | デフォルトは 0
| `htmx.config.defaultSettleDelay`      | デフォルトは 20
| `htmx.config.includeIndicatorStyles`  | デフォルトは `true` (インジケータのスタイルを読み込むかどうかを決定する) 
| `htmx.config.indicatorClass`          | デフォルトは `htmx-indicator` である。
| `htmx.config.requestClass`            | デフォルトは `htmx-request` である。
| `htmx.config.addedClass`              | デフォルトは `htmx-added` である。
| `htmx.config.settlingClass`           | デフォルトは `htmx-settling` である。
| `htmx.config.swappingClass`           | デフォルトは `htmx-swapping` である。
| `htmx.config.allowEval`               | デフォルトは `true` で、特定の機能 (例えばトリガーフィルター) に対して htmx が eval を使用するのを無効にするのに使用する。
| `htmx.config.allowScriptTags`         | デフォルトは `true` で、htmx が新しいコンテンツで見つかったスクリプトタグを処理するかどうかを決定する。
| `htmx.config.inlineScriptNonce`       | デフォルトは `''` で、インラインスクリプトにnonceが追加されないことを意味する。
| `htmx.config.attributesToSettle`      | デフォルトは`["class", "style", "width", "height"]`で、セトリング段階でセトリングする属性。
| `htmx.config.inlineStyleNonce`        | デフォルトは `''` で、インラインスタイルに nonce が追加されない。
| `htmx.config.useTemplateFragments`    | デフォルトは `false`, サーバからのコンテンツを解析するためのHTMLテンプレートタグ (IE11には対応していません!)
| `htmx.config.wsReconnectDelay`        | デフォルトは `full-jitter` である。                
| `htmx.config.wsBinaryType`            | デフォルトは `blob` で、WebSocket 接続で受信される [バイナリデータの型](https://developer.mozilla.org/docs/Web/API/WebSocket/binaryType) である。
| `htmx.config.disableSelector`         | デフォルトは `[hx-disable], [data-hx-disable]` で、htmx はこの属性を持つ要素や親要素を処理しません。
| `htmx.config.withCredentials`         | デフォルトは `false` で、クッキー、認証ヘッダー、TLS クライアント証明書などのクレデンシャルを使ったクロスサイトアクセス制御リクエストを許可する。
| `htmx.config.timeout`                 | デフォルトは 0 で、リクエストが自動的に終了するまでのミリ秒数
| `htmx.config.scrollBehavior`          | デフォルトを'smooth'に設定することで、ページ遷移時のブーストリンクの動作を指定します。指定できる値は `auto` と `smooth` です。smoothはページの一番上までスムーススクロールし、autoはバニラリンクのように動作する。
| `htmx.config.defaultFocusScroll`      | デフォルトはfalseで、[focus-scroll](@/attributes/hx-swap.md#focus-scroll) swap修飾子を使って上書きできます。
| `htmx.config.getCacheBusterParam`     | デフォルトは false で、true に設定すると htmx は `org.htmx.cache-buster=targetElementId` という形式で `GET` リクエストにターゲット要素を追加します。
| `htmx.config.globalViewTransitions`   | `true` に設定すると、htmx は新しいコンテンツを入れ替えるときに [View Transition](https://developer.mozilla.org/en-US/docs/Web/API/View_Transitions_API) API を使用します。
| `htmx.config.methodsThatUseUrlParams` | デフォルトは `["get"]` で、htmx はこれらのメソッドのリクエストを、リクエストボディではなく URL にエンコードしてフォーマットします。
| `htmx.config.selfRequestsOnly`        | デフォルトは `true`, 現在のドキュメントと同じドメインへのAJAXリクエストのみを許可するかどうか。
| `htmx.config.ignoreTitle`             | デフォルトは `false` で、`true` に設定すると htmx は新しいコンテンツに `title` タグがあってもドキュメントのタイトルを更新しない。
| `htmx.config.disableInheritance`      | htmxの属性継承を無効にし、[`hx-inherit`](@/attributes/hx-inherit.md)属性で上書きできるようにする。
| `htmx.config.scrollIntoViewOnBoost`   | デフォルトは `true` で、ブーストされた要素のターゲットがビューポートにスクロールされるかどうかを指定する。boosted 要素で `hx-target` が省略された場合、ターゲットのデフォルトは `body` となり、ページが一番上にスクロールされる。
| `htmx.config.triggerSpecsCache`       | デフォルトは `null` で、評価されたトリガ指定を格納するキャッシュです。クリアされないキャッシュを使用する単純なオブジェクトを定義するか、[プロキシオブジェクト](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Proxy)を使用して独自のシステムを実装することができます。
| `htmx.config.allowNestedOobSwaps`     | デフォルトは `true` で、メインのレスポンス要素の中に入れ子になっている要素の OOB スワップを処理するかどうかを指定します。[入れ子のOOBスワップ](@/attributes/hx-swap-oob.md#nested-oob-swaps)を参照してください。

</div>

javascriptで直接設定することもできるし、`meta`タグを使うこともできる：

```html
<meta name="htmx-config" content='{"defaultSwapStyle":"outerHTML"}'>
```

## 結論

それで終わりだ！

htmxを楽しんでください！たくさんのコードを書かなくても、[かなりのこと](@/examples/_index.md)を達成することができます！

</div>
</div>
