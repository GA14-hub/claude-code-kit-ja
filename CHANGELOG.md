# 変更履歴

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
