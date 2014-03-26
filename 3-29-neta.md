
# 3/29向けメモ

## 今回のAWS講習会と関係あるキーワード

### Immutable Infrastructure

> 一度作成したサーバー（インフラ）は設定変更などを行わず、不変なものとして扱います。デプロイメントのたびに、新しいインフラを構築し、既存のインフラは不要になった後に廃棄します。
> [NTT Data | Immutable Infrastructure～デプロイメントをめぐるシステムインフラの管理～](http://www.nttdata.com/jp/ja/insights/trend_keyword/2013122601.html)

> Immutable Infrastructureの話題が目に付くようになったのは昨年、2013年あたりからで、Kief Morris氏が2013年6月13日付けで「ImmutableServer」という記事をMartin Fowler氏のWebサイトにポスト、6月23日には「情熱プログラマー」の著者などとして知られるチャド・ファウラー氏が自身のブログに記事「Trash Your Servers and Burn Your Code: Immutable Infrastructure and Disposable Components」をポストして、「Immutable Infrastructure」という言葉が広く使われる流れを作ったように思います。
> [Publickey | 「Immutable Infrastructure（イミュータブルインフラストラクチャ）と捨ててしまえるコンポーネント」 チャド・ファウラー氏](http://www.publickey1.jp/blog/14/immutable_infrastructure.html)


### IaaS (Infrastructure as a Service)

* Amazon Web Services
* Google Compute Engine / Managed Virtual Machines


### 構成管理ツール

構成管理(Configuration Management、CM)を行う代表的なOSS

* Puppet
* Chef
* Salt
* Ansible


### 継続的インテグレーション (CI)

* [Jenkins](http://jenkins-ci.org/)
* [Travis CI](https://travis-ci.org/)

> Jenkinsは、ソフトウェアのビルドやcronで起動するジョブなどの繰り返しのジョブの実行を監視します。これらのうち、Jenkinsは現在次の2つのジョブに重点を置いています。
> 1. *継続的な、ソフトウェアプロジェクトのビルドとテスト*: つまり、CruiseControlやDamageControlが行うこと。 一言で言えば、Jenkinsは、容易ないわゆる「継続インテグレーションシステム」を提供し、開発者が変更をプロジェクトに統合でき、ユーザーがより新しいビルドを容易に取得できるようにします。自動化された継続的なビルドは、生産性を向上させます。
> 2. *外部で起動するジョブの実行監視*: cronによるジョブやprocmailのジョブで、リモートマシンで動作するものも含みます。例えばcronについて言えば、出力をキャプチャーした定期的なメールだけ受信し、こつこつとそれを見ます。おかしくなっていることに気がつくかどうかは、すべてあなた次第です。Jenkinsは出力を保存し、 いつおかしくなったのか容易に把握することができるようになります。


### テスト駆動開発 (TDD)

> テスト駆動開発 (てすとくどうかいはつ、test-driven development; TDD) とは、プログラム開発手法の一種で、プログラムに必要な各機能について、最初にテストを書き（これをテストファーストと言う）、そのテストが動作する必要最低限な実装をとりあえず行った後、コードを洗練させる、という短い工程を繰り返すスタイルである。
> [Wikipedia | テスト駆動開発](http://ja.wikipedia.org/wiki/%E3%83%86%E3%82%B9%E3%83%88%E9%A7%86%E5%8B%95%E9%96%8B%E7%99%BA)


### GitHub / Git

* TravisやJenkinsとレポジトリを連携

### Docker

* [これから始める「DockerでかんたんLAMP環境 for CentOS」](http://knowledge.sakura.ad.jp/tech/1811/)


----------------

## 全然講習会と関係ないけど、やりたいこと

* node.js
* Raspberry Pi
* Google Glass (に代表される wearable device)
* PhoneGap (Apache Cordova)
  - Objective-Cはもう書きたくない...


## 将来の勉強会とか今後の方針

* クラウドに関する勉強会は継続して進めたい
  - AWSのノウハウとか蓄積したい
  - AWS上で動かすアプリの開発
  - プライベートクラウド環境の構築 (できればAWS互換)

* GitHubのユーザーを増やしたい
  - Git / GitHub の啓蒙活動 (勉強会が必要？)

* Android研究会はなんとか開催してほしい
  - ここをトリガーにWearableな方向の活動を広げたい
  - スマホ向けアプリならPhoneGapで作るけど。

* 勉強会の裾野を広げる活動
  - Webアプリケーション開発入門など、初学者向けの講習会を開催して参加者を集める

* 技術的な話題で盛り上がる機会をもっと作りたい
  - Online/Offline問わず。
  - ライトニングトーク会は企画倒れだった
  - FacebookのMCEA関西パートナーのグループを活性化できるといいな
  - MCEAパートナー以外の方も参加できる会合を増やす？

