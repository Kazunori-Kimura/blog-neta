2014-02-19
====================

OpenGL
-------------

OpenGLをJavaScriptで使いたい → canvas & WebGL

- [Getting started with WebGL](https://developer.mozilla.org/ja/docs/Web/WebGL/Getting_started_with_WebGL)

> WebGL は、HTMLの canvas 内で 3D レンダリングを実行するために、Web コンテンツで OpenGL ES 2.0 に基づく API を使用することを可能にします。

- [MMD.js](https://github.com/edvakf/MMD.js)

MMDをWebGLで動かす


### three.js

- [初心者でも絶対わかる、WebGLプログラミング＜three.js最初の一歩＞](http://html5experts.jp/yomotsu/5225/)
- [多彩な表現力のWebGLを扱いやすくする「Three.js」](http://www.atmarkit.co.jp/ait/articles/1210/04/news142.html)



OpenCV
----------------

OpenCVをJavaScriptで使いたい

- node-opencv
- node-webcl



Camera,Video
-----------------

JavaScriptでPCに搭載されているカメラ等にアクセスする方法。

- [Capturing Audio & Video in HTML5](http://www.html5rocks.com/en/tutorials/getusermedia/intro/)
- [[HTML5]getUserMedia APIを使ってカメラを表示させてみる](http://blog.o24.me/?p=253)

`getUserMedia()`ってやつを使うみたい。
カメラで取得した画像をCanvasに流し込むことになる模様。

ただ解析等をクライアントサイドで実施するのは重すぎるように思うので
Canvasの内容をサーバーサイドに送ってOpenCVで解析・画像処理した後
クライアントサイドに結果を返すのが良いのかな...

マーカー上にMMDデータを表示するだけで結構な負荷が掛かりそう。


### JSARToolKit

なんかやりたいことがほぼ実装されてそう。
でもあんまり更新されてないな。

- [JSARToolKit](https://github.com/kig/JSARToolKit)
- [JSARToolKit を使用した拡張現実アプリケーションの作成](http://www.html5rocks.com/ja/tutorials/webgl/jsartoolkit_webrtc/)



WebRTC
----------------

[WebRTC(wikipedia)](http://ja.wikipedia.org/wiki/WebRTC)
> WebRTC (Web Real-Time Communication)とはWorld Wide Web Consortium (W3C)が提唱するリアルタイムコミュニケーション用のAPIの定義で、プラグイン無しでウェブブラウザ間のボイスチャット、ビデオチャット、ファイル共有ができる。

P2P(サーバー不要)でやり取りするのが目的。 今回やりたいこととはちょっと違う。

