# Claude Code ベストプラクティス

このドキュメントは「Claude Code フル自律運用ベストプラクティス」の要点をまとめたもの。
実装時に `@docs/best-practices.md` で参照する。

---

## 最大の失敗要因：コンテキスト汚染

コンテキストが汚染されると Claude の判断品質が下がる。防止策：

- 大きな変更前は `/clear` + 新セッション
- 脱線したら `Esc Esc` / `/rewind` で巻き戻し
- 同じコンテキストで修正を繰り返さない

---

## CLAUDE.md の鉄則

- 命令数は **150〜200 が上限**（増えると全体の遵守率が下がる）
- 「この行を削除しても Claude がミスするか？」→ No なら削除
- 書くべき内容：Claude が繰り返しミスしたことだけ

---

## コンテキスト管理

| 操作 | タイミング |
|---|---|
| `git commit` | タスク完了ごと（最低1時間に1回）|
| `/project:progress` | セッション終了前 |
| `/project:new-session` | セッション開始時 |
| `/clear` + 新セッション | 大きな変更の前 |
| `/compact` | 遅い（1分以上）ので多用しない |

---

## 実装フロー（プロダクションコード）

1. `/project:plan` で `docs/architecture.md` と実装プランを作成
2. フェーズごとに実装（unit → integration → e2e）
3. 別セッションで `/project:review`（スタッフエンジニア役）
4. タスク完了ごとに即コミット

---

## セキュリティ設定（settings.json）

```json
"deny": [
  "Read(.env*)",
  "Read(*secret*)",
  "Bash(rm -rf *)",
  "Bash(git push --force *)"
]
```

---

## カスタムコマンド一覧

| コマンド | 用途 |
|---|---|
| `/project:new-session` | セッション開始時のウォームアップ |
| `/project:plan` | 実装前プランニング |
| `/project:review` | コードレビュー（スタッフエンジニア視点）|
| `/project:progress` | セッション進捗を保存・引き継ぎ |

---

## 参考リポジトリ

- [everything-claude-code](https://github.com/affaan-m/everything-claude-code) — 28エージェント、116スキルの本番対応ハーネス
