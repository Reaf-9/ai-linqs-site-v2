# AI Linqs コーポレートサイト v2（テスト版）

社長の理想構成（ダークテーマ・1ページLP）で現行HPを作り直す v2。**本番（ai-linqs.com）にはまだ反映しない。**

- テスト公開：GitHub Pages `https://reaf-9.github.io/ai-linqs-site-v2/`（リポジトリ `Reaf-9/ai-linqs-site-v2`）
- 本番（v1）：`../ai-linqs-site-pages/`（お名前.com へ FTP。v2 とは完全に別管理）
- CV：LINE友だち追加 `https://lin.ee/XFEkgJS`

## 構成

- `index.html` … HTML / CSS / JS をこの1ファイルに集約（外部ライブラリなし。Google Fonts の Inter ＋ 和文用 Noto Sans JP のみ）
- `assets/` … 画像

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
| `hero-01-kobe.jpg`（PC 2560×1440）／`hero-01-kobe-sp.jpg`（SP 1080×1920） | Adobe Stock 455397400「摩耶山から見た神戸市の夜景」（通常ライセンス・4000×2667）から切り出し。灯りの色を残すため CSS の filter は他の3枚より弱め |
| `hero-02〜04.jpg`（PC 2560×1440）／`hero-02〜04-sp.jpg`（SP 1080×1920） | v1 背景と同じ Adobe Stock ライセンス版（`../ai-linqs-site/assets/背景/`）から切り出し。02=bg-people／03=bg-connect／04=bg-city |
| `works-01〜04.jpg`（1200×900） | 同じ4枚から別の画角で切り出し（サイト上に「写真はイメージです」と表記） |
| `line-qr.png` `signature.png` | v1 から複製 |

写真の色味（彩度・明るさ）は画像ではなく CSS の `filter` で落としているので、元の jpg は明るいまま。

## 公開前に必ず外す・決めるもの

- [ ] `<meta name="robots" content="noindex,nofollow">` を外す
- [ ] 画面に出ている `[要確認]` 表記の解消（v1 から持ち越し）
  - 「2030年には、644万人の労働力不足」の出典
  - 「中小企業ではAI活用が遅れ格差が広がりつつある」の数値・出典
  - 広告内製化コーチング／LPコーチングの料金
- [ ] 導入事例3社の掲載許諾の最終確認（v1 から持ち越し）
- [ ] Works の写真を実際の写真に差し替えるか判断（現在はストック写真の切り出し）
- [ ] ヒーローの拠点行に設立年（EST.）を入れるか（設立年が未確定のため「KOBE, JAPAN」のみ）
- [ ] 本番切替時、v1 の旧URL（about / services / service / cases / contact / privacy .html）をどうするか（リダイレクト or 残す）

※ 左下の「TEST · v2」バッジは github.io とローカルでだけ表示される。本番ドメインでは自動で消える。
