---
title: ConoHaでVPSを使ってログをためてみよう
tags:
  - oracle
  - vps
  - Elasticsearch
  - Docker
  - Conoha
private: true
updated_at: '2025-12-08T21:25:13+09:00'
id: 59b320cb286262fe78eb
organization_url_name: null
slide: false
ignorePublish: false
---
:::note info
この記事は[ConoHa Advent Calendar 2025](https://qiita.com/advent-calendar/2025/conoha)の12日目の記事です。
:::
# ConoHaでVPSを使ってログをためてみよう

こんにちはおかかです。
今回は、ConoHa VPS上にDockerを構築して、Elasticsearchを使ってログをとってみようという感じです。
## 必要なもの
- ConoHa VPS 6Core 12GB SSD100GB (100/100Mbps)
┗ OS: Ubuntu 20.04 LTS
- Docker (書いている最中にDashboardみたら、アプリケーションテンプレートとしてありました。それを使うのをお勧めします)
## 構築編
### Step.1 ConoHaでVPSを起動する
まず、ConoHaでVPSを作ります。
<details><summary>作成時の画像（縦長で少し見にくめです）</summary>

![cp.conoha.jp_VPS_Service_Create_.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3113699/689579ff-9117-493c-9dc6-bc2980bf3c81.png)
</details>
ポートを後々開けていくのがめんどくさいので、すべて開けるセキュリティグループを設定していますが、実際に利用される場合は超絶非推奨です。
SSH Keyは事前に設定した公開鍵（今回は名前をGlobalで設定しています）を設定してSSHで秘密鍵でログインをするようにしておきましょう。

ここで、追加ボタンを押すと構築が始まります！
自分は大体水曜の18時ごろで時間帯か悪いのか、ホスト容量がないのかわかりませんが、3時間かかりました...
構築が完了したらメールが来るので、優雅にコーヒーを飲みながら待ちましょう☕
<details><summary>大量のコーヒー設置予定地</summary>
<h1>☕☕☕☕☕☕☕☕☕☕☕☕☕☕☕☕☕☕☕☕...（以下省略3000文字）</h1>
</details>

### Step.2 サーバーにログインしてDockerを導入しよう
見事構築が完了したあなたは次のステップへ進めます。
SSHする方法は省略しますが、`root@<ip>:22`で接続可能です。
ということで、Dockerをインストールします。
`curl https://get.docker.com | sudo sh`であとは待つだけです。
アプリケーションテンプレートでDockerを利用している場合は今更ですが、このStep.2はすべて省略可能です。
(root ユーザー以外で実行する場合、個人利用の場合はdockerグループにユーザーを追加しておくことをお勧めします)
### Step.3 Docker-elkでElasticsearchを立てよう
まず追加で必要なものを入れます。
```shell
sudo apt install -y git
```
これで、docker-elkのリポジトリを持ってきます
```shell
git clone https://github.com/deviantony/docker-elk.git
```
ここからはコマンド連発です。
```shell
# ポート開放
sudo ufw allow 5601/tcp
sudo ufw allow 9200/tcp
# sudo ufw allow 9300/tcp
cd docker-elk
# トライアル版ライセンスを、無効にする場合
# nano elasticsearch/config/elasticsearch.yml
# 8行目周辺にある `xpack.license.self_generated.type: trial`をコメントアウトします。
docker compose up setup
docker compose up -d
# Kibanaアクセス: http://<ip>:5601
# Elasticsearchアクセス: http://<ip>:9200
user: elastic
password: changeme
# でログインできます。
```
## 最後に
いかがだったでしょうか、もし外部からログを入れてみたい場合は、jsやtsだとHono&Elasticserchのnpmパッケージで実現可能です。
ぜひ皆さんもログをためてみてください
