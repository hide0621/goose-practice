# gooseについて

公式は[こちら](https://github.com/pressly/goose?tab=readme-ov-file#down)

記事は[こちら](https://www.issoh.co.jp/tech/details/3401/#i-2)と[こちら](https://zenn.dev/skrikzts/articles/4b785ce264a5c9)

## setup

以下のコマンドを使用

`brew install goose`

## 使い方

1. マイグレーション先のDBを稼働させておく
2. マイグレーション用のファイルを以下のようなgooseコマンドで生成する

例：`goose create add_post_table sql`

このコマンドによりカレントディレクトリにて`20241028051727_add_post_table.sql`のようなsqlマイグレーションファイルが生成される

3. gooseコマンドを使ってスキーマを作成する

例：`goose postgres "host=hostname port=portnumber user=username password=yourdbpassword dbname=dbnameforyourpostgres sslmode=disable" up`

なお、テーブルをdropしたいなら...

例：`goose postgres "host=hostname port=portnumber user=username password=yourdbpassword dbname=dbnameforyourpostgres sslmode=disable" down`
