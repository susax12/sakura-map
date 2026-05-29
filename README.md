# 全国 桜マップ — SAKURA DRONE PROJECT

日本地図から撮影地を選んで、DRONE ENTERTAINMENT の桜ドローン空撮映像（YouTube）を視聴できる単一HTMLページ。

- **公開URL**: https://susax12.github.io/sakura-map/
- デザイン: claude.ai/design リデザイン（雅/rose）を移植。明朝見出し・和紙トーン・ブルームクラスタ・サムネピン・舞う花びら
- データソース: YouTube [@drone-entertainment](https://www.youtube.com/@drone-entertainment) 全公開動画から抽出（地図掲載 **125スポット / 134動画**）
- 地域フィルタ＋桜の種類フィルタ＋検索、詳細パネル、撮影地一覧ドロワー
- 同一スポットの複数動画はピンに集約（パネルで動画切替）
- ブランド（配色・フォント・ロゴ）は [drone-entertainment.co.jp](https://drone-entertainment.co.jp/) に準拠

## 構成

| ファイル | 役割 |
|---|---|
| `index.html` | 本体（地図・データ・UI 全部入りの単一HTML・バニラJS） |
| `design.md` | デザインガイド（雅/rose）＋データ連携＋移植方針 |
| `assets/logo_dark.svg` | 会社公式ロゴ（濃色＋赤、明色ヘッダー用） |
| `assets/logo_de.svg` / `logo_white.svg` | 旧版ロゴ（暗色ヘッダー用・未使用） |

## データ更新

`index.html` 内の `const SPOTS = [...]` に1行追加。形状は `{id,name,pref,city,region,type,lat,lng,videos:[{ytId,label,title}]}`。同一スポットへの動画集約は `MERGE` で定義。桜の種類(`type`)は動画タイトルから自動推定（要会社確認）。

## ステータス

社内レビュー用プレビュー。品質確定後に会社HPへ移植予定（iframe先行 → 固定ページ化）。
