# daily-auto-commit-app

GitHub Actions で毎日 21:00 (JST) に `data/log.txt` へタイムスタンプを1行追記してコミット・pushするだけのリポジトリです。

- ワークフロー: [.github/workflows/daily-commit.yml](.github/workflows/daily-commit.yml)
- 手動実行: GitHub の Actions タブ → `Daily Auto Commit` → `Run workflow`

## GitHub のプロフィールに反映させるための注意

- このリポジトリを **Private** のまま使う場合、GitHub の
  `Settings > Profile > Contributions and activity` にある
  **「Include private contributions on my profile」** を ON にしてください。
  OFF のままだと緑のマスは表示されません。
- コミットの author/committer は `BonchaN66@users.noreply.github.com` を使用しています。
  この noreply アドレスは GitHub アカウントに自動的に紐づくため、追加のメール認証は不要です。
