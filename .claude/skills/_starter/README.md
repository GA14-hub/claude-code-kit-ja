# まずこの5つから始めよう

30個のスキルに圧倒される必要はありません。まずは以下の5つだけ覚えれば、日常の開発作業がすぐに変わります。

## 1. `/bug-triage` — バグが出たらまずこれ

エラーログやエラーメッセージを渡すと、原因候補と切り分け手順を作ってくれます。

```
/bug-triage エラーログ.txt
/bug-triage "TypeError: Cannot read properties of undefined"
```

## 2. `/test-add` — テストを追加したい時

ファイルや関数を指定すると、既存のテストパターンに合わせてユニットテストを追加します。

```
/test-add src/utils/validator.ts
/test-add UserService 境界値テスト重視
```

## 3. `/pr-write` — PR を出す前に

現在の変更差分から PR 説明文とレビューチェックリストを自動生成します。

```
/pr-write
/pr-write ユーザー認証機能の追加
```

## 4. `/security-quick` — セキュリティが気になったら

OWASP Top 10 の観点でコードベースを簡易監査します。

```
/security-quick src/
/security-quick app/controllers/ インジェクション重視
```

## 5. `/refactor-plan` — リファクタする前に

いきなりコードを触らず、影響範囲とリスクを整理した計画書を先に作ります。

```
/refactor-plan src/legacy/payment.js
/refactor-plan UserModel 責務分離
```

---

## 困ったらこのフローチャート

```
バグが出た
  → /bug-triage でトリアージ
  → /bug-reproduce で再現手順を確立
  → 修正後 /test-add でテスト追加

PR を出したい
  → /pr-quality-gate で品質チェック
  → /pr-write で説明文生成

コードが気になる
  → /security-quick でセキュリティ確認
  → /refactor-plan で計画を立ててから着手
```

## 全スキル一覧

すべてのスキルの詳細は [README.md](../../README.md) の「全スキル早見表」を参照してください。
