# アーチェリーフォーム分析AI

右射ちリカーブ向けのフォーム分析Webアプリです。練習動画を選ぶと、ブラウザの中で姿勢を推定し、フォームを計測します。

**公開ページ:** Cloudflare Pages で公開（URLはデプロイ後にここへ記載）

## 特徴

- 総合点は付けません。結果は「観測結果／再現性／基準の射との違い／基本フォーム確認／判定不可」の5つに分けて表示します
- 動画は端末の外に送信されません。姿勢推定も保存も、すべて自分のスマホ・PCの中で完結します
- 8つのフェーズ（スタンス〜フォロースルー）を自動で推定し、手で直すこともできます
- 一番よかった射を「基準の射」にして、次の分析と比べられます

## 使い方

1. 撮影方向（右側面／左側面／後方）を選ぶ
2. 動画を選ぶ
3. フェーズを確認して「分析する」
4. 結果を見て、必要なら保存する

安全のため、射線より前に人やスマホを置かないでください。

## 公開の仕組み（引き継ぎ用メモ）

- このリポジトリ（GitHub）に `index.html` が入っています。これがアプリ本体のすべてです
- `main` ブランチへ push すると GitHub Actions が Cloudflare Pages へ自動でデプロイします
  - 必要な Secrets（リポジトリの Settings → Secrets and variables → Actions）:
    - `CLOUDFLARE_API_TOKEN` … Cloudflare の API トークン（Pages の編集権限）
    - `CLOUDFLARE_ACCOUNT_ID` … Cloudflare のアカウントID
- リポジトリを他の人へ渡すとき: Settings → General → Danger Zone → Transfer ownership
- Cloudflare 側を渡すとき: Cloudflare ダッシュボードで Pages プロジェクト `archery-form-ai` を相手のアカウントへ移すか、相手をアカウントメンバーに招待します

## 技術メモ

- 姿勢推定: MediaPipe Pose Landmarker（ブラウザ内実行、CDNから読み込み）
- データ保存: ブラウザの localStorage（端末内のみ）
