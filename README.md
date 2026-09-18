# AI Linqs コーポレートサイト v2（テスト版）

社長の理想構成（ダークテーマ・1ページ）で現行HPを作り直す v2。**本番（ai-linqs.com）にはまだ反映しない。**

背景は「1本の映像をスクロールで進める」方式（参考：horyx.studio のリール）。写真の切り替えではなく、連番画像 150 枚を `<canvas>` に描き、スクロール位置でコマを進める。

映像の物語（案2・2026-09-14）：**① 夜明けの事務所で帳票と向き合う経営者 → ② 帳票から青い光が立ち上がり、隣に光のパートナー（AI）が現れる → ③ 明るい職場で社員たちとAIの同僚が並んで働く → ④ 夜明けの港町。会社から光の線が街と空へ伸びる**。「AIは働く人のパートナー」「人とAIは共存できる」「AIを入れた会社がどう飛躍するか」を1本で見せる。人＝暖色、AI＝青の光。

文章は「1スクロール＝1メッセージ」。42 のスライド（各 1 画面）で構成し、長い説明（サービス詳細①②・比較表・プライバシーポリシー）は「詳しく見る」で開く小窓（`<dialog>`）に入れて、画面上の文字量を抑えつつ v1 の文言はすべて残している。

- テスト公開：GitHub Pages `https://reaf-9.github.io/ai-linqs-site-v2/`（リポジトリ `Reaf-9/ai-linqs-site-v2`）
- 本番（v1）：`../ai-linqs-site-pages/`（お名前.com へ FTP。v2 とは完全に別管理）
- CV：LINE友だち追加 `https://lin.ee/XFEkgJS`

## 構成

- `index.html` … HTML / CSS / JS をこの1ファイルに集約（外部ライブラリなし。Google Fonts の Inter ＋ 和文用 Noto Sans JP のみ）
- `assets/seq/pc/f0001〜f0150.jpg`（1280×720）／`assets/seq/sp/`（540×960、中央を 9:16 で切り出し）… 背景映像の連番。3本の5秒クリップ（①→②／②→③／③→④）を 50 枚ずつつなげたもの
- `assets/seq/pc-lo/`（480×270）／`assets/seq/sp-lo/`（270×480）… 同じ連番の軽い版（1枚 25KB 前後）。先にこちらを読んで動きを見せ、後から高解像度に置き換える
- `assets/` … そのほかの画像

### 背景の仕組み

- `.world`（fixed）の canvas に、スクロール位置に応じたコマを描く。`data-frame="0.3"` の付いた章（`.chapter`）が画面中央に来た時にその割合の位置になる（章① CONNECTION＝30%：AIが現れる／章② PARTNERSHIP＝62%：共に働く／章③ THE FUTURE＝90%：街へ）。章と章の間は直線補間、ページ末尾で 100%
- 入口はヒーローの1枚（神戸の夜景 `.world__poster`）。最初の 70vh で映像に溶ける
- 連番は「16枚おき → 8 → 4 → 2 → 全部」の順に読み込むが、常に「いま見ている位置の±14枚」を優先する。読む順は「近くの低解像度（4枚おき）→ 近くの高解像度 → 残りの低解像度 → 残りの高解像度」。見ている位置から遠いコマの通信は打ち切る。`decode()` 済みのものだけ描き、隣り合う2コマを重ねて描くことでコマ送りを滑らかに見せる。未読込のコマは読み込み済みの最寄りで代用（回線が遅いときのカクつき対策・2026-09-18）
- 各スライドは左側にグラデーションの影を敷いて文字を読ませる。canvas 全体にも `brightness(.78)` をかけている（③の明るい職場でも白文字が読めるように）

## 文言の出どころ（改変しない）

v1（`ai-linqs-site-pages` コミット `759e474`）の7ページの文言を、すべてこの1ページに移植している。

| v1 のページ | v2 での位置 |
|---|---|
| index.html | ヒーロー／章①〜③（旧見せ場①〜③）／Issues（3画面）／Why AI Linqs（3画面）／Our Stance／Process（4画面）／FAQ 前半／Contact 見出し |
| about.html | Philosophy（Mission／Vision／Value 各1画面）／Company（代表メッセージ・設立背景・会社情報） |
| services.html | Service（Guide・主要3サービス各1画面・Lineup・士業AI・「どれが合うか分からない方へ。」）。比較表は小窓 `#detail-compare` |
| service.html | 小窓 `#detail-training`（学ぶ、から、任せるへ。／AI研修・教育の詳細）と `#detail-aistaff`（AI社員・AI部署長構築の詳細）／FAQ 後半／FAQ 下の相談導線 |
| cases.html | Works（3社 各1画面：課題・成果）／Our Stance に Voice の一文／「うちも同じ課題がある」 |
| contact.html | Contact（3画面：見出し／無料相談で分かること／QR・LINEボタン・個人情報の注記） |
| privacy.html | フッターの「プライバシーポリシー」から開くモーダル（全文）。`#privacy` 付きURLで直接開く |

