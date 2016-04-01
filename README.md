# vagrant-ansible-centos67


ローカル開発環境用の仮想マシン作成と、サーバーの初期設定を行うVagrantfile + Playbookです。

ansible_local provisionerを使って仮想マシン側にAnsibleをインストールしてプロビジョニングします。

- 2台の仮想マシン作成 (CentOS6.7)
  - webサーバー(192.168.33.10)
  - dbサーバー(192.168.33.20)
- 各サーバー共通で実行するタスクをcommonロールとして定義
  - サーバー初期設定 (locale, timezone, ntpなど)
  - よく使うパッケージをインストール (wget, nkf, mlocaleなど)
- webサーバーで実行するタスクをwebロールとして定義
  - httpd, php7.0などをインストール
- dbサーバーで実行するタスクをdbロールとして定義
  - postgresqlなどをインストール(予定)


# 使用方法

### VirtualBoxとVagrantをインストール

Vagrant1.8以降なら大丈夫です。[こちら](http://qiita.com/ozawan/items/160728f7c6b10c73b97e#%E3%82%A4%E3%83%B3%E3%82%B9%E3%83%88%E3%83%BC%E3%83%AB%E6%89%8B%E9%A0%86) にインストール手順があります。

### VagrantfileとPlaybookをダウンロード

```
git clone https://github.com/ozawan/vagrant-ansible-centos67.git
```

### 仮想マシンを起動

```
cd vagrant-ansible-centos67
vagrant up
```

結構時間がかかりますが、初期設定済みのCentOS6.7が起動するはずです。

※Vagrant Box(bento/centos-6.7)が追加されていない場合は、ダウンロード→追加を行うので更に時間がかかります。
