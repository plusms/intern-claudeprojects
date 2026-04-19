# CLAUDE.md — インターン向けClaude Code設定

## このリポジトリについて
プラス社SEOチームのインターン向けClaude Code環境。
社員と同じスキルを使って、記事改修・更新作業を担う。

---

## 担当できる作業

| コマンド | 内容 |
|---------|------|
| `/rank-local` | 地域記事の改修分析・方針案作成（PHASE1〜3）→ 引き継ぎシート出力 |
| `/knowhow-update` | ノウハウ記事の定期更新 |

---

## ファイル構成

```
knowledge/
  block-rules.md           ← ブロック別ライティングルール
  guidelines.md            ← SEO記事作成ガイドライン
  article-types/
    local.md               ← 地域記事の前提ルール（必読）
.claude/commands/
  rank-local.md            ← 地域記事改修フロー（インターン用・起動コマンド）
  knowhow-update.md        ← ノウハウ記事定期更新フロー
  skills/
    rank-sc-check.md       ← GSCクエリ分析スキル（PHASE1）
    rank-local-check.md    ← 地域やり切り診断スキル（PHASE2）
    rank-reform-design.md  ← 改修設計スキル（PHASE3）
handoffs/                  ← 引き継ぎシート格納先（自動生成・git pushで共有）
  [サイト名]/
    [スラッグ].md
```

---

## 行動原則

- 結論から出す
- 確認が必要な場合はその場で聞く。判断できないときは止まって確認する。勝手に進まない
- ユーザーへの質問は1回につき1つまで
- コピペできる形式を優先する
