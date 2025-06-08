#docker #dockerfile
FROM openjdk:21-jdk-slim
- ベースイメージを指定しています
WORKDIR /app
- 「コンテナの中で作業をする場所（フォルダ）を決める命令」
    コンテナの中で　/appフォルダという場所で作業する
COPY build/libs/*.jar app.jar
- ホストマシン（あなたのパソコン）の build/libs/ ディレクトリにある .jar ファイルを、コンテナ内の /app/app.jar にコピーします。
- *.jar は Gradle のビルドで作られる Spring Boot のアプリ本体。
- 名前を app.jar にリネームし、固定することで扱いやすくしています。
ENTRYPOINT ["java", "-jar", "app.jar"]
- Dockerコンテナを 起動したときに最初に実行するコマンド を指定しています。
