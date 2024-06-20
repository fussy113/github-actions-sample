# ワークフロー構文

## コンテキスト(Contexts)

実行時の情報やジョブの実行結果を保持するオブジェクト

### [github コンテキスト](https://docs.github.com/ja/actions/learn-github-actions/contexts#github-context)

ワークフロー実行時の情報、トリガーになったイベントの情報を保持

- 基本的には文字列型のプロパティ
- `github.event`のみオブジェクト型

## 環境変数(Environment variables)

- ワークフロー、ジョブ、ステップの各レベルで定義できる
  - 定義場所によってスコープが異なる
  - オーバーライドできる
    - スコープが狭い方が優先される

### デフォルト環境変数

- github コンテキストと、runner コンテキストのプロパティがそのまま定義されている

### 中間環境変数

- コンテキストを直接シェルコマンドに埋め込むことができる
  - `${{ github.repository }}`
  - `${{ github.event_name }}`
  - これは**アンチパターン**
    - 特殊文字が含まれる場合があるため
  - 環境変数経由で渡すことが推奨される

## Variables

- GitHubのリポジトリの設定で登録することで、複数のワークフローで同じ値を使い回せる
- `vars.<変数名>`で参照できる
- gh コマンドでも設定できる

```shell
gh variable set <変数名> --body <値>
```

## Secrets

機密情報を保持するための仕組み

- 暗号化され、安全に管理される
- GitHub内で安全に管理される
- 登録した後に値は全く確認できなくなる
- gh コマンドでも設定できる

```shell
gh secret set <シークレット名> --body <値>
```

## 式で利用できる関数

- 文字列の比較
- 文字列の生成
- JSONの操作
- ハッシュ生成

## ifによる条件分岐

- ステップやJobの条件分岐ができる

## ステータスチェック関数

- `success()`
- `failure()`
- `cancelled()`
- `always()`

## ステップ間のデータ共有

### GITHUB_OUTPUTによる共有

```yaml
  # 設定
  - id: <step-id>
    run: echo "<キー名>=<値>" >> "${GITHUB_OUTPUT}"
  # 参照
  - run: echo "${{ steps.<step-id>.outputs.<キー名> }}"
```

### GITHUB_ENVによる共有

```yaml
# 設定
run: echo "<キー名>=<値>" >> "${GITHUB_ENV}"
```

グローバル変数として定義する

### GitHub APIの実行

GitHub CLIを利用して、GitHub Action上からGitHub APIを実行できる

- GitHub APIの実行のためには、**GITHUB_TOKEN**が必要

```yml
${{ secrets.GITHUB_TOKEN }}
# または
${{ github.token }}
```

GITHUB_TOKENの権限は、パーミッションで制御する
