# 講師向け: GitHubへの登録

ローカルリポジトリと練習用ブランチは作成済みです。
GitHubへの登録・pushは講師が実施してください。ZIPやブラウザのファイルアップロードでは、必要なブランチ履歴を移せません。

## 1. 空のリポジトリを作る

GitHubのNew repositoryから `git-conflict-practice` を作成します。
公開範囲は任意です。README・.gitignore・Licenseの追加は選択せず、空の状態で作成してください。

## 2. ログインして3ブランチを送る

以下はこの教材を作成したMacでのコマンドです。
`YOUR_ACCOUNT` は登録先のユーザー名またはOrganization名に置き換えます。

```bash
cd /Users/mr/ghq/github.com/RM0428MR/git-conflict-practice

gh auth login
gh auth setup-git

git remote add origin https://github.com/YOUR_ACCOUNT/git-conflict-practice.git
git push -u origin main
git push -u origin practice/early-opening practice/late-closing
```

`gh auth login` はGitHub.com・HTTPSを選んで進めます。
すでにログイン済みの場合は `gh auth status` で確認できます。
`origin already exists` が出たら `git remote -v` で接続先を確認してください。
この手順の再実行時は、接続先が正しければ `remote add` を省略できます。

## 3. 権限と準備

- デフォルトブランチが `main` になっていることを確認します。
- リポジトリのSettings → Collaborators（Organizationでは相当するアクセス管理）から研修生を招待し、書き込み権限を付けます。
- 招待承認後、[INSTRUCTOR.md](INSTRUCTOR.md) の順番で2つのPRを作成します。

複数人が各自取り組む場合は、講師が研修生ごとに別の空リポジトリを作成してください。
次のコマンドで、同じ初期状態の3ブランチを別リポジトリへ送れます。
`TRAINEE_REPO` を実際のリポジトリ名に置き換えてください。

```bash
git push https://github.com/YOUR_ACCOUNT/TRAINEE_REPO.git main practice/early-opening practice/late-closing
```

その後、各リポジトリで招待・PR準備を行います。

参考: [GitHub公式: ローカルコードの追加](https://docs.github.com/en/migrations/importing-source-code/using-the-command-line-to-import-source-code/adding-locally-hosted-code-to-github)
