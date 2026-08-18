# ローカルの変更をGitHubに反映する手順

ブログをローカル環境（MacBook Air）で編集した後、GitHubに反映するための標準手順です。

## 基本の3ステップ

```bash
git add .
git commit -m "変更内容がわかるメッセージ"
git push origin main
```

| コマンド | 役割 |
|---|---|
| `git add .` | 変更したファイルをすべてステージ（コミット対象）に追加する |
| `git commit -m "..."` | 変更内容を記録する（メッセージは自由に変更可） |
| `git push origin main` | GitHubへアップロードする |

## 詳細な手順

### 1. 作業ディレクトリに移動する

```bash
cd ~/Documents/malaoanania.github.io
```

（実際にリポジトリをcloneした場所に合わせてパスを変更）

### 2. 変更内容を確認する（任意）

どのファイルが変更されたか、pushする前に確認しておくと安心です。

```bash
git status
```

赤字で変更されたファイル一覧が表示されます。

### 3. 変更をステージに追加する

```bash
git add .
```

### 4. コミットする

```bash
git commit -m "デザインとフォントのカスタマイズ"
```

`-m` の後のメッセージは、何を変更したか分かるように自由に書き換えてください。

### 5. GitHubにpushする

```bash
git push origin main
```

### 6. 反映を確認する

以下の2箇所を確認してください。

- リポジトリのページ: `https://github.com/malaoanania/malaoanania.github.io`
- 公開サイト: `https://malaoanania.github.io/`（反映まで1〜2分かかることがあります）

## 補足

### `_config.yml` を変更した場合

ローカルでプレビューしているサーバー（`bundle exec jekyll serve`）は、`_config.yml` の変更を自動反映しません。以下の手順で再起動してから確認してください。

```bash
# Ctrl + C でサーバーを停止してから
bundle exec jekyll serve
```

### `_site` フォルダについて

`_site` フォルダはローカルでビルドした際に自動生成される一時ファイルです。GitHubにpushする必要はありません。`.gitignore` に含まれているか、以下のコマンドで確認できます。

```bash
cat .gitignore
```

含まれていない場合は、以下で追加しておくと安心です。

```bash
echo "_site" >> .gitignore
```

### pushが失敗した場合（認証エラー）

パスワード認証は廃止されているため、GitHubにログインする際は **Personal Access Token（個人アクセストークン）** を使用します。

1. GitHubの **Settings → Developer settings → Personal access tokens → Tokens (classic)** でトークンを発行
2. `push` 実行時、Usernameには GitHubのユーザー名、Passwordには発行したトークンを入力

毎回の入力を省略したい場合は、以下を設定しておくとMacのキーチェーンに保存されます。

```bash
git config --global credential.helper osxkeychain
```
