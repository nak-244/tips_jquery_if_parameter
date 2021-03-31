# jQueryでURLパラメータ取得後ifで条件分岐

URLのパラメータもしくはアンカータグを利用して、jQueryで条件分岐をします。  
GETメソッドでURLパラメータが付く場合に、CONTENTSの中身を入れ替えたりできるので、A/Bテストの実行にも有用だと思います。かんたんな実装なのでこの機会に使ってみましょう。

## URLパラメータを取得
```java:title
var url   = location.href;
params    = url.split("?");
spparams   = params[1].split("&");
 
var paramArray = [];
```
