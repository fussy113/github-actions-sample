# ワークフロー構文

## コンテキスト(Contexts)

実行時の情報やジョブの実行結果を保持するオブジェクト

### [github コンテキスト](https://docs.github.com/ja/actions/learn-github-actions/contexts#github-context)

ワークフロー実行時の情報、トリガーになったイベントの情報を保持

- 基本的には文字列型のプロパティ
- `github.event`のみオブジェクト型
