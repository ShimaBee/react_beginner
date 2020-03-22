# React_Beginner

## はじめに
　この記事は2020年1月25日に行われたReact質問会の個人的な振り返りと、今後React入門会を行ってく方に簡単なドキュメントを残すことが目的です。React入門会を資料をアップデートしながら今後も行っていきたい😊

## 目次
- Reactとは
- Reactの特徴
- プロジェクトを作ろう
- JSX
- componentとは

## React.jsとは
> React はユーザインターフェイスを構築するための、宣言型で効率的で柔軟な JavaScriptライブラリです。複雑なUIを、「コンポーネント」と呼ばれる小さく独立した部品から組み立てることができます。( Reactチュートリアルより )

## Reactの特徴 
1. コンポーネント指向
2. 仮想DOM

### コンポーネント指向とは
まず、一般的にコンポーネントとは構成要素、部品を表す言葉です。そして、Reactの中でのコンポーネントとは構造、見た目、振る舞いをワンセットにした部品のことです。

このコンポーネントを必要な時に呼び出して、ページを構成することがコンポーネント指向の考え方です。

### コンポーネント指向のメリット

**コンポーネントは使い回しができる**
ページ必要なところでそのコンポーネントを呼び出し、ページを構成するため同じコンポーネントを表示させたい場合はイチイチ同じコードを書くことなく、表示させたい数だけそのコンポーネントを呼び出せば良いのですごく楽！

 
**コードを切り分けることができ、メンテナンスがしやすい**
コンポーネントは基本的に別ファイルに記述されており、コードが切り分けられているため、見やすくメンテナンスがしやすい。

**まとめ**
コンポーネント指向によって、今まで作れなかった見た目のUIを実装できるようになったりはしませんが、作る側にとって非常に優しいUIを作ることができる。

<br>

## 仮想DOMとは
仮想DOMとはJavascriptのオブジェクトにより、仮想的に作られたDOMのことです。

ここでは仮想DOMについて深くは触れません。ただ、仮想DOMは通常のDOMと違い、Javascriptのオブジェクトで作られているということ、仮想DOMを使うことでページの表示速度が上がることを覚えて欲しいです。

### なぜ仮想DOMで表示速度が上がるのか？

　簡単な図を用意してみました。この図を見てわかるように、ページ遷移などでDOMを再構築する際に、その再構築する量が明らかに減るので表示速度が上がります。特に共通部分が多いページに遷移するときの速度に差が出ます。

