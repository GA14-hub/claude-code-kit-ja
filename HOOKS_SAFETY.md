# Git Hooks 安全性ガイド

本ドキュメントは、本パックに含まれる Git Hooks の動作内容と安全性を説明するものです。チームへの導入時に、技術リーダーや管理者が内容を確認し、承認判断に使用することを想定しています。

---

## 実行されるコマンド一覧

| Hook 名 | 実行タイミング | 実行されるコマンド | 推定実行時間 |
|---------|--------------|------------------|-------------|
| `pre-commit` | `git commit` 実行時 | ESLint / Prettier / TypeScript tsc（Node.js の場合） | 5〜15 秒 |
| | | ruff check / ruff format / mypy（Python の場合） | 3〜10 秒 |
| | | gofmt / go vet（Go の場合） | 2〜5 秒 |
| `pre-push` | `git push` 実行時 | シークレットスキャン（grep による文字列検索） | 1〜3 秒 |
| | | npm test / pytest / go test（テスト実行） | プロジェクト依存 |
| `commit-msg` | `git commit` 実行時 | コミットメッセージの正規表現チェック（grep のみ） | 1 秒未満 |

**補足**: 各 Hook は対応するツールがインストールされている場合のみ実行します。ツールが見つからない場合は何もせず成功終了します（`exit 0`）。

---

## ネットワークアクセス: なし

全ての Hook スクリプトはネットワークアクセスを一切行いません。

- `npm install`、`pip install`、`go get` などのパッケージ取得は行いません
- 外部 API への通信は行いません
- テレメトリやデータ送信は行いません
- 実行されるコマンドは全てローカルにインストール済みのツールのみです

---

## 無効化方法

### 方法 1: 全 Hook を一括スキップ（一時的）

```bash
SKIP_HOOKS=1 git commit -m "message"
SKIP_HOOKS=1 git push
```

### 方法 2: 個別 Hook をスキップ（一時的）

```bash
SKIP_PRE_COMMIT=1 git commit -m "message"
SKIP_PRE_PUSH=1 git push
SKIP_COMMIT_MSG=1 git commit -m "message"
```

### 方法 3: 特定の Hook を無効化（恒久的）

```bash
# 実行権限を外す
chmod -x .git/hooks/pre-commit

# または削除する
rm .git/hooks/pre-commit
```

### 方法 4: 全 Hook をアンインストール

```bash
rm .git/hooks/pre-commit .git/hooks/pre-push .git/hooks/commit-msg
```

### 方法 5: Git の --no-verify オプション

```bash
git commit --no-verify -m "message"
git push --no-verify
```

---

## 監査方法

各スクリプトは以下の方針で設計されており、内容を容易に監査できます。

| 監査観点 | 設計方針 |
|---------|---------|
| **コード量** | 各スクリプトは 100 行前後。5 分以内に全文を読める |
| **依存関係** | bash 標準コマンド（`grep`、`echo`、`exit`）のみ使用。外部ツールの呼び出しは `command -v` で存在確認してから実行 |
| **副作用** | ファイルの変更・削除は一切行わない。読み取りと検査のみ |
| **外部通信** | ネットワークアクセスは一切なし（`curl`、`wget`、`npm install` 等を使用しない） |
| **ブロック挙動** | `commit-msg` は非準拠でも警告のみ（`exit 0`）。`pre-commit` と `pre-push` はチェック失敗時にブロックするが、環境変数で即座にスキップ可能 |
| **エラー処理** | ツールが見つからない場合は何もせず成功終了。プロジェクト種別が不一致の場合もブロックしない |

### 監査手順

```bash
# 1. スクリプトの内容を確認
cat .git/hooks/pre-commit
cat .git/hooks/pre-push
cat .git/hooks/commit-msg

# 2. 実行されるコマンドだけを抽出して確認
grep -E '(npx|npm|pytest|python|go |ruff|flake8|mypy|gofmt|grep)' .git/hooks/*

# 3. ネットワーク関連のコマンドがないことを確認
grep -E '(curl|wget|fetch|http|https|npm install|pip install|go get)' .git/hooks/*
# → 結果が空であることを確認
```

---

## FAQ

**Q: CI/CD の代わりになりますか？**
A: いいえ。Hooks はローカルの軽量チェックで、CI/CD を補完するものです。本格的なテストやデプロイは CI/CD で行ってください。

**Q: 他のメンバーのマシンでも動きますか？**
A: Hooks はリポジトリの `.git/hooks/` にコピーする必要があります。`git config core.hooksPath` を使えばチーム共有も可能です。

**Q: Windows でも動きますか？**
A: Git Bash がインストールされていれば動作します。Git for Windows に Git Bash は同梱されています。

---

v1.0.0 | 2026-02-14
