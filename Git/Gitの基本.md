#git #github #fleeting 

# Gitリポジトリの作成〜コピーまで
- 初期化コマンド
  `git init` --> Gitリポジトリの初期化
  これで.gitというサブディレクトリが作成される。リポジトリに必要なファイルががその中に格納される。
  ！この時点ではバージョン管理を行なっていない。
- 追加コマンド
  `git add` → `git commit`
  これで監視対象のファイルを持つGitリポジトリができる
- クローンコマンド
  `git clone` --> 既存のGitリポジトリのコピーの取得
  サーバーが保持するデータを、ほぼすべてコピーする
---
# Gitへの記録
各ファイルは、追跡されているものと追跡されていないものがある。
1. 追跡されているもの
   直近のスナップショットに存在したファイルのこと
   --> Gitは全てのファイルの状態をスナップショットを撮り、
   　　それへの参照を格納する
   -->スナップショットとは、ある時点の状態を記録・保存すること
   ファイルは下記三つの状態がある
   - 変更されていない
   - 変更されている
   - ステージされている
2. 追跡されていないもの
   - スナップショットに存在しない、かつ、ステージングされていないこと
3. 無視されるもの
   自動生成されるファイルやセキュリティー面で公開したくないもの
   .gitignoreファイルを作成して、そこに記載したファイルは監視されない
ファイルが変更されれば、ファイルのステータスは変更されている状態となる。
それをステージし、コミットするとGitで記録される。

### 状態の確認
`git status` -->ファイルがどの状態にあるかを知るために使用する
最新状態や、追跡されていないファイルが存在しない場合````
````
git status
On branch master
nothing to commit, working directory clean
````
READMEファイルを新たに追加した場合
```
 git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)

    README

nothing added to commit but untracked files present (use "git add" to track)
```
---
### ファイルの追跡の開始
`git add` を使用する
上記READMEファイルを追跡する場合
`git add README`
```
git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

    new file:   README
```
ステージされているかの判断をChanges to be committed:ここに表示されているかで判断する。

ステージされているファイルが変更された場合
```console
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

    modified:   CONTRIBUTING.md
```
Changes not staged for commit:ここに表示される。
同様にgit add CONTRIBUTING.mdすれば解決する
※コミットする前に、また変更したら再度追加すること。

---
# 変更内容の確認
`git status` コマンド --> ファイルの状態を確認
`git diff` コマンド --> 変更行をパッチ形式で表示
### オプション
-  `git diff --staged` ステージされている変更と直近のコミットを比較
  　※ステージされていない変更だけの表示である
- `git diff --cashed` ステージした内容の履歴を見れる。

---
# コミット
コミットの対象となるのは、ステージされたものだけ。
つまり、`git add` をしていないファイルはコミットされない。
`git commit` を実行すると、指定したエディタが立ち上がる。
- `git config --global core.editor` エディタを指定できる
- `git commit -v` diffの内容がエディタに表示される
- `git commit -m` インライン形式でコミットメッセージを記述できる
- `git commit -a` ステージングエリアを省略するためのショートカット
  追跡対象のファイルを自動的にステージしてからコミットを行う
  = `git add` の省略が可能

--- 
# 削除
Gitから削除する場合の流れ
追跡対象から外す --> コミット
`git rm` --> `git commit`
- もし、変更したファイルをすでにステージしている場合は
  `git rm -f` で強制的に削除する
- Gitで追跡はさせず、ファイルは残したい場合
  `git rm --cached` 
  他にもglobパターンを渡すことも可能
  `git rm log/¥*.log` 
  globパターンとは？ [[globパターン]]

---
# 移動
Gitは明示的にファイルの移動を追跡しない。
ファイル名を変更したい場合、下記を実行
`git mb file_from file_to` 
実際は、下記と同じことになる
`mv README.md README
git rm README.md
git add README`
