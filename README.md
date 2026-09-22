# daily-auto-commit-app

GitHub Actions で `data/log.txt` にタイムスタンプを1行追記してコミット・push するだけのリポジトリです。
GitHub の Contribution Graph(草)を生やすことだけが目的で、コミット内容そのものに意味はありません。

- ワークフロー: [.github/workflows/daily-commit.yml](.github/workflows/daily-commit.yml)
- 手動実行: GitHub の Actions タブ → `Daily Auto Commit` → `Run workflow`(常にコミットされます)

## 現在の運用モード

**Public リポジトリ + 毎日1回コミット**

- ワークフロー上部の `env.COMMIT_MODE: daily`
- 5つの起動タイミング(JST 09:00 / 12:00 / 15:00 / 18:00 / 21:00)のうち、
  `DAILY_RUN_HOUR_UTC`(UTC 12:00 = JST 21:00)の回だけが実際にコミットします。
- Public なので Contribution Graph には無条件で反映されます。

## 将来の切り替え: Private + ランダムコミット

以下の2箇所を変更するだけで切り替えられます。

1. **[.github/workflows/daily-commit.yml](.github/workflows/daily-commit.yml) の `env` を書き換える**
   ```yaml
   env:
     COMMIT_MODE: random
     RANDOM_COMMIT_PROBABILITY: 40 # 1回の起動あたりのコミット確率(%)。お好みで調整
   ```
   random モードでは、5つの起動タイミングそれぞれで確率抽選が行われ、
   日によってコミット回数・時間帯が変わるようになります。

2. **GitHub 側でリポジトリを Private に変更**
   `Settings > General > Danger Zone > Change repository visibility`

3. **GitHub 個人設定で Private contributions を表示対象にする**
   `Settings(個人) > Profile > Contributions and activity` の
   **「Include private contributions on my profile」を ON** にする。
   これを ON にしないと、Private リポジトリのコミットは Contribution Graph に反映されません。

## 草が生える条件のメモ

- コミットが **デフォルトブランチ**(このリポジトリでは `main`)に存在すること
- コミットの author/committer メールアドレスが、その GitHub アカウントに紐づいていること
  → 本ワークフローでは `BonchaN66@users.noreply.github.com`(GitHub 標準の noreply アドレス)を使用。
    追加のメール認証なしに自動的にアカウントへ紐づくため安全。
- リポジトリが **フォークでない** こと
- Public なら常にカウント。Private の場合は上記「Include private contributions」設定が ON であること
