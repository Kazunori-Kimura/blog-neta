
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



