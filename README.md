# 全国 桜マップ — SAKURA DRONE PROJECT

日本地図から撮影地を選んで、DRONE ENTERTAINMENT の桜ドローン空撮映像（YouTube）を視聴できる単一HTMLページ。

- **公開URL**: https://susax12.github.io/sakura-map/
- データソース: YouTube [@drone-entertainment](https://www.youtube.com/@drone-entertainment) の全公開動画から抽出（地図掲載125スポット / 134動画）
- 同一スポットの複数動画はピンに集約（パネルでサムネ切替）
- ブランド（配色・フォント・ロゴ）は [drone-entertainment.co.jp](https://drone-entertainment.co.jp/) に準拠

## 構成

| ファイル | 役割 |
|---|---|
| `index.html` | 本体（地図・データ・UI 全部入りの単一HTML） |
| `design.md` | HP由来のデザインガイド＋会社HPへの移植方針 |
| `assets/logo_de.svg` | 会社公式ロゴ（白テキスト＋赤ドローンアイコン、HP配色準拠） |

## データ更新

`index.html` 内の `const SPOTS = [...]` に1行追加するだけ。同一スポットへの動画集約は `MERGE` 配列で定義。

## ステータス

社内レビュー用プレビュー。品質確定後に会社HPへ移植予定（iframe先行 → 固定ページ化）。
