> **English**: This is a Japanese-only Claude Code skill kit.
> For English users, see [`README.en.md`](README.en.md).

# Claude Code 導入キット 日本語版

`.claude/` フォルダをコピーするだけで、Claude Code に日本語の開発ワークフローが追加されるキットです。

**v3.0.0 で全40スキル＋Git Hooks を無料化しました。**

> **このキットのスキルは手動呼び出し専用です。** Claude が自発的に提案することはありません。使いたいスキルは `/skill-name` で直接呼び出してください。

### 関連リンク

- [Claude Code の使い方・スキル解説（Zenn）](https://zenn.dev/ga14tools)
- [BOOTH 無料ダウンロード](https://ga14tools.booth.pm/items/7984292)
- [Zenn Book — Claude Code 実務ワークショップ（500円）](https://zenn.dev/ga14tools/books/claude-code-workshop)

---

## 3分クイックスタート

### 1. コピー

```bash
# macOS / Linux / Git Bash
cp -r .claude/ /path/to/your-project/.claude/
cp CLAUDE.md /path/to/your-project/CLAUDE.md
```

```powershell
# Windows (PowerShell)
Copy-Item -Recurse .claude\ \path\to\your-project\.claude\
Copy-Item CLAUDE.md \path\to\your-project\CLAUDE.md
```

### 2. CLAUDE.md を編集

`CLAUDE.md` を開いて、プロジェクト名・言語・テストコマンド等を記入してください。

### 3. 使ってみる

```bash
# Claude Code を起動して、スキルを呼び出す
/bug-triage "TypeError: Cannot read properties of undefined"
/pr-write
/security-quick src/
```

これだけで動きます。

---

## まずこの5つから

| スキル | やること | 使い方 |
|-------|---------|--------|
| `/bug-triage` | エラーから原因候補を出す | `/bug-triage エラーログ.txt` |
| `/test-add` | テストを追加する | `/test-add src/utils/validator.ts` |
| `/pr-write` | PR 説明文を生成する | `/pr-write` |
| `/security-quick` | セキュリティ簡易監査 | `/security-quick src/` |
| `/refactor-plan` | リファクタの計画を立てる | `/refactor-plan src/legacy/payment.js` |

詳しくは [.claude/skills/_starter/README.md](.claude/skills/_starter/README.md) を参照。

---

## 全40スキル早見表

### バグ調査（2個）

| スキル | 概要 |
|-------|------|
| `/bug-triage` | エラーログから原因候補と切り分け手順を作成 |
| `/bug-reproduce` | バグの最小再現手順を確立 |

### テスト（1個）

| スキル | 概要 |
|-------|------|
| `/test-add` | 既存パターンに合わせてユニットテストを追加 |

### PR・レビュー（3個）

| スキル | 概要 |
|-------|------|
| `/pr-write` | 変更差分から PR 説明文を生成 |
| `/pr-review` | PR の差分をレビューし指摘事項を出力 |
| `/pr-quality-gate` | PR 前の品質チェックを一括実行 |

### セキュリティ（2個）

| スキル | 概要 |
|-------|------|
| `/security-quick` | OWASP Top 10 観点の基本セキュリティ監査 |
| `/security-secrets` | 秘密情報（APIキー・トークン等）の漏洩検出 |

### リファクタ（1個）

| スキル | 概要 |
|-------|------|
| `/refactor-plan` | リファクタの計画書を作成（影響範囲・リスク・手順） |

### 障害対応（1個）

| スキル | 概要 |
|-------|------|
| `/incident-debug` | 本番障害の総合調査フロー（fork で分離実行） |

### API 設計・レビュー（7個）

| スキル | 概要 |
|-------|------|
| `/api-auth-review` | API 認証・認可の設計レビュー |
| `/api-client-sdk-notes` | SDK 利用者向けの注意事項・変更点メモを生成 |
| `/api-endpoint-design` | RESTful エンドポイントの設計レビュー |
| `/api-error-contract` | API エラーレスポンスの契約（フォーマット・コード体系）を策定 |
| `/api-openapi-diff` | OpenAPI スキーマの差分を検出し破壊的変更を警告 |
| `/api-pagination-standard` | ページネーション方式の標準化レビュー |
| `/api-versioning-plan` | API バージョニング戦略の策定 |

### CI/CD（5個）

| スキル | 概要 |
|-------|------|
| `/ci-coverage-gate` | カバレッジ閾値のゲート設計・設定レビュー |
| `/ci-flaky-triage` | 不安定テスト（Flaky Test）の原因調査と対策 |
| `/ci-test-matrix` | テストマトリクス（OS・言語バージョン等）の設計 |
| `/ci-workflow-add` | CI ワークフロー（GitHub Actions 等）の新規作成 |
| `/ci-workflow-fix` | CI ワークフローのエラー修正・最適化 |

### データベース（7個）

| スキル | 概要 |
|-------|------|
| `/db-backfill-plan` | データバックフィル（既存データの一括更新）計画を策定 |
| `/db-index-suggest` | クエリパターンに基づくインデックス追加を提案 |
| `/db-migration-draft` | マイグレーションファイルのドラフト作成 |
| `/db-migration-review` | マイグレーションの安全性レビュー（ロック・互換性・ロールバック） |
| `/db-query-review` | SQL/ORM クエリのパフォーマンス・安全性レビュー |
| `/db-schema-review` | データベーススキーマの設計レビュー |
| `/db-seed-data-plan` | 開発・テスト用シードデータの設計 |

### 運用・監視（3個）

| スキル | 概要 |
|-------|------|
| `/ops-alert-design` | アラートルールの設計（閾値・通知先・エスカレーション） |
| `/ops-log-sift` | ログから異常パターンを検出・分析 |
| `/ops-metric-plan` | メトリクス収集・ダッシュボード設計の計画策定 |

### フロントエンド（2個）

| スキル | 概要 |
|-------|------|
| `/fe-a11y-audit` | アクセシビリティ（WCAG）監査 |
| `/fe-performance-review` | フロントエンドパフォーマンスのレビュー（Core Web Vitals 等） |

### その他（6個）

| スキル | 概要 |
|-------|------|
| `/dependency-update-plan` | 依存パッケージの更新計画（リスク評価・優先順位付け） |
| `/deploy-script-review` | デプロイスクリプトのレビュー（安全性・冪等性） |
| `/postmortem-write` | インシデントのポストモーテム（振り返り文書）を作成 |
| `/quality-checklist-gen` | プロジェクト固有の品質チェックリストを生成 |
| `/release-tag-plan` | リリースタグ・バージョニングの運用計画を策定 |
| `/team-adoption-plan` | チームへのツール・プラクティス導入計画を策定 |

---

## Git Hooks（3個）

`hooks/` ディレクトリに、すぐ使える Git Hooks を同梱しています。

| Hook | 概要 |
|------|------|
| `pre-commit` | コミット前に lint・format・型チェックを自動実行（Node.js / Python / Go 対応） |
| `pre-push` | プッシュ前にシークレットスキャン＋テストを実行 |
| `commit-msg` | コミットメッセージが Conventional Commits 形式かチェック（警告のみ） |

### Hooks の導入方法

```bash
# プロジェクトの .git/hooks/ にコピー
cp hooks/* /path/to/your-project/.git/hooks/
chmod +x /path/to/your-project/.git/hooks/*
```

```powershell
# Windows (PowerShell) — chmod は不要（Git Bash がシェバンを認識）
Copy-Item hooks\* \path\to\your-project\.git\hooks\
```

**安全に使うための注意事項は [HOOKS_SAFETY.md](HOOKS_SAFETY.md) を必ずお読みください。**

---

## 困ったらこれフローチャート

```
バグが出た → /bug-triage → /bug-reproduce → 修正 → /test-add

PR を出したい → /pr-quality-gate → /pr-write

レビューを頼まれた → /pr-review

セキュリティが心配 → /security-quick → /security-secrets

リファクタしたい → /refactor-plan → 実行 → /test-add

本番障害が起きた → /incident-debug → /postmortem-write

API を設計したい → /api-endpoint-design → /api-auth-review → /api-error-contract

DB を変更したい → /db-schema-review → /db-migration-draft → /db-migration-review

CI を整備したい → /ci-workflow-add → /ci-test-matrix → /ci-coverage-gate

リリースしたい → /release-tag-plan → /deploy-script-review
```

---

## 安全設計

### permissions.deny（第一防御線）

`settings.json` に設定済み。Claude Code が `.env` や `secrets/` を読み取ることを禁止します。

```json
{
  "permissions": {
    "deny": [
      "Read(./.env)", "Read(**/.env)", "Read(**/.env.*)",
      "Read(./secrets/**)", "Read(**/secrets/**)",
      "Edit(./.env)", "Edit(**/.env)", "Edit(**/.env.*)",
      "Edit(./secrets/**)", "Edit(**/secrets/**)"
    ]
  }
}
```

### rules（行動ルール）

| ルール | 内容 |
|-------|------|
| security.md | 秘密情報を読まない・貼らない・生成物に含めない |
| git-workflow.md | feature branch 必須、force push 禁止 |
| coding-style.md | 既存パターンに従う、命名規則を守る |

---

## カスタマイズ

### CLAUDE.md の編集

`CLAUDE.md` はプロジェクトの説明書です。言語、フレームワーク、テストコマンド等を記入すると、全スキルの出力品質が向上します。

### rules の編集

`.claude/rules/` 内のファイルを編集して、チームのルールに合わせてください。

### settings.json の編集

`permissions.deny` に追加のパターンを加えることで、保護対象を拡張できます。

---

## 互換性情報

- **対象**: Claude Code (CLI)
- **動作確認**: 2026年2月時点
- **必要なもの**: Claude Code がインストールされた環境

---

## FAQ

### スキルを呼び出しても反応しない

`.claude/skills/` フォルダがプロジェクトルートに正しくコピーされているか確認してください。

### 権限の確認で止まる

`allowed-tools` が設定されていないスキル（test-add、refactor-plan 等）は、ファイル編集時に権限確認が表示されます。これは正常な動作です。「許可」を選んでください。

### 出力が英語になる

SKILL.md の指示は日本語で書かれていますが、Claude が英語で回答する場合は、プロンプトに「日本語で回答してください」と追記してください。

### settings.json の deny が効かない

Claude Code の permissions.deny には既知の不安定な動作が報告されています。deny はベストエフォートの防御として使い、秘密情報は `.gitignore` で管理し、環境変数で扱うことを推奨します。

### hooks がうまく動かない

[HOOKS_SAFETY.md](HOOKS_SAFETY.md) の「トラブルシューティング」セクションを確認してください。Windows 環境では `chmod +x` が不要な場合があります。

---

## ライセンス

[LICENSE.md](LICENSE.md) を参照してください。
