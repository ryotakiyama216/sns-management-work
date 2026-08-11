# 03. 分析プロンプト

## 役割
自分の投稿実績（`data/posts/`）と収集したバズ投稿（`data/buzz/`）を突き合わせ、良かったパターン・悪かったパターンを抽出し、次回投稿の方針（`todays_policy`）を作る。

## 手順
1. 各プラットフォームの `data/posts/<platform>/index.json` の `overall_summary` を読む（生データの全件読みはしない）。
2. `data/buzz/index.json` の `overall_patterns` を読む。
3. 必要に応じて、`rating` が「良かった」「微妙」の投稿だけを対象ファイルから抽出し、詳細を確認する。
4. 以下の観点でまとめる。
   - `good_patterns`：自分の投稿で反応が良かったテーマ・型・フックの共通点
   - `bad_patterns`：反応が薄かった・NGパターンに触れてしまった投稿の共通点
   - `buzz_patterns`：`data/buzz/` から見えた、今の自分に取り入れられそうな型
5. 次回投稿の方針を決める。

```json
{
  "date": "YYYY-MM-DD",
  "good_patterns": [],
  "bad_patterns": [],
  "buzz_patterns": [],
  "todays_policy": {
    "theme": "",
    "type": "",
    "hook": "",
    "tone": "",
    "avoid": []
  },
  "insight": "今回の分析で得た気づきを一言で"
}
```

6. `data/analysis/index.json` を読み、最新ファイルの `file_info.count` が300行を超えていれば新しいファイル（`analysis_年_連番.json`）を作成する。年が変わっていれば連番をリセットする。
7. 上記エントリーを対象ファイルの `entries` に追記し、`file_info` を更新する。
8. `data/analysis/index.json` を更新する。
   - `files` に対象ファイル名を追加する。
   - `total_files` を再集計する。
   - `insights` に今回の `insight` を追加する（直近のものが末尾に来るようにする）。
   - `last_updated` を実行日に更新する。

## 注意
- `todays_policy` は次の `04_generate.md` の入力になる。曖昧な表現を避け、具体的なテーマ・型・トーンを指定する。
- `data/profile.json` の `ng` に抵触するパターンは `bad_patterns` / `avoid` に必ず含める。
