# 地域記事改修フロー（インターン担当：PHASE1〜3 + 引き継ぎシート出力）

---

## このフローの全体像

インターンは **PHASE1〜3** を担当し、最後に引き継ぎシートを生成する。
PHASE4以降（HTMLエディット・WP実装）は社員が担当する。

```
PHASE1: rank-sc-check（GSCクエリ分析）
    ↓
PHASE2: rank-local-check（地域やり切り診断）
    ↓
PHASE3: rank-reform-design（改修方針案作成）
    ↓
PHASE4: 引き継ぎシート生成 → git push（社員へバトン）
```

---

## 起動方法

Claude Codeで `/rank-local` を起動し、以下を伝える。

```
対象サイト：[サイト名（フォルダ名）]
対象記事URL：[URL]
メインKW：[KW]
サブKW：[KW1]・[KW2]
GSCデータ：[コピペまたは添付]
記事HTML（または構成）：[コピペまたは添付]
```

以降はClaude Codeの指示に従って進める。

---

## PHASE1：GSCクエリ分析

**使用スキル：** `.claude/commands/skills/rank-sc-check.md`

実行前に読む：`rank-sc-check.md`

フローはrank-sc-checkに従う。STEP6のユーザー確認（FB）を受けてからPHASE2に進む。

**PHASE1完了の定義：**
- クエリ意図グループが分類されている
- 上位・0クリックKWの仮説が出ている
- 対応リスト（優先度付き）が出ている
- ユーザーがOKを出している

---

## PHASE2：地域やり切り診断

**使用スキル：** `.claude/commands/skills/rank-local-check.md`

実行前に読む：`rank-local-check.md`

フローはrank-local-checkに従う。
- STEP2（AIO・PAA・サジェスト）はユーザーに提供を依頼する
- STEP3（競合3記事）のURLはユーザーに提供を依頼する
- 最後のユーザー確認（FB）を受けてからPHASE3に進む

**PHASE2完了の定義：**
- 競合との地域差分サマリが出ている
- 6軸チェックが完了し、△・×に根拠が書かれている
- 対応リストが出ている
- 次ステップのルーティングが決まっている（rank-reform-design or rank-edit-html）
- ユーザーがOKを出している

---

## PHASE3：改修方針案作成

**使用スキル：** `.claude/commands/skills/rank-reform-design.md`

実行前に読む：`rank-reform-design.md`・`knowledge/block-rules.md`・`knowledge/article-types/local.md`

フローはrank-reform-designに従う。
構成案の確認をユーザーから取ってからPHASE4に進む。

**PHASE3完了の定義：**
- 改修後H2/H3構成が出ている
- 各ブロックに分類ラベル・方針・根拠が付いている
- So what確認が完了している
- ユーザーがOKを出している

---

## PHASE4：引き継ぎシート生成 → git push

PHASE1〜3の全アウトプットをまとめた引き継ぎシートを生成し、GitHubリポジトリにpushする。

### 引き継ぎシートの生成

以下のフォーマットでシートを生成する。

---

**ファイル名：** `handoffs/[サイトフォルダ名]/[記事スラッグ].md`
（例：`handoffs/chigasaki/houkyou-osaka.md`）

**記事スラッグ：** URLの末尾パス（例：`https://example.com/houkyou-osaka/` → `houkyou-osaka`）

---

```markdown
# 引き継ぎシート：[サイト名] / [記事スラッグ]

作成日：[YYYY-MM-DD]
担当インターン：[名前]（任意）

---

## 対象記事情報

| 項目 | 内容 |
|------|------|
| サイト | [サイト表示名]（[フォルダ名]） |
| URL | [記事URL] |
| メインKW | [KW] |
| サブKW | [KW1]・[KW2] |

---

## PHASE1：GSCクエリ分析の結果（rank-sc-check）

### クエリ意図グループ
[rank-sc-checkのSTEP2アウトプットをそのまま貼る]

### 上位・0クリックKW
[rank-sc-checkのSTEP3アウトプットをそのまま貼る]

### クエリ意図 × H2/H3 対応確認
[rank-sc-checkのSTEP4アウトプットをそのまま貼る]

### PHASE1対応リスト
[rank-sc-checkのSTEP5対応リストをそのまま貼る]

---

## PHASE2：地域やり切り診断の結果（rank-local-check）

### 競合との地域差分サマリ
[rank-local-checkのSTEP3サマリをそのまま貼る]

### 6軸チェック
[rank-local-checkのSTEP4チェック結果をそのまま貼る]

### PHASE2対応リスト
[rank-local-checkのSTEP5対応リストをそのまま貼る]

---

## PHASE3：改修方針案（rank-reform-design）

### 改修後タイトル案
[rank-reform-designのアウトプットから]

### H2/H3構成（改修後）
[rank-reform-designのH2/H3構成アウトプットをそのまま貼る]

### So what確認
[rank-reform-designのSo what確認アウトプットをそのまま貼る]

---

## 判断の根拠・意図

### なぜこの構成にしたか
[PHASE1〜3を通じた主要な判断ポイントを箇条書きで記載]
- 例：「クエリ意図グループ『〇〇』が表示回数最多かつ×判定のため、H2追加を優先した」
- 例：「競合上位3記事すべてが△△セクションを持ち、自社のみ欠落していたため追加」
- 例：「⑤来院ハードル情報が×のため、医療ジャンル観点でアクセス羅列→体制・費用透明性に差し替えを提案」

### 判断に迷ったポイント（社員に確認してほしいこと）
[自分の判断に自信がない部分・前提が不確かな部分を書く]
- 例：「△△H3は削除vs維持で迷った。現状順位を維持するための判断基準を確認してほしい」
- 例：「競合3記事中2記事が○○を入れているが、クライアントの実態情報が不明。追加可否の判断を頼みたい」

---

## 社員へのバトン

### 次のアクション
PHASE3の構成案に基づき、HTMLエディット（rank-edit-html）を実施してください。

### 使用スキル
`rank-edit-html`（社員環境の claude-projects/.claude/commands/skills/ に存在）

### 注意点
- PHASE3の構成案は確定案ではありません。社員側でFBを加えた上で最終確定してください
- 「判断に迷ったポイント」に記載した項目は必ず確認してから着手してください
- 引き継ぎシートの内容は `/rank-local` セッションの全アウトプットです。追加の分析なしにそのまま利用できます
```

---

### gitでpushする

引き継ぎシートの内容が確定したら、以下の手順でpushする。

```bash
# 1. ファイルを handoffs/[サイト名]/ に保存する（Claudeが自動実行）

# 2. git操作
cd /path/to/intern-claudeprojects
git add handoffs/[サイト名]/[スラッグ].md
git commit -m "add handoff: [サイト名]/[スラッグ]"
git push origin main
```

pushが完了したら、GitHubのURL（`https://github.com/plusms/intern-claudeprojects/blob/main/handoffs/[サイト名]/[スラッグ].md`）をユーザーに伝える。

---

## 完了報告フォーマット

```
✅ PHASE1〜3 完了・引き継ぎシート push済み

サイト：[サイト名]
記事：[URL]
引き継ぎシート：https://github.com/plusms/intern-claudeprojects/blob/main/handoffs/[サイト名]/[スラッグ].md

主要な改修方針：
- [一言サマリー1]
- [一言サマリー2]

社員確認事項：
- [判断に迷ったポイントの要約]
```
