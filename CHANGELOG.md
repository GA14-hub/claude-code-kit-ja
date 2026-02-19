# 変更履歴

## v3.0.0 (2026-02-19)

### 全スキル無料化

有料版（Claude Code 実務スキルパック）の全スキルを本キットに統合し、無料化しました。

### 新機能
- 30スキル追加（API設計 7 / CI/CD 5 / DB 7 / 運用 3 / フロントエンド 2 / その他 6）
- Git Hooks 3本追加（pre-commit / pre-push / commit-msg）
- HOOKS_SAFETY.md（Hooks の安全利用ガイド）を追加

### v2 からの変更点
- 全40スキル体制（10 → 40）
- 有料版・無料版の区別を廃止
- README を全面改訂（40スキル対応・Hooks セクション追加）

---

## v2.0.0 (2026-02-13)

### 新機能
- Claude Code skills 形式に全面移行（v1 のプロンプト集から進化）
- 10 skills（バグ調査・テスト・PR・セキュリティ・リファクタ・障害対応）
- permissions.deny による秘密情報保護
- rules 3本（セキュリティ・Git ワークフロー・コーディングスタイル）
- 3分クイックスタート README

### v1 からの変更点
- マークダウン手順書 → `.claude/skills/` のネイティブ skill 形式に変更
- コピペ運用 → `/skill-name` でワンコマンド実行に変更
- settings.json による権限管理を追加
