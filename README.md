![](sass.svg)

# SCSSの導入について

SCSSはSassというCSSを拡張した言語の種類の一つです。

CSSの記述がより書きやすくなり、ネストの使用や変数の使用や複数のCSSファイルの読み込みなどが可能になります。

しかもCSSと同じ書き方ができるので、CSSを学習していれば誰でも使うことができます。

SCSSはプリプロセッサとなっているので、コンパイルが必要です。SCSSからCSSに変換することでHTMLと連携することができます。

今回はVSCodeの拡張機能を使ってSCSSを記述する方法とコンパイルをしてCSSに変換していきます。

# 導入するVSCode拡張機能

### Live Sass Compiler

この「Live Sass Compiler」をインストールすることによって、SCSSファイルからCSSファイルに自動変換してくれます。

自動変換されたCSSをHTMLから読み込むことによってCSSを適用することができます。

まずはVSCodeに拡張機能「Live Sass Compiler」をインストールしましょう。

# SCSSファイルの変換とHTMLとの連携

これから実際にSCSSを記述して、CSSに変換し、HTMLから読み込んでいきたいと思います。

まずは、デスクトップ上に「`scss`」という新規フォルダを作成し、そのフォルダをVSCodeで開きます。

そのフォルダの中に、「`index.html`」と「`css`」フォルダを作成します。
「`css`」フォルダの中には「`style.scss`」を作成します。

下のようなフォルダ階層になります。

```
scss
├── index.html
└── css
    └── style.scss
```

`index.html`には以下のコードを入力しておきます。

```html:index.html

<!DOCTYPE html>
<html lang="ja">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <link rel="stylesheet" href="css/style.css" />
  </head>
  <body>
    <h1>見出し</h1>
  </body>
</html>

```

`style.scss`には以下のコードを入力します。

```scss:style.scss
h1 {
  color: red;
}
```

この状態で、index.htmlをブラウザで確認しても、見出しの色は変更されていません。まだ、SCSSからCSSの変換が行われていないからです。

CSSへの変換を行うには、`style.scss`を開いた状態でVSCodeの下のステータスバーの「**Watch Sass**」ボタンをクリックしましょう。

そうすると、cssフォルダの中に、`style.css`と`style.css.map`ファイルが生成されていることを確認できます。

`style.css`の中を見てみると

```css:style.css
h1 {
  color: red;
}/*# sourceMappingURL=style.css.map */
```
となっており、scssの内容がcssに変換されてファイルが生成されていることが確認できます。この状態でブラウザを確認すると、見出しの文字色が赤に変化していることがわかります。

以後、scssファイルを更新し保存すると自動的にcssファイルも変換されます。

**※注意点として、cssファイルを直接編集するのではなく、scssに記述しcssに変換するようにしましょう。**

# SCSSの記述方法について

今の状態だと、SCSSのメリットは特に感じられないかもしれません。scssとcssの内容が同じだからです。

ここから、scssの独自の主な記述方法のいくつかについて解説していきます。

## コメントアウト

CSSのコメントアウトは

```
/* コメントアウト */
```
のみでしたが、scssでは加えて

```
// 一行コメントアウト
```
も使用することができます。

これは、scss内だけでのコメントになりますので、cssに反映されることはありません。

## ネスト

SCSSでは、ネストを使用して記述することができます。

例えば、h1をhoverした時に文字色を変えたい場合CSSで記述すると

```css
h1 {
  color: black;
}
h1:hover {
  color: red;
}
```
となりますが、SCSSで記述すると

```scss
h1 {
  color: black;
  &:hover {
    color: red;
  }
}
```
となり、h1に関係するセレクタを入れ子にして書くことができます。このSCSSを変換すると上のCSSに変換されます。

「**&**」マークは親セレクタを指します。

このマークの使い方はもう一つあります。

`index.html`の内容を以下に変更しましょう。

```html:index.html
<!DOCTYPE html>
<html lang="ja">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <link rel="stylesheet" href="css/style.css" />
  </head>
  <body>
    <header>
      <h1>見出し</h1>
    </header>
  </body>
</html>
```
header要素の中にh1があります。

今回はこのheader要素に背景色をつけて、h1には先程のhoverを設定します。

CSSで記述すると

```css:style.css
header {
  width: 600px;
  height: 60px;
  background-color: #aaafff;
}
header h1 {
  color: black;
}
header h1:hover {
  color: red;
}
```
となりますが、SCSSで記述すると

```scss:style.scss
header {
  width: 600px;
  height: 60px;
  background-color: #aaafff;
  & h1 {
    color: black;
    &:hover {
      color: red;
    }
  }
}
```
となります。

5行目の
```
& h1 {
```
は、「&」と「h1」の間にスペースがあります。このスペースは「h1」が「header」の子孫セレクタであることを指します。

そして、この場合「&」は省略して次のように書くことができます。


```scss:style.scss
header {
  width: 600px;
  height: 60px;
  background-color: #aaafff;
  h1 {
    color: black;
    &:hover {
      color: red;
    }
  }
}
```

SCSSのネストを使うことによって、煩雑になりやすいCSSの記述もシンプルかつ見やすく書くことができます。

## 変数

よく使う値や色などを変数に格納して使用することができます。

例えば、紫をメインカラーで赤をサブカラーと変数で定義しそれを使用するSCSSを記述します。

```scss:style.scss
$mainColor: #aaafff;
$subColor: red;

header {
  width: 600px;
  height: 60px;
  background-color: $mainColor;
  h1 {
    color: black;
    &:hover {
      color: $subColor;
    }
  }
}
```
変数はSCSSの中で
```
$変数名：値;
```
で定義し、使用する場合は
```
プロパティ名：$変数名;
```
と記述します。

# その他SCSSの記述について

ここでは取り上げませんが、まだまだSCSSには便利な記述方法があります。

興味のある方は検索してさらにコーディングを便利にしてもらえればと思います。
