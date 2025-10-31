---
title: Conohaでマイクラ鯖を建ててみた(付録？付き)
tags:
  - Conoha
  - ConohaVPS
  - Conoha-for-GAME
private: false
updated_at: '2024-12-12T18:13:17+09:00'
id: 58ca488479a773760b63
organization_url_name: null
slide: false
ignorePublish: false
---
# はじめに
これは[ConoHa Advent Calendar 2024](https://qiita.com/advent-calendar/2024/conoha)の13日目の記事です。
自分はマイクラが大好きで、自分で色々作ってみたい！と思いプログラミングを始めて、今では様々なサーバーの管理者をしています。
そして今回なぜConohaを紹介しようと思ったかと言うと、最近Conohaのクーポンが2000円分ほどあり、ドメインを取得しました。それ以降VPSもやっていると言うことで、どんな感じ何だろう、と思い今回自分で試してみる兼紹介記事を書いてみようと思いました。
こう言う記事を書くのは久しぶり(Qiitaでは初めて)なので、どうぞよろしくお願いします。

# 用意するもの
- Conohaアカウント
- お金

# 作り方(簡単 3Step)
1 青色の追加ボタンを押す
2 イメージタイプを選択(今回はMinecraft Bedrock)
3 サーバーを作成を押す
サーバーリストに追加できました！

サーバーを起動してこのような画面が出ていたら成功です！
![IMG_4341.jpeg](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3113699/4bb799cf-c05c-ce84-5631-87b99a4e2be0.jpeg)

ちなみに1GBメモリーのプランでTNT5万個は耐えました！
![IMG_4149.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3113699/697a5bec-65ad-56e8-0402-492a6154271b.png)

## 付録(?)コーナー
<details><summary>付録１ SSH接続をする</summary>
1 サーバーの詳細設定ボタン(⚙️マーク)を押す。

2 セキュリティグループにIPv4-6-SSHを追加して保存します！

3 後は普段通りにSSH接続をサーバーのIPにするだけ！

(普段自分で使っているSSH鍵がある場合、設定方法は付録2をご覧ください)
</details>
<details><summary>付録２ SSH鍵をアップロードor追加する</summary>
1 セキュリティタブを開きSSH Keyを押す。

2 自分の行いたいことに合わせて、ボタンを選択してください！
(自動作成 or インポート)
(ネームタグはご自由にどうぞ！)
![IMG_4500.jpeg](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3113699/d146f261-6735-aa45-ac3f-55b3a938a6f2.jpeg)
4 新規サーバーを追加する時に、詳細設定を押してSSH Keyの部分をキーを選択にして、インポートしたキーを選択してください！
(この時にセキュリティグループにIPv4-6-SSHを追加しておくことを推奨します！)
![IMG_4501.jpeg](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3113699/770d88ac-ee9c-73fc-2efe-df9422b54fcd.jpeg)
</details>
<details><summary>付録３ 使わないわけにはいかない！ マイクラの管理パネル！</summary>
みなさん！マイクラ鯖に必要なものといえばなんですか！やっぱり簡単な操作パネルですよね！なんとConohaにはそれがあります！
これです！

![IMG_4502.jpeg](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3113699/2e2fa3cd-3e75-2916-6682-46f4aa81c91b.jpeg)
初めてアクセスするとBASIC認証を求められますが、ユーザー名はroot パスワードは契約時に設定したrootパスワードです。


アクセスするとこんな感じ！(縦長画像です)
![IMG_4504.jpeg](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3113699/6ec56d25-8af3-3547-c89b-4e013afaf93a.jpeg)
画像ではスマホですが、パソコンでも楽々操作が可能です！
主にできる機能
- マイクラサーバーとSSHサーバーの起動・停止
- サーバーのバックアップと自動起動設定
- バージョン情報(ここからアプデもできる)
- サーバーの情報(起動時間など)
- サーバー設定(ゲームモード・難易度・ワールドタイプ)
- ホワイトリスト
- バックアップ一覧

です！
(Java版ではプレイヤー管理などもできて最強です！)
ですがこの最強パネルにも意外な弱点(統合版のみ？)があります🥺それについては次で書きたいと思います。
</details>
<details><summary>付録４ 意外な弱点とは</summary>
このパネルでできないこと(特に鯖管ガチ勢(？))には痛いものがあります。

- サーバーソフトウェアのコンソール
- プレイヤーの権限管理(OPなど)
です。
###### サーバーソフトウェアのコンソール
(自分が見落としてるだけであるかも？)
マイクラサーバーのコンソールでは、様々なコマンドをサーバーに入ることなく、実行することができます。
それをできないのはとても難しいです。
特にJava版などPCがないとできないものでは、外からの管理ができにくいので、別途管理プラグインなどを入れる必要があります。
###### プレイヤーの権限の管理(統合版限定？・時間はかかるが対処法あり)
マイクラサーバーでは基本的にOP(オペレーター)権限がないと、ゲームモードなどを変えることができません。それを解消するための手順(自分流)を紹介します。
1 まずSSHでサーバーにアクセスします。
そうするとmotdのところに次のようなメッセージが出ます。
![IMG_4505.jpeg](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3113699/23ccf4da-450c-34cd-a447-e44af01a0140.jpeg)
```shell:console
cd /opt/minecraft_be_server
```
と打ってみてください！
そうするとマイクラサーバーの構成ファイルが表示されます。
![IMG_4506.jpeg](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3113699/ae4f679a-1451-3e76-2417-88cc5c6ee9b8.jpeg)
この中のpermissions.json
```json:permissions.json
[
　{
　　”permission”: “operator”,
　　”xuid”: “2535461334923392”
　}
]
```
でどんどん増やしていけば権限を追加できます(詳細は省きます)
(xuidは https://api.geysermc.org/v1/xbox/xuid/[GamerTag] で調べられます。)
</details>

### 他にも色々ありますが、全部紹介すると睡眠時間がなくなるので、自分で試してみてください！ 良いマイクラ&Conohaライフを！！
