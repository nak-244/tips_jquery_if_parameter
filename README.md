# jQueryでURLパラメータ取得後ifで条件分岐

URLのパラメータもしくはアンカータグを利用して、jQueryで条件分岐をします。  
GETメソッドでURLパラメータが付く場合に、CONTENTSの中身を入れ替えたりできるので、A/Bテストの実行にも有用だと思います。かんたんな実装なのでこの機会に使ってみましょう。

## URLパラメータを取得
```java:URLパラメータを取得
var url   = location.href;
params    = url.split("?");
spparams   = params[1].split("&");
 
var paramArray = [];
```
  
まずはURLのパラメーターを取得します。　http://www.example.com/?key=onece
このようなURLをsplitで切っているわけですね。
  
```java:URLパラメータを取得
for ( i = 0; i < spparams.length; i++ ) {
    vol = spparams[i].split("=");
    paramArray.push(vol[0]);
    paramArray[vol[0]] = vol[1];
}
 
 
if ( paramArray["key"] == "onece") {
    alert("onece");
} else {
    alert("no onece");
}
```
  
## 条件分岐で入れ替える
if文を書き換えればいいだけですね。
```java:if文
for ( i = 0; i < spparams.length; i++ ) {
    vol = spparams[i].split("=");
    paramArray.push(vol[0]);
    paramArray[vol[0]] = vol[1];
}
 
 
if ( paramArray["key"] == "onece") {
    $("#link").attr("href", "http://www.yahoo.co.jp/");
} else {
    $("#link").attr("href", "http://www.google.com/");
}
```
  
JQueryで画像を入れ替えたり、コンテンツを.hide()とか様々なやり方が考えられます。  
LPからの遷移などで使うと便利だと思います。  
  
簡易的なA/Bテストにも直ぐ使えるのでオススメ。
  
## コピペで使えるソースコード

```java:コピペ
<script src="http://code.jquery.com/jquery-2.1.3.min.js"></script>
<script>
$(function(){
var url   = location.href;
params    = url.split("?");
spparams   = params[1].split("&");
 
var paramArray = [];
for ( i = 0; i < spparams.length; i++ ) {
    vol = spparams[i].split("=");
    paramArray.push(vol[0]);
    paramArray[vol[0]] = vol[1];
}
 
 
if ( paramArray["key"] == "onece") {
    $("#link").attr("href", "http://www.yahoo.co.jp/");
} else {
    $("#link").attr("href", "http://www.google.com/");
}
});
</script>
```
  
***
（↓別の方法）
  
### JavaScriptでURLのパラメータやアンカーを判断して処理を変更する方法
URLのパラメータやアンカー（#以降の部分）を取得して、その値ごとに処理を変更する方法をまとめました。

`https://www.yahoo.co.jp/?category=A&id=1123`  
※パラメータは1つとは限らず、複数ある場合は「&」でつないでいきます。  
  
まずlocation.searchを利用して「?」で始まるパラメータ部分を取得します。  
（substring(1)とすることで2文字目以降［?以外］を取得します）  
もしURLにパラメータが存在すれば、さらに「&」で分割した後に、連想配列のkeyとvalueにそれぞれパラメータのkeyとvalueを格納します。  
処理を変更するにはif文で条件を指定するだけです。  

#### パラメータに「id=osaka」が含まれるかどうかを調べる場合
```java:id=osaka
// URLのパラメータを取得
var urlParam = location.search.substring(1);
 
// URLにパラメータが存在する場合
if(urlParam) {
  // 「&」が含まれている場合は「&」で分割
  var param = urlParam.split('&');
 
  // パラメータを格納する用の配列を用意
  var paramArray = [];
 
  // 用意した配列にパラメータを格納
  for (i = 0; i < param.length; i++) {
    var paramItem = param[i].split('=');
    paramArray[paramItem[0]] = paramItem[1];
  }
 
  // パラメータidがosakaかどうかを判断する
  if (paramArray.id == 'osaka') {
    $('.pram').append('<p>大阪です</p>');
  } else {
    $('.pram').append('<p>大阪ではありません</p>');
  }
}
```

#### URLのアンカーで判断する場合
アンカーの取得は簡単で、location.hashを利用して#以降の部分を取得します。
```java:アンカー取得
// URLのアンカー（#以降の部分）を取得
var urlHash = location.hash;
 
// URLにアンカーが存在する場合
if(urlHash){
  // アンカーが#osakaかどうかを判断する
  if (urlHash == '#osaka') {
    $('.hash').append('<p>大阪です</p>');
  } else {
    $('.hash').append('<p>大阪ではありません</p>');
  }
}
```
