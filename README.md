# kickstart

## 目次
1. 概要
2. AWSの環境を用意する
3. asw cliを用意する

## 1. 概要
### 1. Kickstartとは？
Kickstartは以下の効果を発揮するためのプロジェクトです。
1. フルスタックエンジニアを目指す方の学習プロセスを提供。
2. プロジェクトの開始のための準備コストの軽減。毎度同じことやっているよねをコード化。

### 2. どんな技術にふれることが出来るのか？
勿論、今後も変化していきますが現状は以下の内容にふれることが出来ます。
- nextjs
- Firebase
- Vercel
- prism
- openapi
- docker / compose
- Rails
- aws ( fargate / API Gateway / RDS / CDK / ECR / NLB )

### 3. Kickstartの歩き方
- front / api / server / inflastractureと、4本の柱に別れています。
- 各READMEを読みながら何回でも納得がいくまで無限ループして下さい。実力が付きます。
- ドキュメント解りづらい、間違っているなどが有れば、お気軽にこちらからドンドンISSUEを発行してくだい。

<a id="kickstart-1" />

## 2. AWSの環境を用意する
### 1. AWSアカウントを持っていない方は登録を済ませて下さい。持っている方は、次の手順に進んで下さい。

### 2. 必要な情報を集める
| 参照名 | 使用箇所 | 取得方法 | ステータス |
| :--- | :--- | :--- | :--- |
| aws_access_key_id | api / github / actions / secretes |  | |
| aws_secret_access_key | api / github / actions / secretes |  | |
| aws_region | api / github / actions / secretes |  | |

既に、awsのaccess_key_idと、secret_access_keyを取得していて確認が出来る方は、[こちら](#kickstart-2)までスキップして下さい。

### 3. リージョンを確認して控える

<img src="https://user-images.githubusercontent.com/1023421/193435017-506e13a0-d8c2-46aa-b822-f30744c14bcc.png" width="400">

| 参照名 | 使用箇所 | 取得方法 | ステータス |
| :--- | :--- | :--- | :--- |
| aws_access_key_id | api / github / actions / secretes |  | |
| aws_secret_access_key | api / github / actions / secretes |  | |
| aws_region | api / github / actions / secretes |  | 取得済み |

### 4. IAMに移動する

<img src="https://user-images.githubusercontent.com/1023421/193435086-ca1c09d8-ef46-4ab3-983b-197beda9488f.png" width="400">

### 5. ユーザーに移動して、`ユーザを追加`をクリック

<img src="https://user-images.githubusercontent.com/1023421/193435121-682f953d-4917-4c49-8e15-ba09d5747937.png" width="400">

<img src="https://user-images.githubusercontent.com/1023421/193435212-5a63c0bf-0390-4159-b50f-f6dc9481d22a.png" width="400">

### 6. 名前を入力（なんでもいい）して、`アクセスキー - プログラムによるアクセス`にチェックして進む

<img src="https://user-images.githubusercontent.com/1023421/193435254-5c7cb3d1-d84a-477c-a44c-1b938cc8493f.png" width="400">

### 7. `既存のポリシーを直接アタッチ`をクリック

<img src="https://user-images.githubusercontent.com/1023421/193435346-7a14e880-cedb-4029-9ca2-4297f6b89c00.png" width="400">

### 8. 以下のポリシーをアタッチ
- AmazonAWSCloudFormationFullAccess

<img src="https://user-images.githubusercontent.com/1023421/193435376-1b2c9ea8-5d76-4e75-8b54-4d7c3edfb60e.png" width="400">

### 9. 何もせずそのまま進む

<img src="https://user-images.githubusercontent.com/1023421/193435402-634c3429-4771-4c8b-a252-6ce29204742e.png" width="400">

### 10. `ユーザーの作成`をクリック

<img src="https://user-images.githubusercontent.com/1023421/193435424-2702fd41-5cd1-45cc-96c7-6a92298aa9be.png" width="400">

### 11. クレデンシャル情報を控える
必ず、`.csvのダウンロード`を押して、csvを保存して下さい。この中に、`aws_access_key_id`と、`aws_secret_access_key`が書かれています。特に`aws_secret_access_key`は、ここでしか取得できず、控え忘れると再度ユーザーの作り直しとなります。

<img src="https://user-images.githubusercontent.com/1023421/193435521-2be4e88c-8076-4228-b31e-2dd003a17b46.png" width="400">

<a id='kickstart-1-11' />

| 参照名 | 使用箇所 | 取得方法 | ステータス |
| :--- | :--- | :--- | :--- |
| aws_access_key_id | api / github / actions / secretes |  | 取得済 |
| aws_secret_access_key | api / github / actions / secretes |  | 取得済 |
| aws_region | api / github / actions / secretes |  | 取得済 |

<a id="kickstart-2" />

## 3. aws cliを用意する

### 1. 以下の公式ページを参考に使用しているOS毎にインストールをする
[AWS CLI の最新バージョンをインストールまたは更新します。](https://docs.aws.amazon.com/ja_jp/cli/latest/userguide/getting-started-install.html)

### 2. 動作確認
以下の様にコマンドをうって、バージョンが表示されれば成功です。
```
$ aws --version
aws-cli/2.2.16 Python/3.8.8 Linux/5.15.0-48-generic exe/x86_64.ubuntu.20 prompt/off

```

### 3. 設定ファイルを作成する
設定ファイルの場所
```
/$HOME
  |- /.aws
       |- config
```

もし、ホームディレクトリに`.aws`ディレクトリが無かったり、またはconfigファイルが無かったりしたら作成をしてください。

### 4. 設定ファイル（`config`）の中身を記入する。
```
[default]
output = json
region = 上記で取得した、`region`
aws_access_key_id = 上記で取得した、`access_key_id`
aws_secret_access_key = 上記で取得した、`secret_access_key`
```

### 5. 動作確認
以下の様にコマンドをうって、自分のアカウント情報が取得できればcliの設定は成功です。
```
$ aws sts get-caller-identity
{
    "UserId": "XXXXXXXXXXXXXXXXX",
    "Account": "0000000000000",
    "Arn": "arn:aws:iam::0000000000000:user/kickstart"
}
```


