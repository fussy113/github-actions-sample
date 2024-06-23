# 継続的インテグレーションの実践

## 自動テスト

- GitHub Actionsを使った自動テストを行おう
  - 各言語のsetupのためのアクションが提供されている
  - 特定ディレクトリ、ファイルが変更された場合に実行するように設定できる

## actionlint

- GitHub ActionsのYAMLファイルの構文チェックを行うツール
  - [actionlint](https://hub.docker.com/r/rhysd/actionlint)

```shell
docker run --rm -v "$(pwd):$(pwd)" -w "$(pwd)" rhysd/actionlint:latest
```

## ステップで実行されるシェル

- ubuntuの場合、デフォルトはBash
  - `shell: bash`などで、明示的に書くことができる
    - その場合、パイプ処理中のエラーを拾えるようになる(デバッグに便利)
- ワークフローのトップレベルで全ステップに適応されるシェルを変更できる

## Concurrency

同じワークフローが同時に実行されることを制御する

- 2つ目のワークフローの実行を待機する
- 1つ目のワークフローをキャンセルし、2つ目のワークフローを実行する
  - `cancel-in-progress`オプションを使う

## 継続的インテグレーションの黄金律

- クリーンに保つ
- 高速に実行する
- ノイズを減らす
  - シグナルとノイズを区別する

