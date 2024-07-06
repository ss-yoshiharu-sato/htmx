+++
title = "リファレンス"
[extra]
custom_classes = "wide-content"
+++
<div class="row">
<div class="2 col nav">

**目次**

<div id="contents">

* htmx
  * [Core Attributes](#attributes)
  * [Additional Attributes](#attributes-additional)
  * [CSS Classes](#classes)
  * [Request Headers](#request_headers)
  * [Response Headers](#response_headers)
  * [Events](#events)
  * [Extensions](#extensions)
* [JavaScript API](#api)
* [Configuration Options](#config)

</div>

</div>
<div class="10 col">

## コア属性リファレンス {#attributes}

htmxを使用する際に最も一般的な属性。

<div class="info-table">

| 属性                                             | 説明                                                                |
|--------------------------------------------------|--------------------------------------------------------------------|
| [`hx-get`](@/attributes/hx-get.md)               | 指定されたURLに `GET` を発行する。|
| [`hx-post`](@/attributes/hx-post.md)             | 指定されたURLに `POST` を送信する。|
| [`hx-on*`](@/attributes/hx-on.md)                | 要素上のインライン・スクリプトでイベントを処理する|
| [`hx-push-url`](@/attributes/hx-push-url.md)     | URLをブラウザのロケーションバーにプッシュして履歴を作成する。|
| [`hx-select`](@/attributes/hx-select.md)         | レスポンスから入れ替えるコンテンツを選択する。|
| [`hx-select-oob`](@/attributes/hx-select-oob.md) | ターゲット（帯域外）以外の場所で、レスポンスから入れ替えるコンテンツを選択する。|
| [`hx-swap`](@/attributes/hx-swap.md)             | コンテンツがどのように入れ替わるかを制御する (`outerHTML`、`beforeend`、`afterend` など)|
| [`hx-swap-oob`](@/attributes/hx-swap-oob.md)     | 回答から入れ替えるマーク要素（帯域外）|
| [`hx-target`](@/attributes/hx-target.md)         | スワップする対象要素を指定する|
| [`hx-trigger`](@/attributes/hx-trigger.md)       | リクエストのトリガーとなるイベントを指定する|
| [`hx-vals`](@/attributes/hx-vals.md)             | リクエストと一緒に送信する値を追加する（JSON形式）|

</div>

## 追加属性リファレンス {#attributes-additional}

htmxで利用可能な他のすべての属性。

<div class="info-table">

| 属性                                                 | 説明                                                      |
|------------------------------------------------------|----------------------------------------------------------|
| [`hx-boost`](@/attributes/hx-boost.md)               | リンクとフォームに[プログレッシブ・エンハンスメント](https://ja.wikipedia.org/wiki/%E3%83%97%E3%83%AD%E3%82%B0%E3%83%AC%E3%83%83%E3%82%B7%E3%83%96%E3%82%A8%E3%83%B3%E3%83%8F%E3%83%B3%E3%82%B9%E3%83%A1%E3%83%B3%E3%83%88)を追加。|
| [`hx-confirm`](@/attributes/hx-confirm.md)           | リクエストを発行する前に `confirm()` ダイアログを表示する。|
| [`hx-delete`](@/attributes/hx-delete.md)             | 指定されたURLに対して `DELETE` を発行する。|
| [`hx-disable`](@/attributes/hx-disable.md)           | 指定されたノードと子ノードの htmx 処理を無効にする。|
| [`hx-disabled-elt`](@/attributes/hx-disabled-elt.md) | リクエストの処理中に、指定した要素に `disabled` 属性を追加する。|
| [`hx-disinherit`](@/attributes/hx-disinherit.md)     | 子ノードの自動属性継承の制御と無効化|
| [`hx-encoding`](@/attributes/hx-encoding.md)         | リクエストのエンコーディング・タイプを変更する|
| [`hx-ext`](@/attributes/hx-ext.md)                   | この要素に使用する拡張子|
| [`hx-headers`](@/attributes/hx-headers.md)           | リクエストとともに送信されるヘッダに追加されます。|
| [`hx-history`](@/attributes/hx-history.md)           | 機密データが履歴キャッシュに保存されるのを防ぐ|
| [`hx-history-elt`](@/attributes/hx-history-elt.md)   | ヒストリーナビゲーション中にスナップショットおよびリストアする要素。|
| [`hx-include`](@/attributes/hx-include.md)           | リクエストに追加データを含める|
| [`hx-indicator`](@/attributes/hx-indicator.md)       | リクエスト時に `htmx-request` クラスを置く要素。|
| [`hx-inherit`](@/attributes/hx-inherit.md)           | デフォルトで無効になっている場合、子ノードの自動属性継承を制御し、有効にする。|
| [`hx-params`](@/attributes/hx-params.md)             | リクエストとともに送信されるパラメータをフィルタリングする|
| [`hx-patch`](@/attributes/hx-patch.md)               | 指定されたURLに `PATCH` を発行する。|
| [`hx-preserve`](@/attributes/hx-preserve.md)         | リクエスト間で変更しない要素を指定する|
| [`hx-prompt`](@/attributes/hx-prompt.md)             | リクエストを送信する前に `prompt()` を表示する。|
| [`hx-put`](@/attributes/hx-put.md)                   | 指定されたURLに `PUT` を発行する。|
| [`hx-replace-url`](@/attributes/hx-replace-url.md)   | ブラウザのロケーションバーのURLを置き換える|
| [`hx-request`](@/attributes/hx-request.md)           | リクエストのさまざまな側面を設定する|
| [`hx-sync`](@/attributes/hx-sync.md)                 | 異なるエレメントからのリクエストをどのように同期させるかを制御する|
| [`hx-validate`](@/attributes/hx-validate.md)         | リクエストの前に要素を強制的にバリデートさせる|
| [`hx-vars`](@/attributes/hx-vars.md)                 | リクエストと一緒に送信するパラメータに動的に値を追加する(非推奨。[`hx-vals`](@/attributes/hx-vals.md) を使ってください)|

</div>

## CSSクラス リファレンス {#classes}

<div class="info-table">

| クラス            | 説明                                                                        |
|------------------|-----------------------------------------------------------------------------|
| `htmx-added`     | 交換前の新しいコンテンツに適用され、決済後に削除される。|
| `htmx-indicator` | `htmx-request` クラスが存在するときに可視 (opacity:1) になるように動的に生成されるクラス。|
| `htmx-request`   | リクエストの実行中に、[`hx-indicator`](@/attributes/hx-indicator.md) で指定された要素に適用される。|
| `htmx-settling`  | コンテンツが入れ替わった後にターゲットに適用され、決済された後に削除されます。継続時間は [`hx-swap`](@/attributes/hx-swap.md) で変更できます。|
| `htmx-swapping`  | 内容が入れ替わる前に対象に適用され、入れ替わった後に削除されます。継続時間は [`hx-swap`](@/attributes/hx-swap.md) で変更できます。|

</div>

## HTTPヘッダー リファレンス {#headers}

### リクエストヘッダ リファレンス {#request_headers}

<div class="info-table">

| ヘッダ                        | 説明                                                           |
|------------------------------|----------------------------------------------------------------|
| `HX-Boosted`                 | [hx-boost](@/attributes/hx-boost.md)を使った要素経由のリクエストであることを示します。|
| `HX-Current-URL`             | ブラウザの現在のURL|
| `HX-History-Restore-Request` | ローカル履歴キャッシュにミスがあった後の履歴復元リクエストであれば "true"|
| `HX-Prompt`                  | [hx-prompt](@/attributes/hx-prompt.md)に対するユーザーの応答。|
| `HX-Request`                 | 常に "true"|
| `HX-Target`                  | ターゲット要素が存在すれば、その `id` を指定する。|
| `HX-Trigger-Name`            | トリガーされた要素が存在する場合、その要素の `name` を指定する。|
| `HX-Trigger`                 | トリガーされた要素の `id` が存在する場合、それを指定する。|

</div>

### レスポンス ヘッダ リファレンス {#response_headers}

<div class="info-table">

| ヘッダ                                                | 説明                                                    |
|------------------------------------------------------|---------------------------------------------------------|
| [`HX-Location`](@/headers/hx-location.md)            | これにより、全ページのリロードを行わないクライアントサイドのリダイレクトが可能になる。|
| [`HX-Push-Url`](@/headers/hx-push-url.md)            | 新しいurlを履歴スタックにプッシュする|
| `HX-Redirect`                                        | クライアント側で新しい場所にリダイレクトすることができる。|
| `HX-Refresh`                                         | "true"に設定された場合、クライアント側はページの完全な更新を行う。|
| [`HX-Replace-Url`](@/headers/hx-replace-url.md)      | ロケーションバーの現在のURLを置き換える|
| `HX-Reswap`                                          | レスポンスがどのようにスワップされるかを指定することができます。指定できる値については [hx-swap](@/attributes/hx-swap.md) を参照してください。|
| `HX-Retarget`                                        | コンテンツ更新のターゲットをページ上の別の要素に更新するCSSセレクタ。|
| `HX-Reselect`                                        | レスポンスのどの部分を入れ替えるかを選択できる CSS セレクタです。既存の[`hx-select`](@/attributes/hx-select.md)を上書きします。|
| [`HX-Trigger`](@/headers/hx-trigger.md)              | クライアント側のイベントをトリガーできる|
| [`HX-Trigger-After-Settle`](@/headers/hx-trigger.md) | これにより、決済ステップの後にクライアントサイドのイベントをトリガーすることができます。|
| [`HX-Trigger-After-Swap`](@/headers/hx-trigger.md)   | スワップ・ステップの後にクライアント側イベントをトリガーすることができる。|

</div>

## イベント リファレンス {#events}

<div class="info-table">

| イベント | 説明 |
|--------|-------------|
| [`htmx:abort`](@/events.md#htmx:abort) | リクエストを中止するために、このイベントを要素に送信する。|
| [`htmx:afterOnLoad`](@/events.md#htmx:afterOnLoad) | AJAXリクエストが成功したレスポンスの処理を完了した後にトリガーされる。|
| [`htmx:afterProcessNode`](@/events.md#htmx:afterProcessNode) | htmxがノードを初期化した後にトリガーされる。|
| [`htmx:afterRequest`](@/events.md#htmx:afterRequest)  | AJAXリクエストが完了した後にトリガーされる|
| [`htmx:afterSettle`](@/events.md#htmx:afterSettle)  | DOMが落ち着いてから発動|
| [`htmx:afterSwap`](@/events.md#htmx:afterSwap)  | 新しいコンテンツが入れ替わった後にトリガーされる|
| [`htmx:beforeCleanupElement`](@/events.md#htmx:beforeCleanupElement)  | htmx [disables](@/attributes/hx-disable.md)が要素を無効にしたり、DOMから取り除いたりする前に発生する。|
| [`htmx:beforeOnLoad`](@/events.md#htmx:beforeOnLoad)  | 応答処理が行われる前にトリガーされる|
| [`htmx:beforeProcessNode`](@/events.md#htmx:beforeProcessNode) | htmxがノードを初期化する前にトリガされる。|
| [`htmx:beforeRequest`](@/events.md#htmx:beforeRequest)  | AJAXリクエストが行われる前にトリガーされる。|
| [`htmx:beforeSwap`](@/events.md#htmx:beforeSwap)  | スワップが実行される前にトリガーされる。|
| [`htmx:beforeSend`](@/events.md#htmx:beforeSend)  | ajaxリクエストが送信される直前にトリガーされる|
| [`htmx:configRequest`](@/events.md#htmx:configRequest)  | リクエストの前にトリガーされ、パラメータやヘッダーをカスタマイズすることができます。|
| [`htmx:confirm`](@/events.md#htmx:confirm)  | 要素上でトリガーが発生した後にトリガーされた場合、AJAXリクエストの発行をキャンセル（または遅延）することができます。|
| [`htmx:historyCacheError`](@/events.md#htmx:historyCacheError)  | キャッシュ書き込み中のエラーで発生|
| [`htmx:historyCacheMiss`](@/events.md#htmx:historyCacheMiss)  | 履歴サブシステムのキャッシュ・ミスでトリガーされる。|
| [`htmx:historyCacheMissError`](@/events.md#htmx:historyCacheMissError)  | リモート検索に失敗した場合に発生|
| [`htmx:historyCacheMissLoad`](@/events.md#htmx:historyCacheMissLoad)  | リモート検索成功時にトリガーされる|
| [`htmx:historyRestore`](@/events.md#htmx:historyRestore)  | htmxが履歴の復元アクションを処理するときにトリガーされる|
| [`htmx:beforeHistorySave`](@/events.md#htmx:beforeHistorySave)  | コンテンツが履歴キャッシュに保存される前にトリガーされる|
| [`htmx:load`](@/events.md#htmx:load)  | 新しいコンテンツがDOMに追加されたときにトリガーされる|
| [`htmx:noSSESourceError`](@/events.md#htmx:noSSESourceError)  | 要素がそのトリガーでSSEイベントを参照しているが、親SEソースが定義されていない場合にトリガーされる。|
| [`htmx:onLoadError`](@/events.md#htmx:onLoadError)  | htmxのonLoad処理中に例外が発生したときにトリガーされる。|
| [`htmx:oobAfterSwap`](@/events.md#htmx:oobAfterSwap)  | 帯域外のエレメントが入れ替わった後にトリガーされる|
| [`htmx:oobBeforeSwap`](@/events.md#htmx:oobBeforeSwap)  | 帯域外エレメントのスワップが行われる前にトリガーされ、スワップを設定できる。|
| [`htmx:oobErrorNoTarget`](@/events.md#htmx:oobErrorNoTarget)  | 帯域外の要素が現在のDOMに一致するIDを持たない場合にトリガーされる。|
| [`htmx:prompt`](@/events.md#htmx:prompt)  | プロンプトが表示された後に発動|
| [`htmx:pushedIntoHistory`](@/events.md#htmx:pushedIntoHistory)  | urlが履歴にプッシュされた後にトリガーされる|
| [`htmx:responseError`](@/events.md#htmx:responseError)  | HTTP レスポンスエラー (レスポンスコード `200` または `300` 以外) が発生したときにトリガーされます。|
| [`htmx:sendError`](@/events.md#htmx:sendError)  | ネットワークエラーによりHTTPリクエストが発生しない場合に発生|
| [`htmx:sseError`](@/events.md#htmx:sseError)  | SSEソースでエラーが発生したときにトリガーされる。|
| [`htmx:sseOpen`](/events#htmx:sseOpen)  | SSEソースがオープンされるとトリガーされる。|
| [`htmx:swapError`](@/events.md#htmx:swapError)  | スワップ・フェーズ中にエラーが発生した場合にトリガーされる。|
| [`htmx:targetError`](@/events.md#htmx:targetError)  | 無効なターゲットが指定されたときにトリガーされる|
| [`htmx:timeout`](@/events.md#htmx:timeout)  | リクエストタイムアウト発生時|
| [`htmx:validation:validate`](@/events.md#htmx:validation:validate)  | 要素が検証される前にトリガされる|
| [`htmx:validation:failed`](@/events.md#htmx:validation:failed)  | 要素がバリデーションに失敗したときに発生する|
| [`htmx:validation:halted`](@/events.md#htmx:validation:halted)  | バリデーションエラーによりリクエストが停止した場合に発生する|
| [`htmx:xhr:abort`](@/events.md#htmx:xhr:abort)  | ajaxリクエストがアボートしたときにトリガーされる|
| [`htmx:xhr:loadend`](@/events.md#htmx:xhr:loadend)  | ajaxリクエストが終了したときにトリガーされる|
| [`htmx:xhr:loadstart`](@/events.md#htmx:xhr:loadstart)  | ajaxリクエストが開始されたときにトリガーされる|
| [`htmx:xhr:progress`](@/events.md#htmx:xhr:progress)  | 進捗イベントをサポートするajaxリクエスト中に定期的にトリガーされる。|

</div>

## Extensions {#extensions}
外部サイトへ [Extensions](https://extensions.htmx.org) 

## JavaScript API リファレンス {#api}

<div class="info-table">

| メソッド | 説明 |
|-------|-------------|
| [`htmx.addClass()`](@/api.md#addClass)  | 与えられた要素にクラスを追加する。 |
| [`htmx.ajax()`](@/api.md#ajax)  | htmx 形式の ajax リクエストを発行する。 |
| [`htmx.closest()`](@/api.md#closest)  | セレクタにマッチする、与えられた要素に最も近い親を見つける。|
| [`htmx.config`](@/api.md#config)  | 現在の htmx config オブジェクトを保持するプロパティ。|
| [`htmx.createEventSource`](@/api.md#createEventSource)  | htmx 用の SSE EventSource オブジェクトを作成する関数を保持するプロパティ。|
| [`htmx.createWebSocket`](@/api.md#createWebSocket)  | htmx 用の WebSocket オブジェクトを作成する関数を保持するプロパティ。|
| [`htmx.defineExtension()`](@/api.md#defineExtension)  | htmx [Extension](https://extensions.htmx.org) を定義します。|
| [`htmx.find()`](@/api.md#find)  | セレクタにマッチする単一の要素を検索します。|
| [`htmx.findAll()` `htmx.findAll(elt, selector)`](@/api.md#find)  | 与えられたセレクタにマッチするすべての要素を検索する。|
| [`htmx.logAll()`](@/api.md#logAll)  | すべての htmx イベントを記録するロガーをインストールします。|
| [`htmx.logger`](@/api.md#logger)  | 現在のロガーに設定されるプロパティ (デフォルトは `null`)|
| [`htmx.off()`](@/api.md#off)  | 与えられた要素からイベントリスナーを削除する。|
| [`htmx.on()`](@/api.md#on)  | 与えられた要素にイベントリスナーを作成し、それを返す。|
| [`htmx.onLoad()`](@/api.md#onLoad)  | `htmx:load` イベントのコールバックハンドラを追加する。|
| [`htmx.parseInterval()`](@/api.md#parseInterval)  | インターバル宣言をミリ秒値にパースする。\
| [`htmx.process()`](@/api.md#process)  | 与えられた要素とその子を処理し、あらゆる htmx の動作をフックする。|
| [`htmx.remove()`](@/api.md#remove)  | 与えられた要素を削除する。|
| [`htmx.removeClass()`](@/api.md#removeClass)  | 与えられた要素からクラスを削除します。|
| [`htmx.removeExtension()`](@/api.md#removeExtension)  | htmx [拡張子](https://extensions.htmx.org) を削除する。|
| [`htmx.swap()`](@/api.md#swap)  | HTMLコンテンツのスワップ（およびセトリング）を実行する。|
| [`htmx.takeClass()`](@/api.md#takeClass)  | 与えられた要素に対して、他の要素からクラスを取る。|
| [`htmx.toggleClass()`](@/api.md#toggleClass)  | 与えられた要素からクラスを切り替える。|
| [`htmx.trigger()`](@/api.md#trigger)  | 要素にイベントをトリガーする。｜
| [`htmx.values()`](@/api.md#values)  | 与えられた要素に関連付けられた入力値を返す。|

</div>

## 設定リファレンス {#config}

Htmxには、プログラム的または宣言的にアクセスできるいくつかの設定オプションがあります。以下にその一覧を示します：

<div class="info-table">

| 設定変数                               | 情報                                 |
|---------------------------------------|-------------------------------------|
| `htmx.config.historyEnabled`          | デフォルトは `true` で、テストにしか使えない。|
| `htmx.config.historyCacheSize`        | デフォルトは 10|
| `htmx.config.refreshOnHistoryMiss`    | デフォルトは `false` で、`true` に設定すると htmx は AJAX リクエストを使わず、履歴が消えたときに全ページを更新する。|
| `htmx.config.defaultSwapStyle`        | デフォルトは `innerHTML` である。|
| `htmx.config.defaultSwapDelay`        | デフォルトは 0|
| `htmx.config.defaultSettleDelay`      | デフォルトは 20|
| `htmx.config.includeIndicatorStyles`  | デフォルトは `true` (インジケータのスタイルを読み込むかどうかを決定する)|
| `htmx.config.indicatorClass`          | デフォルトは `htmx-indicator` である。|
| `htmx.config.requestClass`            | デフォルトは `htmx-request` である。|
| `htmx.config.addedClass`              | デフォルトは `htmx-added` である。|
| `htmx.config.settlingClass`           | デフォルトは `htmx-settling` である。|
| `htmx.config.swappingClass`           | デフォルトは `htmx-swapping` である。|
| `htmx.config.allowEval`               | デフォルトは `true` で、特定の機能 (例えばトリガーフィルター) に対して htmx が eval を使用するのを無効にするのに使用する。|
| `htmx.config.allowScriptTags`         | デフォルトは `true` で、htmx が新しいコンテンツで見つかったスクリプトタグを処理するかどうかを決定する。|
| `htmx.config.inlineScriptNonce`       | デフォルトは `''` で、インラインスクリプトにnonceが追加されないことを意味する。|
| `htmx.config.inlineSlyeNonce`         | デフォルトは `''` で、インラインスタイルに nonce が追加されない。|
| `htmx.config.attributesToSettle`      | デフォルトは`["class", "style", "width", "height"]`で、セトリング段階でセトリングする属性。|
| `htmx.config.wsReconnectDelay`        | デフォルトは `full-jitter` である。|
| `htmx.config.wsBinaryType`            | デフォルトは `blob` で、WebSocket 接続で受信される [バイナリデータのタイプ](https://developer.mozilla.org/docs/Web/API/WebSocket/binaryType) である。|
| `htmx.config.disableSelector`         | デフォルトは `[hx-disable], [data-hx-disable]` で、htmx はこの属性を持つ要素や親要素を処理しません。|
| `htmx.config.withCredentials`         | デフォルトは `false` で、クッキー、認証ヘッダー、TLS クライアント証明書などのクレデンシャルを使ったクロスサイトアクセス制御リクエストを許可する。|
| `htmx.config.timeout`                 | デフォルトは 0 で、リクエストが自動的に終了するまでのミリ秒数|
| `htmx.config.scrollBehavior`          | デフォルトは'smooth'で、ページ遷移時のブーストリンクの動作になります。指定できる値は `auto` と `smooth` です。smoothはページの一番上までスムーススクロールし、autoはバニラリンクのように動作する。|
| `htmx.config.defaultFocusScroll`      | デフォルトはfalseで、[focus-scroll](@/attributes/hx-swap.md#focus-scroll) swap修飾子を使って上書きできます。|
| `htmx.config.getCacheBusterParam`     | デフォルトは false で、true に設定すると htmx は `org.htmx.cache-buster=targetElementId` という形式で `GET` リクエストにターゲット要素を追加します。|
| `htmx.config.globalViewTransitions`   | `true` に設定すると、htmx は新しいコンテンツを入れ替えるときに [View Transition](https://developer.mozilla.org/en-US/docs/Web/API/View_Transitions_API) API を使用します。|
| `htmx.config.methodsThatUseUrlParams` | デフォルトは `["get"]` で、htmx はこれらのメソッドのリクエストを、リクエストボディではなく URL にエンコードしてフォーマットします。|
| `htmx.config.selfRequestsOnly`        | デフォルトは `true`, 現在のドキュメントと同じドメインへのAJAXリクエストのみを許可するかどうか。|
| `htmx.config.ignoreTitle`             | デフォルトは `false` で、`true` に設定すると htmx は新しいコンテンツに `title` タグがあってもドキュメントのタイトルを更新しない。|
| `htmx.config.scrollIntoViewOnBoost`   | デフォルトは `true` で、ブーストされた要素のターゲットがビューポートにスクロールされるかどうかを指定する。boosted 要素で `hx-target` が省略された場合、ターゲットのデフォルトは `body` となり、ページが一番上にスクロールされる。|
| `htmx.config.triggerSpecsCache`       | デフォルトは `null` で、評価されたトリガ指定を格納するキャッシュです。クリアされないキャッシュを使用する単純なオブジェクトを定義するか、[プロキシオブジェクト](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Proxy)を使用して独自のシステムを実装することができます。 |
| `htmx.config.allowNestedOobSwaps`     | デフォルトは `true` で、メインのレスポンス要素の中に入れ子になっている要素の OOB スワップを処理するかどうかを指定します。[入れ子のOOBスワップ](@/attributes/hx-swap-oob.md#nested-oob-swaps)を参照してください。|

</div>

javascriptで直接設定することもできるし、`meta`タグを使うこともできる：

```html
<meta name="htmx-config" content='{"defaultSwapStyle":"outerHTML"}'>
```

</div>
</div>