# 講師向け: 公開・権限の設定

この教材は `RM0428MR/git-conflict-practice` に公開済みです。
更新版ではmainとtraining-startタグを使います。研修用PRは研修生自身が作ります。

## 研修前の準備

- GitHubのSettings → Collaboratorsから研修生を招待し、書き込み権限を付けます。
- 研修生に招待を承認してもらいます。
- デフォルトブランチがmainであることを確認します。
- READMEのURLを渡します。

## 別の空リポジトリへ教材をコピーする場合

準備済みのローカルリポジトリから実行します。`YOUR_ACCOUNT` と `NEW_REPO` は実際の公開先へ置き換えます。

```bash
git push git@github.com:YOUR_ACCOUNT/NEW_REPO.git main refs/tags/training-start
```

READMEにあるクローン先・PR作成先のURLも、新しいリポジトリに合わせて案内してください。
mainに研修生の解答を取り込む前の状態でコピーします。

[講師向けの運営手順](INSTRUCTOR.md)も参照してください。
