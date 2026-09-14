# AI Linqs コーポレートサイト v2（テスト版）

社長の理想構成（ダークテーマ・1ページ）で現行HPを作り直す v2。**本番（ai-linqs.com）にはまだ反映しない。**

背景は「1本の飛行映像をスクロールで進める」方式（参考：horyx.studio のリール）。写真の切り替えではなく、連番画像 150 枚を `<canvas>` に描き、スクロール位置でコマを進める。

- テスト公開：GitHub Pages `https://reaf-9.github.io/ai-linqs-site-v2/`（リポジトリ `Reaf-9/ai-linqs-site-v2`）
- 本番（v1）：`../ai-linqs-site-pages/`（お名前.com へ FTP。v2 とは完全に別管理）
- CV：LINE友だち追加 `https://lin.ee/XFEkgJS`

## 構成

- `index.html` … HTML / CSS / JS をこの1ファイルに集約（外部ライブラリなし。Google Fonts の Inter ＋ 和文用 Noto Sans JP のみ）
- `assets/seq/pc/f0001〜f0150.jpg`（1440×810）／`assets/seq/sp/`（608×1080、中央を 9:16 で切り出し）… 背景映像の連番
- `assets/` … そのほかの画像

### 背景の仕組み

- `.world`（fixed）の canvas に、スクロール位置に応じたコマを描く。`data-frame="0.2"` の付いた章（`.chapter`）が画面中央に来た時にその割合の位置になる。章と章の間は直線補間、ページ末尾で 100%
- 入口はヒーローの1枚（神戸の夜景 `.world__poster`）。最初の 70vh で映像に溶ける
- 連番は「16枚おき → 8 → 4 → 2 → 全部」の順に読み込み、未読込のコマは読み込み済みの最寄りで代用する
- 読み物のセクションは背景を 88〜92% の黒で透かして世界を薄く見せる。章①〜③は透かさない

## 文言の出どころ（改変しない）

v1（`ai-linqs-site-pages` コミット `759e474`）の7ページの文言を、すべてこの1ページに移植している。

| v1 のページ | v2 での位置 |
|---|---|
| index.html | ヒーロー（4コピー＝旧ヒーロー＋見せ場①〜③）／Issues／Why AI Linqs／Works 内 Our Stance／Process／FAQ 前半／Contact 見出し |
| about.html | 01 Philosophy（ABOUT・Mission/Vision/Value）／05 Company（代表メッセージ・設立背景・会社情報） |
| services.html | 02 Service（Guide・Lineup・士業AI・サービス比較・「どれが合うか分からない方へ。」） |
| service.html | 02 Service 内「学ぶ、から、任せるへ。」（AI研修・教育／AI社員・AI部署長構築）／FAQ 後半／FAQ 下の相談導線 |
| cases.html | 03 Works（3社の課題・成果／Voice）／4枠目「うちも同じ課題がある」 |
| contact.html | 06 Contact（無料相談で分かること・QR・LINEボタン・個人情報の注記） |
| privacy.html | フッターの「プライバシーポリシー」から開くモーダル（全文）。`#privacy` 付きURLで直接開く |

## 画像の出どころ

| ファイル | 出どころ |
|---|---|
| `seq/pc/`・`seq/sp/` | Seedance 2.5（Higgsfield 経由）で生成した 10 秒の飛行映像（基板の上 → 光の渦 → 光の都市）。元 mp4 と生成プロンプトは `../02_sozai/v2_背景映像_Seedance2.5_07ccbe6c.mp4` と下記 |
| `hero-01-kobe.jpg`（PC 2560×1440）／`hero-01-kobe-sp.jpg`（SP 1080×1920） | Adobe Stock 455397400「摩耶山から見た神戸市の夜景」（通常ライセンス・4000×2667）から切り出し。入口の1枚 |
| `hero-01〜04*.jpg` | 旧構成（4枚スライド）の名残。未使用 |
| `works-01〜04.jpg`（1200×900） | 同じ4枚から別の画角で切り出し（サイト上に「写真はイメージです」と表記） |
| `line-qr.png` `signature.png` | v1 から複製 |

写真の色味（彩度・明るさ）は画像ではなく CSS の `filter` で落としているので、元の jpg は明るいまま。

背景映像の生成プロンプト（Seedance 2.5・16:9・10s・1080p・音なし・2026-09-14）：

> Cinematic single unbroken shot, first-person camera gliding forward at a steady constant speed through a dark digital world. Begins flying low over a vast matte-black circuit board landscape with thin glowing warm-gold traces and tiny amber lights; the camera lifts and enters a tunnel of flowing golden data streams and fine light filaments rushing past; then emerges high above an endless futuristic city of light at night, built from server towers and circuit-like streets, warm gold and amber lights on deep black, soft haze, gentle bokeh. Smooth forward dolly, no camera shake, no cuts, no zoom bursts. Minimal, elegant, luxurious, high contrast, matte black surfaces, desaturated palette except warm gold highlights. No text, no letters, no logos, no people, no faces, no screens with UI. Photorealistic, ultra-detailed, shallow depth of field, calm slow-motion feel.

連番の切り出しは ffmpeg ではなく macOS 標準の AVFoundation（Swift）で行った（`seq.swift`：等間隔 150 枚、末尾 2% は捨てる）。

## 公開前に必ず外す・決めるもの

- [ ] `<meta name="robots" content="noindex,nofollow">` を外す
- [ ] 画面に出ている `[要確認]` 表記の解消（v1 から持ち越し）
  - 「2030年には、644万人の労働力不足」の出典
  - 「中小企業ではAI活用が遅れ格差が広がりつつある」の数値・出典
  - 広告内製化コーチング／LPコーチングの料金
- [ ] 導入事例3社の掲載許諾の最終確認（v1 から持ち越し）
- [ ] Works の写真を実際の写真に差し替えるか判断（現在はストック写真の切り出し）
- [ ] ヒーローの拠点行に設立年（EST.）を入れるか（設立年が未確定のため「KOBE, JAPAN」のみ）
- [ ] 背景連番の重さ（PC 約15MB／SP 約8MB）。本番前に枚数・画質を詰めるか、WebP 化を検討
- [ ] スマホ用の映像は PC 用の中央を切り出しているだけ。縦向きの映像を別に生成するか判断
- [ ] 本番切替時、v1 の旧URL（about / services / service / cases / contact / privacy .html）をどうするか（リダイレクト or 残す）

※ 左下の「TEST · v2」バッジは github.io とローカルでだけ表示される。本番ドメインでは自動で消える。
