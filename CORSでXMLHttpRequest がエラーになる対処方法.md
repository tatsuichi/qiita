## CORSでXMLHttpRequest がエラーになる対処方法

### はじめに

GitHub Pagesで電車遅延を知らせるWebページを作っていた時にCORSにハマったので対処方法をまとめました。

環境
-
ブラウザ：chrome バージョン 74

```javascript
const xhr = new XMLHttpRequest();
xhr.open("GET", `https://rti-giken.jp/fhc/api/train_tetsudo/delay.json`, true);
xhr.responseType = 'json';
xhr.onreadystatechange = function() {
  if(xhr.readyState === 4) {
    if(xhr.status === 200) {
      //
      // JSON遅延データ処理
      //
    }
  }
};
xhr.send();
```

エラーメッセージ
-
実行すると以下のメッセージが出る。
```text
Access to XMLHttpRequest at 'https://rti-giken.jp/fhc/api/train_tetsudo/delay.json' from origin 'https://username.github.io' has been blocked by CORS policy: No 'Access-Control-Allow-Origin' header is present on the requested resource.
```

対処方法
-
chrome.exeの起動オプション（引数）に --disable-web-security、--disable-web-securityを付ける。クライアント側の対応のみで解決する。

参考
-
[Access-Control-Allow-Originのエラーを回避してWebサービスを呼ぶには？](https://web.plus-idea.net/2018/03/allow-control-allow-origin-plug-in/)
[鉄道遅延情報のjson](https://rti-giken.jp/fhc/api/train_tetsudo/)