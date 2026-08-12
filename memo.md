# 作業メモ（2026-08-12時点）

## リポジトリの状態
作業ツリーはクリーン。以下のコミットが `origin/main` にpush済み。
- `505fd65` Switch prompts to interactive v2 versions, record initial analysis policy
- `4471c3b` Restructure sns-manager to index-based data layout with workflow prompts
- `6fa1c4a` Add SNS content management system scaffold

## これまでの経緯
1. `sns-manager/` を `setup_prompt_v2.md` の仕様に沿って作り直した（index.json + 連番ファイルの分割構成、`prompts/01〜04` を新設）。→ コミット `4471c3b`
2. その後、`sns-manager/prompts/01_record.md` 〜 `04_generate.md` は削除され、代わりに `prompts/prompt_01_record_v2.md` 〜 `prompt_04_generate_v2.md` が追加された（対話形式・毎日運用を想定した書き直し版）。
3. `02_collect_v2` を試したが、Web検索では実際のX/Threadsの投稿本文・反応数を正確に取得できず、実在URLがないと収集できないと判断。収集は見送り、`data/buzz/` は空のまま。
4. `03_analyze_v2` を実行。実績・バズデータが0件だったため、`good_patterns`/`bad_patterns`/`buzz_patterns` は空のまま、`skills/`と`data/profile.json`のコンセプトのみを根拠に「初回方針」を1件だけ `data/analysis/analysis_2026_001.json` に記録した。
   - theme: 地方フルリモートワークの一日（日常のありのままを見せる）
   - type: リアル日常型
   - hook: 結論・意外性・数字を冒頭に置き、地方フルリモートならではの視点を最初の一文で示す
   - tone: 等身大・共感重視・営業感なし
   - avoid: 誇張・煽り・直接的な宣伝・押し売り
5. `04_generate_v2` を実行。エピソード入力なしで、上記の初回方針をもとにX・Threads用のドラフトをチャット上に生成した（**ファイルには未保存**、`drafts/`にも書き出していない。まだ投稿もしていない）。
6. 上記2〜4の変更をコミット（`505fd65`）し、`origin/main` にpush済み。

## 生成済みドラフト（未投稿・未保存・ファイル化していない）
**X（94字）**
> 満員電車ゼロ、通勤時間ゼロ。それでも地方フルリモートでいまだに一番驚くのは「1日中、近所の人と一度もすれ違わない日がある」ということ。静かすぎる環境が、逆に一番集中できる時間をくれている。

**Threads（219字）**
> 地方でフルリモートをしていて、いまだに新鮮に感じることがある。それは「1日中、近所の人と一度もすれ違わない日がある」ということ。会社にいた頃は、通勤や外出のたびに誰かとすれ違うのが当たり前だった。でも今は、家の中で一日が完結してしまうこともある。最初は少し寂しさもあったけど、今では静かな環境のおかげで仕事に一番集中できる時間だと思うようになった。みなさんは、こういう「誰にも会わない日」得意な方ですか、それとも寂しく感じるタイプですか?

※「フルリモート◯年目」など、プロフィールにない具体的な勤続年数はフックに入れていない（事実確認できないため）。

## 現在のデータ状態
- `data/posts/{x,threads,instagram,tiktok}/` … 投稿実績はすべて0件
- `data/buzz/` … 収集データ0件
- `data/analysis/` … 初回方針エントリーが1件のみ（実績ベースではない、skills/profileのみ根拠）

## 次にやること（候補）
- 上記ドラフトを実際に投稿するか判断する（投稿しない場合は別テーマで再生成も可）
- 投稿したら `prompt_01_record_v2.md` の手順で `data/posts/x/` `data/posts/threads/` に記録する
- バズ収集をやる場合は、参考にしたい投稿の実URLを用意して `prompt_02_collect_v2.md` を実行する
- 実績・バズデータが貯まってきたら、`prompt_03_analyze_v2.md` で実績ベースの分析に切り替える
