# プルリクエスト（PR）作成

プルリクエストを作成する手順です。

## 前提条件

- GitHub CLI (`gh`) がインストールされていること
- 変更がコミット・プッシュされていること
- 作業ブランチが作成されていること

## 手順

### 1. 差分確認


**ベースブランチ名・レビュアーを変数に格納（PowerShell/JSON方式）:**
```powershell
$settings = Get-Content .github/skills/git-skill/reference/pr-settings.json | ConvertFrom-Json
$BASE_BRANCH = $settings.base
$REVIEWERS = $settings.reviewers -join ','
```

**現在のブランチを確認:**
```powershell
git branch
```

**ベースブランチとの差分を確認:**
```powershell
git diff $BASE_BRANCH...HEAD
```

**コミット履歴を確認:**
```powershell
git log $BASE_BRANCH..HEAD
```

### 2. PR作成（設定ファイルを参照して自動化）

コマンド：
```powershell
gh pr create --title "タイトル" --body "本文" \
  --base $BASE_BRANCH \
  --reviewer $REVIEWERS
```
※ --baseや--reviewerはpr-settings.jsonの内容が使われます。

## PR本文 必須情報
- 概要（何を変更したか）

## よく使う管理コマンド
```powershell
gh pr list                # PR一覧
gh pr view <番号>         # PR詳細
gh pr view --web          # ブラウザで開く
gh pr status              # ステータス
gh pr comment <番号> --body "コメント"
gh pr merge <番号>        # マージ
```
