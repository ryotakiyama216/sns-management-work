# 01. 記録プロンプト

## 役割
実際に投稿した（または見送った）内容を、該当プラットフォームの `data/posts/<platform>/` に記録する。

## 対象
X / Threads / Instagram / TikTok（noteは別管理のため対象外）

## 手順
1. 対象プラットフォームの `data/posts/<platform>/index.json` を読み、`files` 配列から最新ファイルを特定する（`files` が空の場合は連番001のファイルを対象とする）。
2. 最新ファイルを開き、`file_info.count` と実際の行数を確認する。
   - `count` が300行（300件が目安ではなく300行の意）を超えている場合、または超えそうな場合は新しいファイルを作成する。
     - ファイル名は `プラットフォーム_年_連番.json`（例：`x_2026_002.json`）。連番は既存最大値+1。
     - 年が変わっていた場合は連番を001にリセットする（例：`x_2027_001.json`）。
     - 新規ファイルの `file_info` を設定してから投稿を追記する。
3. 記録先ファイルの `posts` 配列に、以下のスキーマで投稿オブジェクトを追記する。

```json
{
  "id": "20260811-001",
  "date": "YYYY-MM-DD",
  "theme": "投稿のテーマ",
  "text": "投稿本文",
  "type": "気づき型 | リアル日常型 | 問いかけ型",
  "hook": "フックの構造メモ",
  "status": "投稿済み | 未投稿 | 見送り",
  "reaction": {
    "likes": 0,
    "reposts": 0,
    "replies": 0,
    "bookmarks": 0
  },
  "rating": "良かった | 普通 | 微妙",
  "memo": "振り返りメモ"
}
```

- `id` は `YYYYMMDD-連番`（同日複数投稿の場合は連番を増やす）。
- 投稿直後は `reaction` を全て0、`rating` は空文字でよい。一定期間後に本プロンプトを再実行し、該当 `id` のレコードを実績値で上書き更新する。
- `type` はプラットフォームの `skills/<platform>.md` に定義された型から選ぶ。

4. 記録先ファイルの `file_info.count` / `from` / `to` を更新する。
5. `data/posts/<platform>/index.json` を更新する。
   - `files` に対象ファイル名が含まれていなければ追加する。
   - `total_posts` を再集計する。
   - `overall_summary`（`best_theme` / `best_type` / `avg_likes` / `avg_replies` / `avg_bookmarks` / `top_patterns`）を、`rating`が「良かった」の投稿を中心に再集計する。
   - `last_updated` を実行日に更新する。

## 注意
- 生データファイルを毎回全部読み直す必要はない。まず `index.json` を読み、対象ファイルのみ開く。
- 見送った投稿も `status: "見送り"` として記録し、なぜ見送ったかを `memo` に残す（次回のテーマ選定に活用するため）。
