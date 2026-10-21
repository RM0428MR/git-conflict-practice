# Git・GitHub コンフリクト解消研修 ☕

自分のPCで「クローン → 編集 → コミット → プッシュ → PR作成 → コンフリクト解消」を体験します。目安は20〜30分です。

## 始める前に

- Git、エディター（VS Codeなど）、GitHubアカウントを用意します。
- リポジトリへの招待を受け、承認します。書き込み権限が必要です。
- HTTPSでクローンします。プッシュにはGitHubへの認証が必要です。
- すでにHTTPSでプッシュできる人は、その認証設定を使ってください。
- 未設定なら、GitHub CLI（`gh`）をインストールし、次を実行します。

  ```bash
  gh auth login
  gh auth setup-git
  ```

  `GitHub.com` → `HTTPS` → ブラウザでのログインを選び、表示に従って認証します。
  `gh` が見つからない場合は講師に準備を依頼してください。
  参考: [GitHub公式のHTTPS認証手順](https://docs.github.com/en/get-started/git-basics/caching-your-github-credentials-in-git)
- `taro` は例です。ブランチ名は自分の名前に置き換えます。

## 今回の仕事

カフェの閉店を18時から20時に延ばしてください。
研修開始地点の営業時間は10:00〜18:00ですが、その後mainでは別の担当者が開店を9時に早めました。
まず閉店時刻の変更をPRにし、その後、先に進んだmainと内容を合わせます。

## 1. クローンする

作業したいフォルダでターミナルを開き、実行します。

```bash
git clone https://github.com/RM0428MR/git-conflict-practice.git
cd git-conflict-practice
```

## 2. 研修開始地点から自分のブランチを作る

```bash
git switch -c practice/taro training-start-https
```

`training-start-https` はmainの開店時刻が変わる前の状態に付けたタグです。
**今回はmainからではなく、このタグから始めてください。** ここが競合を体験するためのポイントです。

## 3. ファイルを編集する

エディターで `cafe.md` を開き、営業時間の1行だけを変更します。

```text
変更前: 営業時間: 10:00〜18:00
変更後: 営業時間: 10:00〜20:00
```

保存してから、変更を確認します。

```bash
git diff
```

## 4. コミットしてプッシュする

```bash
git add cafe.md
git commit -m "docs: Extend cafe closing time"
git push -u origin practice/taro
```

コミット時に名前・メールが未設定と出た場合は、次を自分の情報に置き換えて設定し、コミットを再実行します。
GitHubの非公開メールアドレス（noreply）も使えます。

```bash
git config user.name "自分の名前"
git config user.email "自分のメールアドレス"
```

## 5. 自分でPRを作る

[GitHubリポジトリ](https://github.com/RM0428MR/git-conflict-practice)を開きます。

1. **Pull requests → New pull request** を押します。
2. **base: main / compare: practice/taro** を選びます。
3. **Create pull request** を押します。自動マージできない表示が出ても、PRは作成できます。
4. タイトルを「閉店時刻を20時に変更」、本文に変更理由を書いてPRを作成します。
5. PRにコンフリクトが表示されることを確認します。

ここではまだマージしません。

## 6. PCでコンフリクトを解消する

作業ブランチのまま、mainの最新情報を取得して取り込みます。

```bash
git branch --show-current
git fetch origin
git merge --no-edit origin/main
```

最初のコマンドで自分のブランチ名が出ることを確認してください。
`CONFLICT` と表示され、処理が止まるのが正常です。

`cafe.md` を開くと、次のように2つの変更が表示されます。

```text
<<<<<<< HEAD
営業時間: 10:00〜20:00
=======
営業時間: 09:00〜18:00
>>>>>>> origin/main
```

上側は自分の変更、下側はmainの変更です。
**「開店を9時に早める」「閉店を20時に延ばす」の両方を満たす1行**に編集してください。
記号3行と不要な営業時間の行を消し、保存します。定休日やメニューは変更しません。

```bash
git diff
git add cafe.md
git commit -m "fix: Resolve cafe hours conflict"
git push
```

やり直したい場合は、解消のコミット前でマージ処理中なら `git merge --abort` でマージ開始前の状態に戻せます。

## 7. PRで解消を確認する

1. 作成したPRを再読み込みします。新しいPRを作る必要はありません。
2. コンフリクトの表示が消えていることを確認します。
3. Files changedで、mainに対して閉店時刻の変更だけが残っていることを確認します。
4. 講師にレビューを依頼します。**マージは講師の指示を待ってください。**

## 完了チェック

- [ ] 自分のブランチで編集・コミット・プッシュした
- [ ] 自分でPRを作った
- [ ] 競合した2つの変更を読み比べた
- [ ] 両方の依頼を残して解消し、同じPRへ反映した
- [ ] 営業時間は1行で、競合の記号が残っていない
- [ ] なぜ競合したのか説明できる

講師用: [準備・解答例](INSTRUCTOR.md) / [公開・権限の設定](GITHUB_SETUP.md)
