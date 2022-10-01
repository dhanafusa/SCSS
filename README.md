![](sass.svg)

# SCSSの導入と擬似要素について

SCSSはSassというCSSを拡張した言語の種類の一つです。

CSSの記述がより書きやすくなり、ネストの使用や変数の使用や複数のCSSファイルの読み込みなどが可能になります。

SCSSはプリプロセッサとなっているので、コンパイルが必要です。SCSSからCSSに変換することでHTMLと連携することができます。

今回はVSCodeの拡張機能を使ってSCSSを記述する方法とコンパイルをしてCSSに変換していきます。

# 導入するVSCode拡張機能

## Live Sass Compiler

この「Live Sass Compiler」をインストールすることによって、SCSSファイルからCSSファイルに自動変換してくれます。

自動変換されたCSSをHTMLから読み込むことによってCSSを適用することができます。

まずはVSCodeに拡張機能「Live Sass Compiler」をインストールしましょう。

# SCSSの記述について

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
