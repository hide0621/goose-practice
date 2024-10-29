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

## 注意点

**同じport番号**を使っているdbがある際はgooseのコマンド（ex. up, down）が失敗する

エラーメッセージ：`goose run: failed to ensure DB version: failed to connect ~. to server error: FATAL: role "postgres" does not exist (SQLSTATE 28000)`

同じport番号を使っているか否かは...

`lsof -i:5432`

このコマンドでわかる

このような問題の解消法として、稼働しているdbをstopすることが挙げられる

例えばhomebrew経由でpostgresを入れていて、docker containerのpostgresと同じport番号を使ってしまい競合が起こっている際は、コンテナじゃない方のpostgresを止めてみればいい

そのコマンドは`brew services stop postgresql@14`

成功時は

`Stopping postgresql@14... (might take a while)
==> Successfully stopped postgresql@14 (label: homebrew.mxcl.postgresql@14)`

と言ったメッセージが流れる

詳しくは[こちら](https://qiita.com/yuppymam/items/fad4eec0c5b7d6c86517#postgresql-%E3%82%92%E5%81%9C%E6%AD%A2)
