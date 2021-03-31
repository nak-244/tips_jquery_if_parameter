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
