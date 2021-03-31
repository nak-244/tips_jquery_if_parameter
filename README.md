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
