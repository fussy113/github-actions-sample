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

- ログを手動でマスクできる

```yml
::add-mask::<secret-value>
```

## アノテーション

```yml
::error::<error-message>
::warning::<warning-message>
::notice::<notice-message>
```

## ジョブサマリー

マークダウン形式で出力できる

`GITHUB_STEP_SUMMARY` 環境変数に値を入れることで、表示される

```yml
echo "# MD形式の文章" >> "${GITHUB_STEP_SUMMARY}"
```
