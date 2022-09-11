# Speee-12days-intern
# 不動産の口コミサイト：サーテイン
![image](https://user-images.githubusercontent.com/70557787/189520007-71f67519-e1f1-412c-951d-328d5a6cf21d.png)

このプロダクトは、株式会社Speee 12daysインターンで制作したものです。<br>
12日間のうち、最初の3日間が開発計画フェーズで、残りの9日間が開発フェーズでした。<br>
開発は学生4人のチームで行い、これを主に1人のメンターがサポートする形です。

# 開発計画
## 現状
不動産取引を経験したユーザの体験談が、これから不動産取引をしようと考えているユーザにあまり届いていない。<br>
したがって、不動産会社を選ぶ際の基準を持つことができず、不安を抱えたまま取引せざるを得ない状況にある。

## 目指すべき姿
不動産取引を経験したユーザの体験談が、これから不動産取引をしようと考えているユーザに届く。
結果として、ユーザは不動産会社を選ぶ際の基準を持つことができ、安心して取引をすることができる。

## 上記を踏まえたうえでの開発計画
![image](https://user-images.githubusercontent.com/70557787/189520654-f2632d7f-120d-4ed0-ab6f-696332df93e8.png)

# 開発の達成度
![image](https://user-images.githubusercontent.com/70557787/189520700-46a5f603-053f-4185-99d5-121c8a849fc7.png)

# 開発の振り返り
![image](https://user-images.githubusercontent.com/70557787/189520723-6402f17b-d138-4f76-a73a-1620620e121f.png)

# 技術面で工夫したこと
ユーザが不動産会社に査定依頼をするための「査定依頼フォーム」ページの作成において、ユーザフレンドリーな画面を意識した。<br>
例えば、バックエンドで実装した入力フォームのバリデーションに通るように、入力項目の横に注意書きをしたり、必須項目には「必須」マークを付けたり、バリデーションに通らなかった場合はエラーメッセージを表示（ja.ymlファイルでデフォルトでは英語の文章を日本語化）したりなど。

# プロダクトの動かし方

## 環境構築

``` bash
docker-compose build
docker-compose run --rm app yarn install --check-files
docker-compose run --rm app bin/setup
```

## サーバー起動

``` bash
docker-compose up
open http://localhost:13000
```

### ローカルで起動する場合
``` bash
docker compose up db
rails s
open http://localhost:3000/
```

## テストの実行

``` bash
docker-compose run --rm app bin/rails test
```

## Rubocop の実行

``` bash
docker-compose run --rm app rubocop
```

## サーバへのデプロイ

0. (初回のみ) `aws ecs run-task --cluster internship-aug2022-2 --task-definition internship-aug2022-2-db-create --launch-type FARGATE --network-configuration '{"awsvpcConfiguration":{"subnets":["subnet-0334f01a7f2e84910","subnet-06e60f8f517606654","subnet-0df45f1bdece2446d"],"securityGroups": ["sg-0ee03f05942978041"],"assignPublicIp":"ENABLED"}}' --count 1` で `rails db:create` を本番環境のDBに適用し、この Rails アプリが使用する MySQL のデータベースを作成する。
1. [GitHub Actions タブの deploy ワークフロー](https://github.com/speee/hr-eng-internship-2022-1st-team-2/actions) に移動
2. `This workflow has a workflow_dispatch event trigger.` の右側にある `Run Workflow` ボタンをクリック
3. `Use workflow from` のセレクトボックスからデプロイ対象のブランチを選択
4. `Run Workflow` ボタンをクリック

## ステージング
https://aug2022-2.intern.speee.in
