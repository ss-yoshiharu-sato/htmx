+++
title = "hx-request"
+++

`hx-request`属性では、以下の属性を使ってリクエストの様々な側面を設定することができます：
 
* `timeout` - リクエストのタイムアウトをミリ秒単位で指定します。
* `credentials` - リクエストがクレデンシャルを送信する場合
* `noHeaders` - リクエストからすべてのヘッダを取り除く

これらの属性は、JSONのような構文を使って設定される：

```html
<div ... hx-request='{"timeout":100}'>
  ...
</div>
```

接頭辞に `javascript:` または `js:` を付けることで、値を動的に評価することができます：

```html
<div ... hx-request='js: timeout:getTimeoutSetting() '>
  ...
</div>
```

## Notes

* `hx-request`はマージ継承され、親要素に置くことができる。
