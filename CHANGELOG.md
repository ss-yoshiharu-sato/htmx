# Changelog

## [2.0.0] - 2024-06-17

* エクステンションを削除し、<https://extensions.htmx.org>からリンクされた独自のリポジトリに移動した。
* ウェブサイトがダークモードに対応しました！(ありがとう！[@pokonski](https://github.com/pokonski))
* 古い非推奨の[SSE & WS](https://v1.htmx.org/docs/#websockets-and-sse)属性は削除された。
* [ウェブ・コンポーネントとシャドウDOM](https://htmx.org/examples/web-components/)のサポート向上
* HTTP `DELETE`リクエストのペイロードに、フォームエンコードされたボディではなく、パラメータを使うようになった（これは仕様に従っている）。
* モジュール・サポートは異なるファイルに分割された：
* 様々なJavaScriptモジュールのスタイルについて、`/dist`に特定のファイルを提供するようになった：
  * ESM Modules: `/dist/htmx.esm.js`
  * AMD Modules: `/dist/htmx.amd.js`
  * CJS Modules: `/dist/htmx.cjs.js`
  * `dist/htmx.js`ファイルは引き続きブラウザからロード可能です。
* 特殊な構文を持つ `hx-on` 属性は削除され、より扱いにくい `hx-on:` 構文が採用された。
* アップグレード手順の詳細については、[アップグレードガイド](https://htmx.org/migration-guide-htmx-1/) を参照してください。
* 内部APIメソッド `selectAndSwap()` は、パブリックな（そしてはるかに優れた） [`swap()`](/api/#swap) メソッドに置き換えられました。

## [1.9.12] - 2024-04-17

* [IE Fixes](https://github.com/bigskysoftware/htmx/commit/e64238dba3113c2eabe26b1e9e9ba7fe29ba3010)

## [1.9.11] - 2024-03-15

* iOS 17.4におけるウェブソケットとSSEに関する新しい問題を修正しました。
* テンプレート解析の使用時にスクリプトが二重に実行されることがあった問題を修正
* TypeScriptの型ファイルを修正
* SSE Ext: 再接続ロジックでEventSourceリスナーを再定義するように修正 (#2272)
    
## [1.9.10] - 2023-12-21

* `hx-on*`属性が、末尾にダッシュを付けた`hx-on-`という形式をサポートするようになり、HTML属性のダブルコロンが嫌いなテンプレートシステム（EJSなど）に対応しやすくなりました。
* トリガースペックの解析をキャッシュするオブジェクトを設定できる `htmx.config.triggerSpecsCache` 設定プロパティを追加しました。
* リクエスト・パスに変数値を設定するための `path-params.js` 拡張モジュールを追加した。
* 多くの小さなバグ修正と改善

## [1.9.9] - 2023-11-21

* `hx-target`のような括弧または中括弧の使用した属性に空白を含むCSSセレクタを許可する。
* ユーザーが `Content-Type` リクエストヘッダを上書きできるようにする。
* `htmx.ajax()` に `select` オプションを追加した。
* サードパーティ製スクリプトローダーを使用したいくつかのシナリオで、htmxが初期化されない原因となっていたreadystate検出の競合状態を修正。
* 新しいURLがプッシュされた際に、相対リソースが誤ったベースURLに対して解決される原因となっていたバグを修正。
* インジケータが短時間点滅することがあったUIの問題を修正

## [1.9.8] - 2023-11-06

* npmとビルドに関するいくつかの問題を修正した。

## [1.9.7] - 2023-11-03

* DOMから入れ替わったフォームに関連するボタンがエラーを引き起こすバグを修正。
* `hx-target-error`属性が `response-targets` 拡張モジュールに追加されました。400件および500件すべての回答を1つの属性でキャプチャできます。
* `hx-on` が複数のリスナーを適切にサポートするようになった。
* `hx-confirm` プロンプトがカスタム確認ハンドラに渡されるようになりました。
* htmxで `next` と `previous` が有効な _extended CSS_ シンボルになった。
* `htmx:beforeHistoryUpdate` イベントが追加された。
* 使用する HTTP メソッドを解決する際に、ボタンの `dialog` formmethod を適切に無視する。
* `htmx.config.scrollIntoViewOnBoost`オプションを追加し、`false`に設定することで、ブーストされた要素のボディ上部のスクロールを無効にすることができる。

## [1.9.6] - 2023-09-22

* IEのサポートが回復しました。(ありがとう！@telroshan)
* リクエスト中に無効にする要素を指定できる `hx-disabled-elt` 属性を導入した。
* `hx-swap`の `ignoreTitle` オプションと `htmx.config.ignoreTitle` 設定変数によって、新しいコンテンツで見つかった `title` タグを無視することを明示的に決定できるようになりました。
* `hx-swap` 修飾子は、スワップ機構を明示的に指定しなくても使うことができる。
* `client-side-templates`拡張機能で配列がサポートされるようになった。
* 拡張機能 `client-side-templates` における XSLT サポート
* 拡張機能のイベント処理で `preventDefault()` をサポートする。
* `HX-Redirect`が発生した後でも`HX-Refresh`ヘッダーを適用できるようにする。
* ボタンの `formaction` 属性と `formmethod` 属性が適切に考慮されるようになりました。
* `hx-on` が名前にドットを含むイベントを扱えるようになった。
* `htmx.ajax()` が常に Promise を返すようになった。
* 先行する `style` タグの解析をより効果的に処理する。

## [1.9.5] - 2023-08-25

* WebソケットがHEADERS構造体にターゲットIDを適切に渡すようになった。
* 非常にまれなロード状態のバグが修正された (https://github.com/bigskysoftware/htmx/commit/93bd81b6d003bb7bc445f10192bdb8089fa3495d を参照)。
* `allowEval`がfalseに設定されている場合、`hx-on`は評価されない。
* スクリプトタグの解釈を無効にするには、新しい設定変数 `htmx.config.allowScriptTags` を使用します。
* `htmx.config.selfRequestsOnly`設定変数を使って、オリジンでないホストへのhtmxベースのリクエストを無効にできるようになりました。
* [セキュリティ](https://htmx.org/docs#security)のセクションが拡張され、htmxベースのアプリケーションを適切に保護する方法を開発者がより理解できるようになりました。

## [1.9.4] - 2023-07-25

* 今回のリリースはバグフィックスが中心で、@telroshanが大量に含まれている。
* `HX-Trigger` レスポンスヘッダがカンマ区切りのイベント名をサポートするようになりました。
* `form`属性を使用した送信ボタンが正しく動作するようになりました。
* `changed` モディファイアは `hx-trigger` が定義されている要素ではなく、トリガーとなる要素を使用するようになりました。
* `hx-disable` は動的に処理されるようになったので、追加したり削除したりできる。
* IE11の互換性が回復した！(多分、テストは難しい)
* イベントハンドラ `hx-on` のクリーンアップに関するバグを修正した。
* 多くの小さなバグ修正、誤字の修正、全般的な改善

## [1.9.3] - 2023-07-14

* `hx-on`属性は廃止され、`hx-on:<イベント名>`属性が使われるようになりました。  詳しくは [`hx-on`](/attributes/hx-on) を参照してください。
* これでGitHubのアクションを使ったCIが機能するようになった！
* HTTP リクエストのタイプがパラメータに body を使うかどうかを設定できるようになった。特に `DELETE` は仕様によると、クエリパラメータを使うべきです。コードを壊さないようにするため、今のところこの未定義の挙動を維持していますが、`htmx.config.methodsThatUseUrlParams`設定オプションを更新することで、使用するケースに合わせて修正できるようにしています。AlexとVincentに感謝します！
* `this`シンボルがイベントフィルター式で使用できるようになり、`hx-trigger`がかかっている要素を指すようになった。
* oob のスワップが発生したときに `htmx:afterSettle` イベントが複数回発生するバグを修正した。
* ドキュメントのアクセシビリティを大幅に修正した（Denis & crewに感謝！）。
* 裸の"`hx-trigger`機能によるWebSocket拡張の初期化のバグを修正した。
* HTTP レスポンスヘッダ `HX-Reselect` が追加され、返されたコンテンツから選択を変更できるようになった。
* その他多くの小さなバグ修正

## [1.9.2] - 2023-04-28

* `hx-on`が正しく初期化されないバグを修正。

## [1.9.1] - 2023-04-27

* 新しいネイキッド・トリガーで、明示的に `hx-trigger` を指定したブースト・エレメントが正しく機能しないバグを修正。
* デイリーリマインダーの `window.onpopstate` を使用する他のライブラリとうまく動作するようにコードを追加した：<https://htmx.org/img/memes/javascripthistory.png>

## [1.9.0] - 2023-04-11

* 新しい[`hx-on`](/attributes/hx-on)属性による一般化されたインライン・イベント処理のサポートは、HTMLにおける限られた[`onevent` properties](https://developer.mozilla.org/en-US/docs/Web/Events/Event_handlers#using_onevent_properties)属性の欠点に対処します。
* [ビュー遷移](/docs#view-transitions)のサポート。実験的な[View Transitions API](https://developer.mozilla.org/en-US/docs/Web/API/View_Transitions_API)に基づいており、現在Chrome 111+で利用可能で、近日中に他のブラウザでも利用可能になります。
* `hx-get`などが定義されていない要素に `hx-trigger` が存在する場合、"裸の" [`hx-trigger`](/attributes/hx-trigger) 属性をサポートします。  その代わりに、新しい `htmx:triggered` イベントがトリガーされ、[好みのスクリプティングソリューション](/docs#scripting) を使って応答することができます。
* メモリリークの修正 by [@croxton](https://github.com/bigskysoftware/htmx/commit/8cd3a480a7388877628ce8b9b8e50cd5df48bb81)
* htmxのウェブサイトは、[@danieljsummers](https://github.com/danieljsummers)によって11tyから[zola](https://www.getzola.org/)に移行され、"開発 "用javascriptの依存関係が大幅に削減された。
* その他多くの小さなバグ修正

## [1.8.6] - 2023-03-02

* ESMのサポート！
* htmx.orgのウェブサイトからSassが駆逐された。その結果、今後の進展が期待できる。
* 入力がタブ化されている場合、`keyup` の `changed` 修飾子が正しく動作しないバグを修正した。
* その他多くの小さなバグ修正とドキュメント修正

## [1.8.5] - 2023-01-17

* 新しいオプションのキャッシュバスター設定オプション `getCacheBusterParam` をサポートし、ブラウザが htmx からの `GET` リクエストと生のブラウザからの `GET` リクエストを区別できないようにする。
* `hx-history='false'`属性をサポートし、機密データが履歴キャッシュに保存されないようにしました。(ありがとうございます。)
* [Web Socket](/extensions/web-sockets/)エクステンションでは、イベント指向の新機能が豊富に用意されている（@Renerick氏に感謝！）。
* フォームに同じ名前の空の入力値が複数ある場合のバグ修正 (@bluekeyes さん、ありがとうございます！)
* `setSelectionRange()`を呼び出したときに例外がスローされる入力に関するバグを修正した。
* `htmx:configRequest`イベントに適切なイベントを渡すようにバグ修正した。
* 拡張機能 `preload` のバグ修正と改善
* その他多くの小さなバグ修正 

## [1.8.4] - 2022-11-05

* 1.8.2と全く同じ `revealed` ロジックのリグレッションを修正。 

## [1.8.3] - 2022-11-04

* 新しい [`htmx:confirm` イベント](/events#htmx:confirm) が追加され、非同期の確認ダイアログを htmx リクエストに統合できるようになりました。
* 新しい[head-support](/extensions/head-support)エクステンションは、標準のhtmxがサポートするよりも精巧なheadタグの結合を可能にします。  この機能はフィードバック次第で htmx 2.0 に統合されるかもしれません。
* 新しい[multi-swap](/extensions/multi-swap)は、カスタムスワップ戦略を使って、スクリーン上の複数の要素をより精巧にスワップします。
* 多くのドキュメント修正（貢献してくれたみんなに感謝！）。

## [1.8.2] - 2022-10-12

* `revealed`ロジックの回帰を修正した。

## [1.8.1] - 2022-10-11

* インジケーターに対する未処理のリクエスト数を保持するようになったので、複数の重複したリクエストが問題なく同じインジケーターを共有できるようになりました。
* 要素の属性の状態を追跡し、`htmx.process()`が要素上で呼ばれて属性が変更された場合に再初期化するようにしました。
* [イディオモーフ](https://github.com/bigskysoftware/idiomorph)は、モーフ交換のあらゆるニーズに対応できるようになりました。
* `unset` ディレクティブが `hx-vals` と `hx-vars` に対して正しく動作するようになった。
* 履歴キャッシュが削除された場合、ページのタイトルが正しく設定されるようになりました。
* 新しい[`hx-validate`](https://htmx.org/attributes/hx-validate)属性は、リクエストが送信されるフォーム内にない場合でも、リクエストの前に要素のバリデーションを強制します。
* 多くの小さなバグとドキュメントの修正

## [1.8.0] - 2022-7-12

* **NOTE**: このリリースでは、微妙なコード（ヒストリーのサポートなど）が変更されています。ですから、十分にテストし、問題があればお知らせください。
* ブーストされたフォームは、リンクと同様に URL を履歴に自動的にプッシュするようになりました。[レスポンスURL](https://caniuse.com/mdn-api_xmlhttprequest_responseurl)検出APIのサポートは十分に優れているため、現在はこれをデフォルトにしています。
  * この動作を望まない場合は、ブーストされたフォームに `hx-push-url='false'` を追加してください。
* [hx-replace-url`](https://htmx.org/attributes/hx-replace-url) 属性が導入され、履歴の現在の URL を置き換えることができるようになりました (`hx-push-url` を補完するため)。
* バグ修正 - htmxがページに複数回含まれる場合、要素を複数回処理しない。
* バグ修正 - localStorageが利用できない場合、履歴を保存しようとしない。
* [バグ修正](https://github.com/bigskysoftware/htmx/issues/908) - `hx-boost` は `enctype` 属性を尊重する。
* `m`が有効なタイミング修飾子になった（例：`hx-trigger="2m毎"`）。
* `next` と `previous` が有効な拡張クエリセレクタ修飾子になった、例えば、`hx-target="next div"` は現在の要素から次の div をターゲットにします。
* バグ修正 - `hx-boost` が `_self` をターゲットとするアンカータグをブーストしてしまうバグを修正した。
* `load` イベントが適切にイベントフィルターをサポートするようになった。
* ウェブソケット・エクステンションには多くの改良が加えられた：(Denis Palashevskiiに感謝します。このプロジェクトで最も新しいコミッターです！)
  * 適切な `hx-trigger` サポートの実装
  * トリガー処理APIを拡張機能に公開
  * 送信キューによる安全なメッセージ送信の実装
  * 新しい要素で `ws-send` 属性が接続されるのを修正した。
  * レスポンスにおける複数要素のOOBスワッピングを修正
* `HX-Location` レスポンスヘッダは、クライアントサイドのリダイレクトを完全に htmx 内で実装するようになった。
* `HX-Reswap`レスポンスヘッダは、htmxのスワップ動作を変更することができる。
* 新しい[`hx-select-oob`](https://htmx.org/attributes/hx-select-oob)属性は、サーバーのレスポンスから1つ以上の要素を選択し、帯域外スワップでスワップします。
* 新しい [`hx-replace-url`](https://htmx.org/attributes/hx-replace-url) 属性を使用すると、ロケーションバーの現在の URL を置き換えることができます (`hx-push-url` に非常に似ていますが、新しい履歴エントリは作成されません)。  対応する `HX-Replace-Url` レスポンスヘッダも使用できます。
* htmxは、ブーストされたリンクや`hx-get`属性などのアンカーを適切に処理するようになった。

## [1.7.0] - 2022-02-22

* 新しい[`hx-sync`](https://htmx.org/attributes/hx-sync)属性は、様々なストラテジー(例えばreplace)を使って、1つのエレメントに対して複数のエレメントリクエストを同期させることができます。
  * また、`htmx:abort` イベントを送信することで、リクエストを行っているエレメントを中止できるようになりました。
* [サーバー送信イベント](/extensions/server-sent-events) と [ウェブソケット](/extensions/web-sockets) が、通常のコアサポートに加えて、拡張機能として利用可能になりました。htmx 2.0 では、現在の `hx-sse` と `hx-ws` 属性はこれらの新しい拡張機能に完全に移行されます。これらの機能を拡張機能に移行することで、htmxのコアファイルサイズを損なうことなく、両方の機能を追加できるようになります。新しい拡張機能に移行することをお勧めしますが、`hx-sse` と `hx-ws` は htmx 1.x で無期限に動作し続けます。
* [属性継承](/docs#inheritance)を[`hx-disinherit`](https://htmx.org/attributes/hx-disinherit)属性でマスクできるようになりました。
* `HX-Push` ヘッダーに `false` 値を指定できるようになり、履歴スナップショットが発生しなくなった。
* 多くの新しいエクステンション、そしてすべての貢献者に感謝する！
  * 新しい[`alpine-morph`](/extensions/alpine-morph)により、アルパインのスワッピングエンジンを使うことができます。
  * [restored](/extensions/restored)エクステンションが追加され、履歴の復元時にDOM内のすべての要素に対して`restore`イベントをトリガーするようになった。
  * [loading-states](/extensions/loading-states)エクステンションが追加され、要素の無効化やCSSクラスの追加・削除など、リクエスト実行中のロード状態を簡単に管理できるようになりました。
* [hx-include`](https://htmx.org/attributes/hx-include) と [`hx-indicator`](https://htmx.org/attributes/hx-indicator) 属性で `this` シンボルが正しく解決されるようになりました。
* オブジェクトが[`hx-vals`](https://htmx.org/attributes/hx-vals)属性でインクルードされると、JSONに変換されます（文字列 `[Object object]"` としてレンダリングされるのではありません）。
* `htmx.ajax()`関数呼び出しにスワップ・スタイルを渡せるようになりました。
* ポーリングイベントに `target` 属性が追加され、ポーリングする要素でポーリングをフィルタリングできるようになりました。
* 帯域外関連の新しいイベントが2つ追加された：`htmx:oobBeforeSwap`と`htmx:oobAfterSwap`。

## [1.6.1] - 2021-11-22

* 新しい `HX-Retarget` ヘッダーにより、返されるコンテンツのデフォルトターゲットを変更することができます。
* `htmx:beforeSwap` イベントには、設定可能なプロパティが追加された：detail.isError`は、指定されたレスポンスをエラーとして扱うかどうかを指定するために使用することができます。
* `htmx:afterRequest`イベントに2つの新しい詳細プロパティが追加された: `success` と `failed` で、htmx や hyperscript でトリガーフィルタを書くことができる：
  ```applescript
    on htmx:afterRequest[failed]
      set #myCheckbox's checked to true
  ```
* [hx-trigger`](https://htmx.org/attributes/hx-trigger) の `from:` オプションを修正し、`closest <CSS selector>` と `find <CSS selector>` フォームをサポートするようにした。
* 明示的に`target`を設定したアンカータグをブーストしない。
* ブーストされた要素のすべてのイベントをキャンセルせず、自然にトリガーされるイベントのみをキャンセルする（アンカーのクリック、フォームの送信）。
* ヒストリーナビゲーションで、明らかにされた要素が再要求されないように、明らかにされた状態をDOMに保持する。
* 要素に他の htmx 属性がない場合でも、すべての [`hx-ext`](https://htmx.org/attributes/hx-ext) 属性を処理する。
* ロード時に現在のURLをスナップショットし、ページ更新後に履歴サポートが適切に機能するようにする。
* 多くのドキュメントの更新（すべての貢献者に感謝します）


## [1.6.0] - 2021-10-01

* `<script>`タグのサポートを完全に見直し、`<script src="...'/>` フォームをサポートするようになった。
* `unset`という値を使って、通常継承されるプロパティをクリアできるようになりました（例：hx-confirm）。
* `htmx-added`クラスはスワップ前に新しいコンテンツに追加され、セトリングフェーズの後に削除される。これは、追加されたコンテンツの CSS トランジションをより柔軟に書くことができます（`htmx-settling` のようにターゲットに依存するのではなく）。
* `htmx:beforeSwap`イベントが更新され、[swapping](https://htmx.org/docs/#modifying_swapping_behavior_with_events) の動作を設定できるようになりました。
* `<title>`抽出サポートの改善
* `hx-trigger` の `from:` モディファイアを使うと、`window` オブジェクトのイベントをリッスンすることができます。
* `intersect`イベントの`root`オプションが修正された。
* ブーストされたフォームは `enctype` 宣言を尊重する。
* `HX-Boosted` ヘッダは boosted 要素からのリクエストに送られます。
* プロミスは、APIコール（すなわち`htmx.ajax`）でない限り、メインのajax関数から返されません。

## [1.5.0] - 2021-7-12

* フォーム送信中にクリックされたボタンのトラッキングをサポートする。
* [hx-trigger](https://htmx.org/attributes/hx-trigger)属性による条件付きポーリング
* [hx-trigger](https://htmx.org/attributes/hx-trigger)の `from:` 引数で `document` が有効な擬似セレクタになり、ドキュメント上のイベントをリッスンできるようになりました。
* [hx-request](https://htmx.org/attributes/hx-request)属性が追加され、リクエストの以下の点を設定できるようになりました。
    * `timeout` - リクエストのタイムアウト時間。
    * `credentials` - リクエストがクレデンシャルを送信する場合
    * `noHeaders` - リクエストからすべてのヘッダーを取り除く。
* 上記の属性とともに、対応する `htmx.config` プロパティ（例えば `htmx.config.timeout`）を使って、それぞれのデフォルト値を設定することができます。
* [hx-swap](https://htmx.org/attributes/hx-swap)の`scroll`オプションと`show`オプションの両方が、擬似セレクタ`window:top`と`window:bottom`を含む、スクロールまたは表示する要素を選択するための拡張構文をサポートするようになりました。

hx-swap](https://htmx.org/attributes/hx-swap)の`scroll`オプションと`show`オプションの両方が、擬似セレクタ`window:top`と`window:bottom`を含む、スクロールまたは表示する要素を選択するための拡張構文をサポートするようになりました。

## [1.4.1] - 2021-6-1

* 誤字修正

## [1.4.0] - 2021-5-25

* [hx-trigger](https://htmx.org/attributes/hx-trigger)属性に `queue` オプションが追加され、飛行中のリクエストと共にイベントを受信した場合に、どのようにイベントをキューに入れるかを指定できるようになりました。
* `htmx.config.useTemplateFragments`オプションが追加され、サーバからのコンテンツの解析にHTMLテンプレートタグを使用できるようになった。これにより、テーブルの行のようなものを返すときに Out of Band コンテンツを使用できるようになりますが、IE11 には対応していません。
* `defaultSettleDelay`が100msから20msに変更されました。
* 新しい合成イベント、[intersect](https://htmx.org/docs#pecial-events)が導入され、`IntersectionObserver` APIによって指定されたアイテムがビューにスクロールされたときにトリガーできるようになりました。
* 信じられないような速度でスクロールしたときに、`reveal`ロジックで例外が発生するタイミングの問題を修正 - <https://github.com/bigskysoftware/htmx/issues/463>
* SVGタイトルがページタイトルとして誤って使用されるバグを修正 - <https://github.com/bigskysoftware/htmx/issues/459>
* GETを発行するブーストされたフォームは、デフォルトでURLをプッシュするようになりました - <https://github.com/bigskysoftware/htmx/issues/485>
* 要素がDOMから削除されたときのリクエスト・イベントのディスパッチが改善された。
* `hx-prompt`が失敗するバグを修正。
* `htmx.config.withCredentials` オプションが追加され、ajax リクエストでクレデンシャルを送信できるようになった (デフォルトは `false`)。
* `hx-trigger`の`throttle`オプションは、最初のリクエストをそれ以上遅らせない。
* `meta`キーはブーストリンクでは無視される。
* `<script>`タグがグローバル・スコープで評価されるようになった。
* `hx-swap` が `none` オプションをサポートするようになった。
* Safariテキスト選択のバグ - <https://github.com/bigskysoftware/htmx/issues/438>
  
## [1.3.3] - 2021-4-5

* DOMの一部でhtmxをオフにできるように、[`hx-disabled`](https://htmx.org/docs#security)属性を追加した。
* SSEは、`htmx.config.wsReconnectDelay` 設定を使用して、再接続時にフルジッター指数バックオフアルゴリズムを使用するようになった。

## [1.3.2] - 2021-3-9

* バグ修正

## [1.3.1] - 2021-3-9

* IE11の修正

## [1.3.0] - 2021-3-6

* `hx-trigger`の `target` 修飾子をサポートし、イベントのターゲットとなる要素に基づいてフィルタリングできるようになった。これにより、ターゲットセレクタへの遅延バインディングが可能になる。
* イベントは、`hx-trigger` 指定に `consume` キーワードが追加されない限り、そのイベントを処理する可能性のある最初のエレメントによって消費されなくなります。
* ajax リクエストが始まる直前に発生する `htmx:beforeSend`イベントを追加した。
* SSEスワップは適切に決済されている
* アンカーをクリックした際、すべてのクリックが不適切にキャンセルされていたバグを修正
* `htmx.ajax()` がプロミスを返すようになった。

## [1.2.1] - 2021-2-19

* 履歴キャッシュで、最初のナビゲーションの後、キャッシュが吹っ飛んでしまう問題を修正。
* `htmx.config.refreshOnHistoryMiss`オプションを追加し、AJAXリクエストを発行するのではなく、履歴キャッシュの取りこぼし時に全ページの更新をトリガーできるようにした。

## [1.2.0] - 2021-2-13

### 新機能

* `hx-vars` は非推奨となり、`hx-vals` が使われるようになった。
* `hx-vars`が提供していた動作を実現するために、`hx-vals`が `javascript:` 接頭辞をサポートするようになった。
* 新しい `hx-headers` 属性は、属性を使ってリクエストにヘッダを追加することができます。`hx-vals` と同様に、JSON や `javascript:` 接頭辞を使った javascript をサポートしています。
* `hx-include` は、その要素がフォームタグでなくても、要素の下にあるすべての入力をインクルードするようになりました。
* [preload extension](https://htmx.org/extensions/preload/) が プリロードされたコンテンツの画像を積極的にロードする、`preload-images="true"` 属性を提供するようになりました。
* 履歴キャッシュのミスによるリクエストでは、サーバーが履歴リクエストと通常のリクエストを区別できるように、新しい `HX-History-Restore-Request` ヘッダーが含まれます。

### 改善とバグ修正

* 入力値の優先順位の取り扱いを改善し、囲み形式を優先するようにした（[こちら](https://github.com/bigskysoftware/htmx/commit/a10e43d619dc340aa324d37772c06a69a2f47ec9)を参照）。
* イベントのフィルタリングロジックを `preventDefault` の後に移動した。そのため、フィルタリングしてもイベントは適切に処理されます。
* `outerHTML`スワップによって削除された要素に対して、スワップ後イベントをトリガーしなくなった。
* 要素がDOMから削除されたときに、他の要素に追加されたイベント・ハンドラを適切に削除する。
* `hx-swap`の`scroll:`モディファイアを、`outerHTML`のスワップが発生したときに適切に処理する。
* 多くのドキュメント修正

## [1.1.0] - 2021-1-6

* 新しく追加された[preload extension](https://htmx.org/extensions/preload/)は、より低遅延なリクエストのためにリソースをプリロードすることができます！
* 拡張機能の `ignore:` 修飾子をサポートする。
* 複数の値が存在する場合、最も関連性の高い値がサーバーによって選択される可能性が最も高くなるように、フォーム変数の順序を更新し、フォームを囲む*最後*の値を含めるようにした。
* htmx 形式の ajax リクエストを javascript から発行するための [`htmx.ajax()`](https://dev.htmx.org/api/#ajax) javascript 関数をサポート。
* キャッシュの動作を改善するために、以下の htmx リクエストヘッダを削除した: `HX-Event-Target`、`HX-Active-Element`、`HX-Active-Element-Name`、`HX-Active-Element-Value`
* [`hx-preserve`](https://dev.htmx.org/attributes/hx-preserve)属性が追加され、リクエストにまたがって要素を保持できるようになりました (たとえば、video要素を正しく再生し続けることができます)。
* [path-deps](https://dev.htmx.org/extensions/path-deps/#refresh)は、javascriptで手動でパスの依存関係を更新するための小さなAPIを表示するようになりました。
* [`hx-trigger`](https://dev.htmx.org/attributes/hx-trigger)の`from:`節をサポートし、ある要素が他の要素のイベントに応答できるようになりました。
* `htmx:beforeProcessNode` イベントを追加し、(以前はドキュメント化されていなかった) `htmx:processedNode` の名前を `htmx:afterProcessNode` に変更した。
* [`hx-indicator`](https://dev.htmx.org/attributes/hx-indicator)属性に `closest` 構文を追加した。
* 最新バージョンの[hyperscript](https://hyperscript.org)の`on load`サポートを追加。
* CSP との互換性のために `htmx.config.allowEval` 設定値を追加した。
* バグ修正と改善 

## [1.0.2] - 2020-12-12

* すべての API メソッドを拡張し、要素だけでなく文字列セレクタも受け取れるようにする。
* 帯域外のスワップ・エレメントがトップレベルである必要はなくなった。
* [hx-swap-oob`](https://htmx.org/attributes/hx-swap-oob) でリターゲットする CSS セレクタを受け付けるようになった。

## [1.0.1] - 2020-12-04

* AJAXファイルアップロードが正しくイベントを発生するようになり、[適切なプログレスバー](https://htmx.org/examples/file-upload)が可能になった。
* htmx apiの関数のうち、要素を指定する関数で、文字列セレクタを指定できるようになりました：
   ```js
    htmx.on('#form', 'htmx:xhr:progress', function(evt) {
      htmx.find('#progress').setAttribute('value', evt.detail.loaded/evt.detail.total * 100)
    });
   ```
* htmx が `<select>` 要素の `multiple` 属性を適切に処理するようになった。

## [1.0.0] - 2020-11-24

* リリース・バージョンを繰り上げ 😀

## [0.4.1] - 2020-11-23

* タイトルタグにHTMLエンティティが含まれる場合のタイトルタグのサポートに関するバグを修正
* `loadstart`、`loadend`、`progress`、`abort` イベント属性を htmx の同等物に適切に渡す。

## [0.4.0] - 2020-11-16

* レスポンスヘッダ `HX-Redirect` と `HX-Refresh` をサポートし、それぞれクライアント側へのリダイレクトとページ更新を行えるようになりました。
* `hx-vars` が入力値を上書きするようになった。
* レスポンスに含まれる`<title>`タグは、ページタイトルの更新に使用される。
* `eval()`の使用はすべて削除され、`Function`が使用されるようになった。
* `hx-vars` に代わる安全な方法として、[`hx-vals`](https://htmx.org/attributes/hx-vals) があります。ユーザーが提供した値を安全に htmx に渡したい場合は、評価ではなく `JSON.parse()` を使用します。

## [0.3.0] - 2020-10-27

* `hx-trigger`の解析が書き直され、任意のjavascript式に基づいてイベントをフィルタリングするための[trigger filters](https://htmx.org/docs/#trigger-filters)がサポートされました。
* htmx は2つの追加レスポンスヘッダ `HX-Trigger-After-Swap` と `HX-Trigger-After-Settle` をサポートし、指定されたライフサイクルイベントの後（スワップ前ではなく）にイベントをトリガーできるようになりました。
* `requestConfig`は、AJAXのライフサイクルを取り巻くイベントに渡されるようになった。
* htmx は `<script>` タグに言語が定義されていない場合、javascript として評価するようになった。
* 新しい[`event-header`](https://htmx.org/extensions/event-header)エクステンションは、リクエストにイベントのトリガーとなるシリアライズされたJSON表現を含めます。

## [0.2.0] - 2020-9-30

* AJAXファイルアップロード [サポート](https://htmx.org/docs#files)
* HTMLバリデーションAPIは[respectected](https://htmx.org/docs#validation)

## [0.1.0] - 2020-9-18

* *画期的な変更*です：SSE属性 [`hx-sse`](https://htmx.org/attributes/hx-sse/) と Web Sockets属性 [`hx-ws`](https://htmx.org/attributes/hx-ws) の構文が変更され、コロン区切りが使用されるようになりました：`hx-sse='connect:/chat swap:message'` となります。
* SSE属性[`hx-sse`](https://htmx.org/attributes/hx-sse/)は、新しい構文`swap:<イベント名>`によって、htmx要素をトリガーするだけでなく、イベントで直接コンテンツを入れ替えることができます。
* [`hx-target`](https://htmx.org/attributes/hx-target)は、CSSセレクタで要素より下の要素を見つけるための`find`構文をサポートするようになりました。
* htmxは遅延ローディングと多くのパッケージマネージャでより良く動作する。
* すべての htmx イベントは、AlpineJS や他のフレームワークとの互換性を高めるために、キャメルケースとケバブケースの両方でディスパッチされます。(例えば、`htmx:afterOnLoad`は、`htmx:after-on-load`としてもトリガーされます)
* [hypeerscript](https://hyperscript.org)がhtmxとは無関係に初期化されるようになった。

## [0.0.8] - 2020-7-8

* `hx-swap` の `view` 修飾子は `show` に名前が変更されました: `hx-swap='innerHTML show:top'`

## [0.0.7] - 2020-6-30

* [`hx-swap`](https://htmx.org/attributes/hx-swap)属性が2つの新しい修飾子に対応しました：
    * `scroll` - ターゲットを `top` または `bottom` にスクロールさせる。
    * `view` - ターゲットの `top` または `bottom` をスクロールして表示する。
* [`hx-push-url`](https://htmx.org/attributes/hx-push-url) 属性は、 `true` と `false` に加えて、オプションでプッシュする URL を指定できるようになりました。
* リクエストと一緒に送信されるパラメータに動的に追加できる [`hx-vars`](https://htmx.org/attributes/hx-vars) 属性を追加しました。

## [0.0.6] - 2020-6-20

* カスタムリクエスト/レスポンスヘッダが `X-` 接頭辞で始まらないようになりました。
* 空の動詞属性が許可され、アンカータグのセマンティクスに従うようになりました (例 `<div hx-get></div>`)
* nunjuksのインライン・レンダリングが`client-side-templates`拡張機能でサポートされるようになった。
* 新しい `ajax-header` 拡張は `X-Requested-With` ヘッダーを含む。
* 悪いJSONがより優雅に処理されるようになった
* `hx-swap="none"`はスワップを行わない <https://github.com/bigskysoftware/htmx/issues/89>
* `hx-trigger` が `throttle` 修飾子をサポートするようになった <https://github.com/bigskysoftware/htmx/issues/88>
* フォーカスされた要素は、可能であれば置換後も保持されます。
* 疎な `hx-` アノテーションを持つ大きな DOM ツリーに対するパフォーマンスの改善

## [0.0.4] - 2020-5-24

* 拡張メカニズム追加
* SSEサポート追加
* WebSocketのサポート追加

## [0.0.3] - 2020-5-17

* htmxに改名
* `hx-prompt`属性のバグ修正
* 複数の `hx-swap-oob` 属性に関するバグ修正
* デフォルトのCSSインジケーター注入を独自のシートに移動し、壊れないようにした。
* `htmx.config.includeIndicatorStyles`設定オプションを追加し、インジケータCSSの注入を拒否できるようにした。


## [0.0.1] - 2020-5-15

* 初回リリース（当初の名前はkutty）
