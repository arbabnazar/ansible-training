# Ansible トレーニング
[Ansible](http://docs.ansible.com/ansible/) はリモートから他のマシンを管理して構成を自動化するための構成管理ツールです。Chef や Puppet等、他の構成管理ツールに比べて、以下のような特徴があります。

- 既存の ssh インフラストラクチャーおよび Python実行環境を利用するため、エージェントレスである
- 専用のサーバーが不要。例えばノートPCから100台のマシンを管理するようなこともできる
- シンプルであるため、気軽に学び始めることができる
- "Facts"と呼ばれる機能によってタスク実行の直前に、実行対象のシステムおよびその環境についての情報を収集することができる
- Ansibeのタスクには冪等性 (idempotency) がある

あらかじめ準備しておくもの:
------------------------------
自分のPC(MacOSX/Linux/Windows)に以下のソフトウェアをインストールしておいてください。

 1 - [Vitualbox](https://www.virtualbox.org/wiki/Downloads)

 2 - [Vagrant](https://www.vagrantup.com)
 
 3 - [Git](https://git-scm.com/downloads) * Linux は yum や apt等からインストール
 
 4 - [Git for Windows](https://git-scm.com/download/win) ※ Windows のみ

コース環境のダウンロード
-----------------------
コース環境を入手するには、以下のコマンドを実行してください。Windowsの場合は、[Git for Windows](https://git-scm.com/download/win)の Git bashから実行してください。

```shell
git clone https://github.com/arbabnazar/ansible-training.git
cd ansible-training
```

このダウンロードファイルの中に、トレーニングで使用する仮想マシンを構築、運用するための `Vagrantfile`が含まれています。手動で"Vagrant box"を入手する必要はありません。単に以下のコマンドを実行するだけで、トレーニング環境の準備が整います。（ネットワーク環境によりますが、およそ10分程度かかります）
```shell
vagrant up
```
It will bring up the **control** machine (Ubuntu 14.04 LTS) and perform the following actions on it:
- Add the latest  Ansible repository
- Add the insecure RSA key that will be used for client machines
- Add some additional SSH config

Once your machine is up and running, login to the control machine using the following command:
```
vagrant ssh
```
There are two other machines, which will be used as clients for practice, on which we'll perform the  configuration using ansible from *control* machine, given them the named 
- web
- database

To start these machines, use the following commands:
```
vagrant up web
vagrant up database
```
If something will go wrong, please refer to the Vagrant's [Getting Started Guide](http://docs.vagrantup.com/v2/getting-started/index.html).

For  grammar, spelling mistake etc... please create a PR for the master branch directly.

Thank you!
