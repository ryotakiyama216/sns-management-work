# SNSコンテンツ管理システム セットアップ v2

## あなたの役割
以下の指示に従い、SNSコンテンツ管理システムを新しいディレクトリ構成で作成してください。
既存の `sns-manager/` がある場合は削除してから作成してください。

---

## 発信者プロフィール
- 20代・地方在住フルリモートエンジニア
- 10月に第一子が生まれる予定
- コンセプト：地方フルリモートエンジニアの日常・リアルを発信し、その生活に憧れを感じてもらう
- 最終目標：noteと直接問い合わせへの自然な誘導（営業感なし）
- 活用媒体：X / Threads / Instagram / TikTok / note

---

## 作成するディレクトリ構成

```
sns-manager/
├── prompts/
│   ├── 01_record.md
│   ├── 02_collect.md
│   ├── 03_analyze.md
│   └── 04_generate.md
├── skills/
│   ├── x.md
│   ├── threads.md
│   ├── instagram.md
│   ├── tiktok.md
│   └── note.md
├── data/
│   ├── posts/
│   │   ├── x/
│   │   │   ├── index.json
│   │   │   └── x_2025_001.json
│   │   ├── threads/
│   │   │   ├── index.json
│   │   │   └── threads_2025_001.json
│   │   ├── instagram/
│   │   │   ├── index.json
│   │   │   └── instagram_2025_001.json
│   │   └── tiktok/
│   │       ├── index.json
│   │       └── tiktok_2025_001.json
│   ├── buzz/
│   │   ├── index.json
│   │   └── buzz_2025_001.json
│   ├── analysis/
│   │   ├── index.json
│   │   └── analysis_2025_001.json
│   └── profile.json
├── drafts/
│   └── .gitkeep
├── workflow.md
└── README.md
```

---

## ファイル分割ルール（重要）

### 基本ルール
- 1ファイルあたり最大300行まで
- 300行を超えたら新しいファイルを自動作成する
- ファイル名は `プラットフォーム_年_連番.json`（例：x_2025_001.json）
- 年をまたいだら連番をリセット（例：x_2026_001.json）

### index.jsonの役割
- 各フォルダに必ず1つ置く
- 全ファイルの目次・期間・サマリーを管理する
- Claude Codeはまずindex.jsonだけを読んで、必要なファイルだけを追加で読む
- 生データを全部読まなくてもindex.jsonのサマリーで8割の分析ができる設計にする

---

## 各index.jsonの構造

### data/posts/x/index.json（他プラットフォームも同様）
```json
{
  "platform": "X",
  "last_updated": "YYYY-MM-DD",
  "total_posts": 0,
  "files": [],
  "overall_summary": {
    "best_theme": "",
    "best_type": "",
    "avg_likes": 0,
    "avg_replies": 0,
    "avg_bookmarks": 0,
    "top_patterns": []
  }
}
```

### data/buzz/index.json
```json
{
  "last_updated": "YYYY-MM-DD",
  "total_files": 0,
  "files": [],
  "overall_patterns": []
}
```

### data/analysis/index.json
```json
{
  "last_updated": "YYYY-MM-DD",
  "total_files": 0,
  "files": [],
  "insights": []
}
```

---

## 各データファイルの構造

### data/posts/x/x_2025_001.json
```json
{
  "file_info": {
    "platform": "X",
    "file_number": 1,
    "year": 2025,
    "from": "YYYY-MM-DD",
    "to": "YYYY-MM-DD",
    "count": 0,
    "max_rows": 300
  },
  "posts": []
}
```

