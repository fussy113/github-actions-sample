# 運用しやすいワークフローの設計

## ロギング

- ステップのデバッグログを出力する
  - `ACTIONS_STEP_DEBUG` 環境変数にtrueを設定することで、ステップのデバッグログを出力できる
- ランナー診断ログ
  - `ACTIONS_RUNNER_DEBUG` 環境変数にtrueを設定することで、ランナー診断ログを出力できる
    - ブラウザから直接は見れない

## ワークフローのデバッグログ

- `echo "::debug::hogehoge"` でデバッグログを出力できる
- Bash tracingを使うのも良い
- ログをグループ化できる

```yml
::group::<group-name>
# echoとか使ってログを出力する
::endgroup::
```
