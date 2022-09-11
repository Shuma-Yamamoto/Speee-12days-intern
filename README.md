# 不動産の口コミサイト
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


## 目指すべき姿

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
