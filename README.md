PhoneGap (Apache Cordova 3) でiOS Appの作成
============

はじめに
--------

PhoneGapこと、Apache Cordova (以降、単に"cordova"とします)
を使って、iOS7向けのアプリケーションを開発していきます。

まずは、HelloWorldアプリを作って開発手順を確認してみます。

### 開発環境について

以下の開発環境で作業したログをまとめています。

- MacOS X (10.8)
- Xcode5.4 (含むCommand-Line Tools)
- Node.js (v0.10.24)
- Apache Cordova v3.3.0

nodeは既にインストールしてある前提です。
それ以外の開発ツールについては、手順の中でインストールしていくかもしれません。


### 参考

以下のDocumentを参考に、必要最小限の箇所を抜粋しています。
詳細は下記のリンク先を参照ください。

- [Apache Cordova](http://cordova.apache.org/)
- [Apache Cordova Documentation](http://cordova.apache.org/docs/en/3.3.0/)

PhoneGapとApache Cordovaの関係については
以下のTech Crunchの記事がわかりやすいです。

- [AdobeがApache Cordovaの私家版PhoneGapの3.0をリリース, APIをプラグイン化してより身軽に](http://jp.techcrunch.com/2013/07/20/20130719adobe-launches-phonegap-3-0-with-new-plug-in-architecture-apis-and-better-tools/)


PhoneGap のインストール
---------------------

npmでインストールします。超簡単!

```sh
sudo npm install -g cordova
```

これで、cordovaコマンドが使用できるはず。

! バージョン確認すること !


Project の作成
---------------------

[iOS Platform Guide](http://cordova.apache.org/docs/en/3.3.0/guide_platforms_ios_index.md.html)


`create`オプションでプロジェクトを作成する模様。

```sh
cordova create hello edu.example.hello HelloWorld
```

引数の説明は以下のとおり。

- hello : directory名
- edu.self.hello : アプリを識別するidentifier  
ドメイン名を逆にしたもの。今回は公開しないので、適当な名前を設定。
- HelloWorld : アプリ名

カレントディレクトリの下に`hello`ディレクトリが作成されています。
つづいて、iOS Appに必要なSDK等のセットアップを行います。

```sh
cd hello
cordova platform add ios
cordovaa prepare
```

`hello/platforms/ios/hello.xcodeproj`というファイルが
生成されているはずなので、XCodeで開いてみます。

あとは、通常のiOS App開発時と同じようにRunしてやれば、
シミュレータでの実行や実機への展開ができるはず。

この時、Xcode左側のツリーで`.xcodeproj`のファイルを選択する必要があります。
`.xcodeproj`と同じ階層に`www`という
htmlやjavascriptを配置するディレクトリが生成されていますが、
そのディレクトリを選択するのでは無いので注意すること。


index.htmlの修正
--------------------

実際の開発では、`hello/www`ディレクトリ以下に
必要なファイルを配置等していくことになります。

とりあえず、`index.html`を編集してみます。

```html
<!doctype html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <title>HelloWorld</title>
</head>
<body>
    <h1>Hello, World!</h1>
    <p>こんにちは、こんにちは！</p>
</body>
</html>
```

で、Xcodeに戻ってRunしてみます。



-------------------------


勤怠管理アプリの開発
====================

Apache Cordovaを使って、前に作ったiOSアプリのバージョンアップ版を開発してみることにします。

簡単な仕様は以下の通り。

- 毎日の出勤・退勤時間を記録する
- 事前に設定された休憩時間を差し引いて、勤務時間を自動的に算出する
- 入力された時間をアプリ内で保存する (外部データ送信は行わない)
- 月ごとに出勤・退勤時間をリスト表示する
- 月ごとに出勤・退勤時間をPDF,CSV形式でエクスポートする

- SinglePageApplication (HTMLはひとつ)
- JS: backbone.js (jQuery, underscore)
- CSS: Bootstrap

まぁ、ベーシックなWebアプリケーションですね。

まずはiPhoneを対象に作っていきます。
(余裕があれば最後にiPad対応を...)


プロジェクトの作成
--------------------

Cordovaで器となるプロジェクトを作成します。

```sh
cordova create timemanager com.kimura-kazunori.SimpleTimeManager SimpleTimeManager
```

前に公開したアプリが`TimeManager`だったので、被らないように頭に`Simple`と付けました。
これから作成するアプリを公開するかどうか分かりませんが。

とりあえず、iOSアプリとしてセットアップしておきます。

```sh
cd timemanager
cordova platform add ios
cordovaa prepare
```

以下の様なフォルダ構成になっています。

```sh
$ cd workspace/timemanager/
$ tree
.
├── merges
│   └── ios
├── platforms
│   └── ios
│       ├── CordovaLib
│       ├── EasyTimeManager
│       │   ├── Classes
│       │   ├── EasyTimeManager-Info.plist
│       │   ├── EasyTimeManager-Prefix.pch
│       │   ├── Plugins
│       │   ├── Resources
│       │   ├── config.xml
│       │   └── main.m
│       ├── EasyTimeManager.xcodeproj
│       │   └── project.pbxproj
│       ├── cordova
│       ├── platform_www
│       └── www
├── plugins
│   └── ios.json
└── www
    ├── config.xml
    ├── css
    │   └── index.css
    ├── img
    │   └── logo.png
    ├── index.html
    └── js
        └── index.js
```


まだ何も変更していませんが、とりあえずgitで管理するようにlocal repositoryを作りました。
.gitignoreを編集して、www以外のCordovaが生成したファイルは管理対象外にしておきます。

`.gitignore`

```sh
$ pwd
/workspace/timemanager
$ git init
$ git add .
$ git commit -m "first commit."
```


Webアプリケーション版の作成
---------------------

とりあえずCordovaの事は考えず、PCのブラウザ上で動作するWebアプリケーションとして作っていきます。
(このアプローチが正しいかどうか分かりません。最初からCordovaを想定して作るべきなのかも...)

実はbackbone.jsを使うのも初めてなので、作りながら細かい設計を詰めていきます。


開発環境の設定
--------------------

ライブラリ管理のために`bower`、テストのために`connect`を使います。
また、後でjsやcssの結合等を行うため、`grunt`も入れておきます。

node大活躍ですね。

```sh
$ sudo npm install -g bower
$ sudo npm install -g grunt-cli

$ npm init
:
$ npm install connect --save-dev
$ npm install grunt --save-dev
```

gruntの設定はある程度アプリケーションの形が見えてから設定します。
gruntのプラグインなども後回し。


### connectの設定

`connect`はnodeで稼働する簡易なHTTPサーバーです。
`www`ディレクトリを公開し、`http://localhost:3000`で接続できるようにします。

```js
//index.js
var connect = require("connect"),
    path = require("path");
connect.createServer(
    connect.static(path.join(__dirname, "www"))
).listen(3000);
```

### bowerの設定

[bower](http://bower.io/)はTwitterが作ったパッケージマネージャです。
フロントエンドのライブラリ管理に使用されます。

参考: [Bower入門(基礎編)](http://yosuke-furukawa.hatenablog.com/entry/2013/06/01/173308)

まず、bowerの初期設定を行います。

```sh
$ bower init
```

つづいて、ダウンロードしたライブラリの保存先を設定します。

```sh
$ mkdir www/vendor/assets/components
$ vim .bowerrc
```

`//.bowerrc`

```json
{
    "directory": "www/vendor/assets/components",
    "json": "bower.json"
}
```

### bowerでライブラリをダウンロード

必要なライブラリをダウンロードしていきます。

```sh
$ bower install jquery --save
$ bower install underscore --save
$ bower install backbone --save
$ bower install bootstrap --save
```

`www/vendor`を`.gitignore`に追加して
バージョン管理の対象外にしておきます。


これで、とりあえず開発に着手できる環境が整いました。
次は、アプリケーションの設計を行っていきます。


-------------------------------

アプリケーション設計
=================

画面設計
----------

基本的な画面は4つ

- 出勤・退勤画面 (main)
- 月間作業実績画面 (list)
- 出退勤修正画面 (edit)
- 設定画面 (config)


SinglePageApplicationの予定なので、
index.htmlに詰め込んでしまいます。


データ設計
-----------

入力されたデータはWebStorage(localStorage)に保存します。

```js
//出退勤データ
localStorage["date-yyyy-MM"] = JSON.stringify(
    {
        "dd" :
            {
                "start": {Date},    //出勤
                "end": {Date},      //退勤
                "rest": {Number},   //休憩時間
                "comment": {String} //コメント
            },
        "dd" : {} ...
    }
);

//設定
localStorage["setting"] = JSON.stringify(
    {
        "user_name": {string},    //氏名 (PDFで使用)
        "project_name": {string}, //案件名 (PDFで使用)
        "project_owner": {string},//顧客名 (PDFで使用)
        "tel": {string},          //連絡先 (PDFで使用)
        "rest": {Number}          //基準休憩時間
    }
);
```