## 画像の出どころ

| ファイル | 出どころ |
|---|---|
| `seq/pc/`・`seq/sp/` | 絵コンテ4枚（GPT Image 2.5）→ Seedance 2.5 の始点・終点画像指定で 5 秒×3 本を生成（Higgsfield 経由）。絵コンテは `../03_参考資料/v2_背景映像_絵コンテ案2.jpg`、元 mp4 は `../02_sozai/v2_背景映像_案2_clip1〜3.mp4`。案1（基板→渦→光の都市、`v2_背景映像_Seedance2.5_07ccbe6c.mp4`）は「まっすぐ進むだけで単調」で不採用 |
| `hero-01-kobe.jpg`（PC 2560×1440）／`hero-01-kobe-sp.jpg`（SP 1080×1920） | Adobe Stock 455397400「摩耶山から見た神戸市の夜景」（通常ライセンス・4000×2667）から切り出し。入口の1枚 |
| `line-qr.png` `signature.png` | v1 から複製 |

写真の色味（彩度・明るさ）は画像ではなく CSS の `filter` で落としているので、元の jpg は明るいまま。

案1（不採用）の生成プロンプト（Seedance 2.5・16:9・10s・1080p・音なし・2026-09-14）：

> Cinematic single unbroken shot, first-person camera gliding forward at a steady constant speed through a dark digital world. Begins flying low over a vast matte-black circuit board landscape with thin glowing warm-gold traces and tiny amber lights; the camera lifts and enters a tunnel of flowing golden data streams and fine light filaments rushing past; then emerges high above an endless futuristic city of light at night, built from server towers and circuit-like streets, warm gold and amber lights on deep black, soft haze, gentle bokeh. Smooth forward dolly, no camera shake, no cuts, no zoom bursts. Minimal, elegant, luxurious, high contrast, matte black surfaces, desaturated palette except warm gold highlights. No text, no letters, no logos, no people, no faces, no screens with UI. Photorealistic, ultra-detailed, shallow depth of field, calm slow-motion feel.

連番の切り出しは ffmpeg ではなく macOS 標準の AVFoundation（Swift）で行った（`seq.swift`：クリップごとに等間隔 50 枚、末尾 2% は捨てる、開始番号を指定してつなぐ）。

## 公開前に必ず外す・決めるもの

- [ ] `<meta name="robots" content="noindex,nofollow">` を外す
- [ ] 画面に出ている `[要確認]` 表記の解消（v1 から持ち越し）
  - 「2030年には、644万人の労働力不足」の出典
  - 「中小企業ではAI活用が遅れ格差が広がりつつある」の数値・出典
  - 広告内製化コーチング／LPコーチングの料金
- [ ] 導入事例3社の掲載許諾の最終確認（v1 から持ち越し）。社名表記も確認：現HPは「門正運輸株式会社」、9/17 打合せ記録では「門真」
- [ ] 写真・ロゴの差し込み（社長の写真＝代表メッセージ横、事例企業の看板前の写真＝各事例の下、ロゴ＝ヘッダー）。差し込み位置は index.html にコメントで用意済み（`assets/ceo.jpg`・`assets/case-01〜03.jpg`・`assets/logo.png`）
- [ ] 「ROI起点で話す」を平易な表現にするか（打合せ方針：経営層に専門用語を使わない）。社長の判断待ち
- [ ] 社長への確認依頼文：`../v2_社長確認依頼文.md`
- [ ] ヒーローの拠点行に設立年（EST.）を入れるか（設立年が未確定のため「KOBE, JAPAN」のみ）
- [ ] 背景連番の重さ（PC 約18MB／SP 約10MB）。本番前に枚数・画質を詰めるか、WebP 化を検討
- [ ] スマホ用の映像は PC 用の中央を切り出しているだけ。縦向きの映像を別に生成するか判断
- [ ] 本番切替時、v1 の旧URL（about / services / service / cases / contact / privacy .html）をどうするか（リダイレクト or 残す）

※ 左下の「TEST · v2」バッジは github.io とローカルでだけ表示される。本番ドメインでは自動で消える。
