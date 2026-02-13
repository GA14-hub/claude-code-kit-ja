> **English**: This is a Japanese-only Claude Code skill kit.
> For English users, see `README.en.md` (TBD).
> EN version may be released after Phase 1.5 validation.

# Claude Code 導入キット 日本語版

`.claude/` フォルダをコピーするだけで、Claude Code に日本語の開発ワークフローが追加されるキットです。

> **このキットのスキルは手動呼び出し専用です。** Claude が自発的に提案することはありません。使いたいスキルは `/skill-name` で直接呼び出してください。

### リンク

- [記事一覧（Zenn / Qiita）][articles-url]
- [BOOTH（無料版 0 円）][booth-url]
- [X 固定ポスト][x-pinned-url]

[articles-url]: https://example.com/TODO
[booth-url]: https://example.com/TODO
[x-pinned-url]: https://example.com/TODO

---

## 3分クイックスタート

### 1. コピー

```bash
# kit の .claude/ フォルダをプロジェクトルートにコピー
cp -r .claude/ /path/to/your-project/.claude/
cp CLAUDE.md /path/to/your-project/CLAUDE.md
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

## 全10スキル早見表

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

---

## 困ったらこれフローチャート

```
バグが出た → /bug-triage → /bug-reproduce → 修正 → /test-add

PR を出したい → /pr-quality-gate → /pr-write

レビューを頼まれた → /pr-review

セキュリティが心配 → /security-quick → /security-secrets

リファクタしたい → /refactor-plan → 実行 → /test-add

本番障害が起きた → /incident-debug
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

---

## ライセンス

[LICENSE.md](LICENSE.md) を参照してください。
