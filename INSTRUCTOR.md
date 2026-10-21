# 講師向け: 準備と解答例

## 構成

- main: 営業時間は10:00〜18:00
- practice/early-opening: 同じ行を09:00〜18:00に変更
- practice/late-closing: 同じ行を10:00〜20:00に変更

両ブランチは同じ初期コミットから分岐しています。
ローカルのmainには、どちらもまだマージしていません。

## GitHubでの準備（5分程度）

[登録手順](GITHUB_SETUP.md) で3ブランチをpushした後に行います。

1. Pull requests → New pull requestで **base: main / compare: practice/early-opening** を選びます。
   - タイトル: `開店を9時に早める`
   - 本文: `朝のお客様向けに開店時刻を9時へ変更します。閉店時刻は維持します。`
2. 同じ方法で **base: main / compare: practice/late-closing** のPRを作成します。
   - タイトル: `閉店を20時に延ばす`
   - 本文: `仕事帰りのお客様向けに閉店時刻を20時へ変更します。先にマージされた開店時刻の変更も維持してください。`
3. **開店のPRだけを先にマージします。**
4. 閉店のPRを再読み込みして、コンフリクトが表示されることを確認します。
5. 研修生にREADMEと閉店のPRのURLを渡します。

2つとも先にマージしようとせず、閉店のPRを練習用に残してください。
教材用リポジトリのルールで直接マージできない場合は、講師が必要な承認を行ってください。

## 解答例

最終的なcafe.mdの営業時間は次の1行です。

```text
営業時間: 09:00〜20:00
```

- 開店を早める意図と、閉店を遅くする意図の両方を反映します。
- 定休日とメニューはそのままです。
- 片方を丸ごと採用するだけでは片方の依頼が失われます。

## 採点の目安

- 競合した理由を「同じ元の行を別々に変更したため」と説明できる
- 2つの変更意図を確認し、正しい1行にまとめられる
- 記号を消すだけではなく、内容が正しいことを確認できる
- 解消結果のコミット後、PRのマージまで確認できる

## ブラウザで解消できない場合のローカル手順

Gitが使える環境で、書き込み権限のある研修生が実施します。
`YOUR_ACCOUNT` は登録先に置き換えます。

```bash
git clone https://github.com/YOUR_ACCOUNT/git-conflict-practice.git
cd git-conflict-practice
git switch practice/late-closing
git fetch origin
git merge origin/main
```

ここで競合が発生するのが正常です。
cafe.mdを解答例に合わせて編集してから、次を実行します。
コミット時に名前とメールが未設定と出る場合は、自分の情報をこのリポジトリに設定します。

```bash
git diff
git add cafe.md
git commit -m "fix: Resolve cafe hours conflict"
git push
```

GitHubでPRの差分を確認してからマージします。
途中でやり直すときは、マージ処理中に `git merge --abort` でマージ開始前へ戻せます。

## 再度練習するとき

講師のローカルの3ブランチは元の状態で残っています。
別の空のGitHubリポジトリへ3ブランチをpushすると、同じ練習を繰り返せます。
登録手順の「複数人が各自取り組む場合」を参照してください。

参考: [GitHub公式: ブラウザでのコンフリクト解消](https://docs.github.com/en/pull-requests/how-tos/merge-and-close-pull-requests/resolving-a-merge-conflict-on-github)
