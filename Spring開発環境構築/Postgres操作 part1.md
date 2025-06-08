#postgres
- バージョン確認
  psql --version
- パスを確認
  which psql
- データベースの確認
  psql -l
### 起動
バージョンを14以外を選択してインストールしている場合に
起動すると下記エラーが発生
Error: Formula `postgresql@14` is not installed.

- バージョンを指定して対応する
　brew services start postgresql@XX
### 接続
psql -h ホスト名 -p ポート番号 -U ユーザー名 -d データベース名
例) psql -h localhost -p 5432 -U endo -d postgres

### 接続解除
¥q

### 停止
brew services stop postgresql

以上の内容参考ソース
https://mkdir-cd.hatenablog.com/entry/2025/01/06/232458