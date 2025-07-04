# Gitのブランチ運用

この文書において、「master」はすべて「main」に読み替えてもよい。

## A.単純化したGitHub Flow
- 使うブランチはmasterとfeature(行う作業ごとのブランチで、各々適切なブランチ名を付ける)
- 開発はすべてfeatureブランチで行う
- featureブランチで完成したものは、masterにマージする(原則、マージコミットを作る)
- masterブランチの内容は、都合のいいタイミングでリリース(デプロイ)する
- リリース用ビルドはmasterブランチで行う(追加事項)
- リリースに用いたコミットに対し、タグをつける(追加事項)
- readmeなど、機能にかかわらない軽微な変更はmasterブランチで行ってもよい(どっちかというとやらかしに対する言い訳)

参考(GitHub Flowの本来の運用)：https://gist.github.com/Gab-km/3705015

GitHub Flowとの違いは、以下のようになっている。
- ~~個人開発のため、プルリクエストと他人のレビューは原則として省く~~ プルリクエストを行い、botによる自動的なレビューを行う。botがいないなら省く。
- リリースのタイミングはmasterへのマージのタイミングではなく自分で管理する
    - ソフトウェアのバージョンアップなどは、複数の変更をまとめた程度の粒度で行いたいため
    - readme等の修正は開発とは別に行いたいため
- マージとリリースのタイミングが無関係になるため、リリースを判断できるように、タグをつける

## B.全部masterブランチ
- 使うブランチはmasterのみ
- コミットはmasterに直接行う
- よほど込み入った開発をする場合は、featureブランチを作成してもよい
- リリースはファイルごとに判断する

Gitの意味があまりないので、まともな開発案件では原則として用いない。
以下のようなリポジトリに使用する。

- どうでもいいリポジトリ(例えばここ)
- バイナリファイルが中心で、そもそもGitの長所を生かせないリポジトリ
- 開発からリリースまでに別の開発が入り過ぎて最新のmasterにマージする際に地獄を見るようなことが頻繁に起きるリポジトリ
- 他者を一切介入させない一本道のリポジトリ

## C.開発はdevelopブランチ、リリースはmasterブランチ
- 使うブランチはmasterとdevelop
- 開発はすべてdevelopで行う
- 機能が完成した時点でmasterへマージする
- masterブランチの内容は、都合のいいタイミングでリリースする

Bはあんまりだろうと思いつつも、Aは毎回ブランチを作るのが面倒ということで考えたパターン。

## D.git-flow
手順が複雑で面倒なので、今後はAに切り替えていく。
この運用だと、未完成案件のmasterブランチがずっとinitial commitだけになってしまう。
