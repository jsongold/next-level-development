---
name: plan
description: 実装前プランニング。architecture.md作成からチェックボックス付きタスクリスト生成まで。
allowed_tools: ["Read", "Write", "Bash", "Grep", "Glob"]
---

# /plan

実装を始める前に構造化された計画を立てる。

## Goal

「バイブコーディング」を防ぎ、品質の高い実装のための設計ドキュメントを作成する。

## Suggested Sequence

1. `@docs/architecture.md` を読んで現在のアーキテクチャを理解する
2. 実装対象の要件を整理する
3. `docs/architecture.md` を更新または新規作成する（設計決定を記録）
4. `[ ]` チェックボックス付きの実装タスクリストを生成する：
   - Phase 1: 単体テスト（unit tests）
   - Phase 2: 統合テスト（integration tests）
   - Phase 3: E2Eテスト
5. リスクと考慮事項を列挙する
6. 別セッションでレビューが必要な場合は `/review` を推奨する

## Notes

- 実装前に必ずこのコマンドを実行する
- 計画は `docs/architecture.md` に保存し、セッションを跨いで参照できるようにする
