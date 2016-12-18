#初めてのReact 

##勉強用雛形

```
<!DOCTYPE html>
<html>
  <head></head>
  <body>
    <script src="https://fb.me/react-15.3.0.js"></script>
    <script src="https://fb.me/react-dom-15.3.0.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/babel-core/5.8.34/browser.min.js"></script>
    
    <div id="content"></div>

    <script type="text/babel">
	React.createClass({
    render: function() {
      return(
        
      );
    }
	});
	ReactDOM.render(
    document.getElementById()
  );
    </script>
  </body>
</html>

```

##Reactってなに
- JavaScriptのViewライブラリ
- UI開発用
- 従来のやり方とは違う方法
- SPAに向いている
- VirtualDOMによりかなり高速

##重要なこと
- サーバサイド脳
	- Stateによるデータバインディング
	- 宣言的なView構築(JSX)
	- VirtualDOM
	- これまでサーバがになっていたものをクライアントに行ってもらう
- コンポーネント志向　（データ，見た目，振る舞い）
	- DOMへの作用をコンポーネントに局所化
	- 再利用可能な部品化
	- React内部に保持している「状態」 に合わせてコンポーネントを作ることで「状態」に合わせたViewの構築ができる
	- カプセル化による保守性が高まる
- データフローが明確
	- ステートレスコンポーネント
	- コンポーネントのインターフェース: PropsとState
- ネイティブアプリにも使える
react-native


##従来のやり方と比較

###そもそもDOM操作は難しい
- DOMはどこからでも変更可能 グローバル
	- いつどこで書き換えられるのか分からない
- DOMが状態を持っている
	- タグが見えているのか見えていないのか分からない
- DOMとコードが離れている
	- どこで処理するのか分からない

***いつどこから書き換えられるかわからない状態を
間違いなく管理しなければならない***

###そこで
- DOMを書き換えるのではなく，常に新しいHTMLを生成する(全更新)
	- しかし常に新しいHTMLを作成するのは時間がかかる，効率が悪い
	- ***→virtualDOM 実際には変更部しか更新されない***
- EventListenerをやめてonXxxを使う
- HTMLとJavaScriptを1つにまとめる


###書き方

####命令的な書き方だった
```js:
$('form').on('submit',function(){
    //要素を作って
    var $li = $('<li>');
    // ...
    
    //リストに追加
    $('ul').append($li);
});
```

####宣言的な書き方になった
```js:
var App = React.createClass({
  getInitialState: function(){
    return{members: []};
  },
  onCLick: function(){
    this.setState({
      members: ['aaa','bbb','ccc']
    });
    render: function(){
      var members = this.state.members.map(function(member){
         return <li>{member}</li>;
       });
      return(
      <div>
        <button onCLick={this.onCLick}>alpha</button>
        <ul>
        {members}
        </ul>
      </div>
      );
  }
});
React.render(<App />,document.getElementById('app-container'));
```





##State,JSX, Virtual DOM
- State
	- 変化する値（状態）を扱う気候
	- 1方向データバインディング
	- setState()で変えると，Viewの再描画が走る

- JSX
	- XMLっぽい
	- 宣言的
- Virtual DOM
ReactのバックエンドにあるDOM構造を抽象化したデータ構造
データモデルの状態変化に合わせてVirtualDOMの前後のdiffを算出
生DOM再描画を差分のあった箇所だけ行う


##エラー対処
###Uncaught SyntaxError: embedded: Unterminated JSX contents 

```
    ReactDOM.render(
      <HelloWorld name='React'/>,
                                ^
      document.getElementById('content')
    );
```
上記では，ReactDOM.render内のシンタックスエラーだと言われていたが，実際はrender:function()内のhtmlタグの閉じ忘れが原因だった
 
 


##dev tool
クロームのプラグイン
https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi
インストールしたら拡張管理機能でファイルへのURLへのアクセスを許可するをチェック

##参考文献
React概論
https://speakerdeck.com/naoya/reactgai-lun


Reactがなぜ素晴らしいのか
https://speakerdeck.com/masuidrive/reactganazesu-qing-rasiifalseka


Why React and not jQuery?
https://speakerdeck.com/maechabin/why-react-and-not-jquery

WebデベロッパーのためのReact開発入門 JavaScript UIライブラリの基本と活用  柴田 文彦 (著)
http://amzn.asia/9DiYPeT
