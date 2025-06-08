#spring #環境構築S
# 環境構築
VSCodeでの開発を想定。
1. プロジェクトを作成する
    WebでSpring initializrを使用してプロジェクト構成を作成する
    VSCodeのコマンドパレットを使用してプロジェクト構成を作成する
    ⚠️ PCで通しているJavaのバージョンと一致しないと
    　新たにjavaクラスが作成できない
2. DBの設定を行う
　　- 設定ファイルに直接記載する
　　  簡単だが、ハードコーディングとなるため非推奨
　　- 環境変数を作成する
　　  設定とソースを分離できるため推奨
　　環境変数の設定方法
　    .envファイルを作成し、そこに設定を記載する
　    記載内容
　     SPRING_DATASOURCE_URL
　     SPRING_DATASOURCE_USERNAME
　     SPRING_DATASOURCE_PASSWORD
　     SPRING_DATASOURCE_DRIVERCLASSNAME

### Dockerの用意
.envファイルを読み込んでから起動させる構成としたいため、Dockerを使用してビルドを行う構成とする
1. gradleで一度ビルドする
   テスト環境の用意は初期段階では、まだ行わないためテスト環境を除いたビルドを行う
   ./gradlew build -x test
   -x test => テストを除外（“exclude”）してビルド
   テストを除外せず行う場合、 ./gradlew build とコマンドを実行する
2. Dockerfileを作成する
   ![[Dockerfile]]
3. docker-compose.ymlファイルを作成する
   SpringとDBを同時に起動させるために必要なファイルを作成する
### Gitにアップしないものを記載
.gitignoreファイルにアップしたくないファイル名を記載すると、gitにプッシュした際にそのファイルはアップされない
今回、新たに追加するファイルは.env, /build, ¥*/jarの3つ

### 起動方法
./gradlew build -x test
docker-compose up --build
このコマンドを順に実行する