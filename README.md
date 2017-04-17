# Ansible トレーニング
[Ansible](http://docs.ansible.com/ansible/) はリモートから他のマシンを管理して構成を自動化するための構成管理ツールです。Chef や Puppet等、他の構成管理ツールに比べて、以下のような特徴があります。

- 既存の ssh インフラストラクチャーおよび Python実行環境を利用するため、エージェントレスである
- 専用のサーバーが不要。例えばノートPCから100台のマシンを管理するようなこともできる
- シンプルであるため、気軽に学び始めることができる
- "Facts"と呼ばれる機能によってタスク実行の直前に、実行対象のシステムおよびその環境についての情報を収集することができる
- Ansibeのタスクには冪等性 (idempotency) がある

あらかじめ準備しておくもの：
------------------------------
トレーニング用の仮想マシンを実行するためのPCを用意してください。RAMは 4GB以上、CPUは仮想化支援機能(VT-x等)が搭載されている必要があります。

自分のPC(MacOSX/Linux/Windows)に以下のソフトウェアをインストールしておいてください。各ソフトウェアの名前の部分が、ダウンロード元サイトのリンクになっています。なお、Windowsの場合は 64bit OSかつ 仮想化支援機能(VT-x等）をBIOS上で有効にしてある必要があります。（所要時間約60分）

 1 - [Vitualbox](https://www.virtualbox.org/wiki/Downloads)  ... 仮想マシン実行環境 ※ CentOS/RHELの場合は dkms パッケージも必要

 2 - [Vagrant](https://www.vagrantup.com)  ... 仮想マシン環境等デプロイツール
 
 3 - [Git](https://git-scm.com/downloads)  ... ドキュメント・コード管理およびバージョン管理ツール  ※ Linuxの人は yum や apt等からインストール
 
 3’ - [Git for Windows](https://git-scm.com/download/win)    ※ Windowsの人はこちら  （bash, vim, git等が使えるようになります）

コース環境のダウンロードと実習環境の構築：
-----------------------
コース環境を入手するには、以下のコマンドを実行してください。Windowsの場合は、[Git for Windows](https://git-scm.com/download/win)の Git bashから実行してください。（所要時間約60分）

```shell
host$ git clone https://github.com/yasufumic/ansible-training.git
host$ cd ansible-training
```

このダウンロードファイルの中に、トレーニングで使用する仮想マシンを構築、運用するための `Vagrantfile`が含まれています。手動で"Vagrant box"を入手する必要はありません。単に以下のコマンドを実行するだけで、トレーニング環境の準備が整います。（初回起動時は、ネットワーク環境にもよりますが、およそ10分程度かかります）
```shell
host$ vagrant up control
```
この段階で、**control** 仮想マシン (CentOS7.2) が起動し、続いて以下のタスクが実行されます。
- Ansibleのインストールに必要な yum リポジトリの追加
- 管理対象マシンにアクセスするための SSH公開鍵アクセス
- その他SSH関連の設定等

 ※ 仮想マシンが起動できなかった場合は、システムリソースの不足、あるいはBIOSでの仮想化支援機能設定が無効である可能性があります。

**control**仮想マシンが起動したら、以下のコマンドでログインし、コース環境ファイルにアクセスできることを確認してください。
```
host$ vagrant ssh control
vagrant@Controll$ ls
```

**crontrol**仮想マシンの他に、以下の2台の仮想マシンがあります。これらは管理対象となるクライアントです。

- web
- database

これらの仮想マシンを起動するために、ホスト側で以下のコマンドを実行してください。
```
host$ vagrant up web
host$ vagrant up database
```

続いて、**control**上で以下のコマンドを試します。
```
vagrant@Control$ ansible all --list-hosts
vagrant@Control$ ansible all -m ping
```

 ※ なお、この段階で、エラーが出たり、何もファイルが見えていない場合は、デプロイに失敗しているので、以下のコマンドをホスト上で実行し、一旦仮想マシンを削除して、再度のデプロイを試行してください。


```
host$ vagrant destroy
host$ vagrant up
```

Vagrantの動作について問題があった場合は、このサイトを参照してください。 [Getting Started Guide](http://docs.vagrantup.com/v2/getting-started/index.html).

このドキュメントや手順に関する問題点や要望などは、この github の master branchに Pull Requestしてください。

Thank you!