![](https://i.imgur.com/CO11FRt.jpg)


***もう少し仮想DOMを知りたい方***

- [VirtualDOMの仕事ってなに？](https://qiita.com/risagon/items/019942c60e9c3e6c05a5)
- [リアルな DOM はなぜ遅いのか](https://blog.dodgson.org/b/2014/12/11/why-is-real-dom-slow/)

<br>


## プロジェクトを作ろう
　ここまでReactの概要、使うメリットなどを話してきましたが、実際に書いてみないと分からないところもあると思うので、ここからハンズオン形式で進めます。
 
はじめは、プロジェクトを作ってから、reactを起動し、"Hello,React"という文字列を表示するまで！


※自分の環境を作るのが面倒な方はこちらのツールで再現してください。
[codesandbox](https://codesandbox.io/)

<br>

### Set Up (Hello,Reactまでの道)
1. プロジェクト作成
`npx create-react-app react_beginner`

2. 起動

- まずは、作ったディレクトリに移動
`cd react_beginner`
- 起動コマンド
`npm start`

- 起動が確認できたら `control+c`で一旦、Reactを落とす。
<br>

3. 今回使わないファイルの削除<br>
src配下全部消す。
`rm -rf src/*`<br>
今回は勉強のため、初めから全部書きます！

<br>


4. src/index.jsを作る

```javascript
import React from 'react';
import ReactDOM from 'react-dom';

ReactDOM.render(<h1>Hello,React</h1>, document.getElementById('root'));
```

- 起動コマンド
`npm start`

<br>

index.jsの簡単な説明。
<br>

Hello,React達成！！
<br>


## コンポーネントを作ってみる。
Hello,Reactをコンポーネントとして切り分ける。
後ほど詳しくコンポーネントはやるので、今は簡単に！

1. src/components/App.jsを作る<br>
a.  srcの中にcomponentというディレクトリを作って、その中にApp.jsというファイルを作る。<br>
b.  App.jsの中身を書く

**App.js**
```javascript
import React, {Component} from 'react';

class App extends Component {
  render() {
    return <div>Hello,react</div>
  }
}

export default App;
```
<br>

2. insex.jsでApp.jsを読み込む
**index.js**
```javascript
import App from './components/App'
```
<br>


3. React.DOMの第一引数をAppコンポーネントにする。
```javascript
ReactDOM.render(<App/>, document.getElementById('root'));
```
<br>

4. [localhost:3000](localhost:3000) にアクセスして、Hello,Reactが出ればOK

<br>

## JSX
一旦、JSXについては、スライド資料！

### JSXを使わないHello,React
```javascript
class App extends Component {
  render() {
    return React.createElement(
      "div",
      null,
      "Hello,React"
    );
  }
}
```
※Babelという仕組みがHTMLっぽい書き方をJSの書き方に直している。

[Babelの変換](https://babeljs.io/repl)

<br>

### jsの変数を含める書き方

```javascript
class App extends Component {
  render() {
    const greet = "Hello,shimaboo"
    return <div>{greet}</div>
  }
}
```

<br>

### 複数の親タグをreturnで返せない
```javascript
class App extends Component {
  render() {
    return <div>Hello,React</div>
    <p>I love React</p>
  }
}
```
- 一つのdivの中にタグをいくつも入れることは可能。
- 複数の親タグを作るとエラー出ます。
<br>


### 複数の親タグをreturnで返すReact.Fragment

```javascript
class App extends Component {
  render() {
    return <React.Fragment>
      <div>Hello,React</div>
      <p>I love React</p>
    </React.Fragment>
  }
}
```

<br>



### クラスコンポーネント
基礎的、学ぶならここから。
```javascript
class App extends Component {
  render() {
    return <div>Hello,react</div>
  }
}
```


### 関数コンポーネント
省略的な書き方、主流。
```javascript
function App() {
  return (
    <div>Hello,react</div>
  );
}
```
<br>

## props
- 親子の説明（親：const User | 子:<User/>）。
- Userコンポーネント（子）をたくさん作っても楽しい。

**App.js**
```javascript
// 描画の処理
class App extends Component {
  render() {
    return <React.Fragment>
    <div><User name={"shimaboo"} email={"shimaboo@mail.com"}/></div>
    <div><User name={"yuta"} email={"yuta@mail.com"} tel={"090-0000-0000"}/></div>
    <div><User name={"hoge"} tel={"090-xxxx-xxxx"}/></div>
    </React.Fragment>
  }
}

// Userコンポーネント
const User = (props) => {
  return <React.Fragment>
    <div>USER: {props.name}　{props.email}　{props.tel}</div>
  </React.Fragment>
  }
```


<br>

## state
### ボタンを押すと数字が増えるCounterコンポーネントを作る！

**App.js**
```javascript
// Appコンポーネント内のCounterコンポーネントの描画
class App extends Component {
  render() {
    return <div><Counter/></div>
  }
}
// Counterコンポーネント
class Counter extends Component {
  // 初期化処理
  constructor(props){
    super(props)
    this.state = { count: 0} 
  }
  // カウントアップ処理
  countUp = () => {
    this.setState({count: this.state.count + 1})
  }
  // コンポーネント自体の描画処理
  render(){
  return (
    <React.Fragment>
  <div>counter: {this.state.count}</div>
  <button onClick={this.countUp}>+1</button>
  </React.Fragment>
  )
 }
}
```

- constructorはCounterが呼び出される際に、最初に走る関数。
- constructor内で、superを用いて初期化処理とstateの初期値を定義する。
[参考：なぜsuper(props) を書くの?](https://qiita.com/hand-dot/items/61a4b808f110b12e4281)
- stateへのアクセスは、`this.state`。
- `this.state = {}`ができるのは、constructorの中だけ、他でやるとエラーする。
- setStateを用いて、値は書き換えないといけない
- setStateはstateの更新と変更したDOMの再レンダリングを行なってくれる、逆にsetStateを使わなければ再レンダリングが行われないのでエラーが出る。

<br>

### 時間があれば演習として使う。

## Counterを別ファイルに
再びコンポーネントを切り分ける練習。
まず、Counter.jsをApp.jsの隣に作ってください

**App.js**
```javascript
import React, {Component} from 'react';
import Counter from './Counter';

// Appコンポーネント内のCounterコンポーネントの描画
class App extends Component {
  render() {
    return <div><Counter/></div>
  }
}

export default App;
```

**Counter.js**

```javascript
import React, {Component} from 'react';

// Counterコンポーネント
class Counter extends Component {
  // 初期化処理
  constructor(props){
    super(props)
    this.state = { count: 0} 
  }
  // カウントアップ処理
  countUp = () => {
    this.setState({count: this.state.count + 1})
  }
  // コンポーネント自体の描画処理
  render(){
  return (
  <React.Fragment>
   <div>counter: {this.state.count}</div>
   <button onClick={this.countUp}>+1</button>
  </React.Fragment>
  )
  }
}

export default Counter;
```

<br>

見ていただきありがとうございました。