各投稿のスキーマ：
```json
{
  "id": "20251001-001",
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

### data/buzz/buzz_2025_001.json
```json
{
  "file_info": {
    "file_number": 1,
    "year": 2025,
    "from": "YYYY-MM-DD",
    "to": "YYYY-MM-DD",
    "count": 0,
    "max_rows": 300
  },
  "entries": []
}
```

各エントリーのスキーマ：
```json
{
  "date": "YYYY-MM-DD",
  "platform": "X | Threads",
  "persona": "投稿者のペルソナ",
  "summary": "投稿内容の要約",
  "reason": "伸びている理由",
  "type": "投稿の型",
  "hook": "フックの構造",
  "patterns": []
}
```

### data/analysis/analysis_2025_001.json
```json
{
  "file_info": {
    "file_number": 1,
    "year": 2025,
    "from": "YYYY-MM-DD",
    "to": "YYYY-MM-DD",
    "count": 0,
    "max_rows": 300
  },
  "entries": []
}
```

各エントリーのスキーマ：
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
  "insight": ""
}
```

---

## data/profile.json
```json
{
  "name": "地方フルリモートエンジニア",
  "age": "20代",
  "location": "地方（妻の実家近く）",
  "work": "フルリモートエンジニア",
  "concept": "地方フルリモートエンジニアの日常・リアルを発信し、その生活に憧れを感じてもらう",
  "goal": "noteと直接問い合わせへの自然な誘導",
  "life_event": "10月に第一子誕生予定",
  "platforms": ["X", "Threads", "Instagram", "TikTok", "note"],
  "tone": "等身大・共感重視・営業感なし",
  "ng": ["誇張", "煽り", "直接的な宣伝", "押し売り"]
}
```

---

## スキルファイルの内容

### skills/x.md
- 文字数：140字以内
- トーン：等身大・共感重視・営業感なし
- 投稿の型：①気づき型 ②リアル日常型 ③問いかけ型
- アルゴリズムの特性：エンゲージメント(リプライ・引用・保存)重視、毎日投稿推奨
- NGパターン：誇張・煽り・直接的な宣伝
- フック：最初の1行で興味を引く
- 導線：押し売りなし、プロフィールへの自然な誘導のみ

### skills/threads.md
- 文字数：150〜250字
- トーン：会話的・親しみやすい・Xより少し長め
- 投稿の型：①日常の背景を語る ②Xの投稿を深掘りした版 ③問いかけ
- アルゴリズムの特性：コメント・返信が優遇される、会話を生む終わり方が効果的
- NGパターン：一方的な情報発信、コメントしにくい締め方
- 導線：押し売りなし

### skills/instagram.md
- 形式：画像+キャプション
- キャプション文字数：100〜200字
- トーン：生活の「見た目」を見せる・憧れを作る
- 投稿の型：①作業環境 ②地方の景色・日常 ③ライフスタイルの一コマ
- ハッシュタグ：5〜10個
- アルゴリズムの特性：保存数・滞在時間が重要
- NGパターン：テキスト多すぎ・生活感のないコンテンツ

### skills/tiktok.md
- 形式：動画（15〜60秒推奨）
- キャプション：50字以内
- トーン：テンポ感・「この人面白い」と思わせる
- 投稿の型：①一日のルーティン ②地方リモートのリアル ③エンジニアあるある
- アルゴリズムの特性：最初の3秒が命・完全視聴率重視
- NGパターン：話が長い・テンポが遅い

### skills/note.md
- 文字数：1,000〜1,500字
- トーン：体験ベース・等身大・上から目線にならない
- 構成：書き出し→本論→まとめ
- 見出し：h2を2〜3個
- 役割：X・Threads・Instagram・TikTokから流入した読者の「深読み」場所
- 収益化：有料記事・マガジン・問い合わせへの自然な導線を1か所

---

## ファイル分割の自動管理ルール

①記録プロンプト実行時に以下を自動チェックすること：

1. 現在の最新データファイルの行数を確認する
2. 300行を超えていた場合、新しいファイルを作成する（連番+1）
3. index.jsonを更新する（ファイル一覧・サマリー・last_updated）
4. 新しいファイルに `file_info` を設定してから投稿を追記する

---

## 作成手順

1. 既存の `sns-manager/` を削除する
2. 上記の構成通りにすべてのディレクトリとファイルを作成する
3. 各スキルファイルに内容を日本語で丁寧に記述する
4. 全JSONファイルを正しい形式で作成する
5. 完了したらディレクトリ構成を表示して確認させてください
