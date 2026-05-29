# 桜マップ デザインガイド（v2 / 雅・rose）

claude.ai/design のリデザイン（高忠実度ハンドオフ）を、現行の単一HTML・バニラJS構成に移植したもの。フレームワークは持ち込まず、雅(miyabi)/rose アクセントの1テーマで実装。

> 設計の出典: `design_handoff_sakura_map`（claude.ai/design 製プロトタイプ）。本実装はその雅/rose状態を再現したもの。

---

## コンセプト

「桜らしい上品な」トーン。地図を淡く後退させ、桜（ブルームクラスタ・サムネピン・舞う花びら）を主役にする。和紙のような明色チップUIをフローティングで重ねる。

## デザイントークン（雅 / rose）

- **フォント**: 見出し＝`Shippori Mincho B1`（明朝）、UI/本文＝`Zen Kaku Gothic New`
- **色**（oklch、`:root` にベイク済み）:
  - `--sakura` `oklch(0.75 0.085 5)` ／ `--sakura-deep` `oklch(0.6 0.135 9)`（主アクセント・カウント・アクティブ）
  - `--sakura-ink` `oklch(0.5 0.13 10)` ／ `--sakura-wash` `oklch(0.93 0.03 4)`
  - `--paper` `oklch(0.985 0.008 78)` ／ `--ink` `oklch(0.27 0.014 40)`
  - YouTube CTA = `#ff0033`
- **ガラス**: chrome 面に `backdrop-filter: blur(16–18px) saturate(1.4)`
- **地図タイル**: 地理院 pale + CSS filter `saturate(.6) brightness(1.05) contrast(.95) sepia(.04)`
- **角丸**: card/panel 16px、小 11px、pill 999px、menu 14px
- **影**: card / pop の2段。**モーション**: panel/drawer `.34/.32s cubic-bezier(.22,1,.36,1)`、map fly `.7–.8s`

## 画面/コンポーネント

| 要素 | 仕様 |
|---|---|
| ヘッダー | フローティングのガラスバー。左に会社公式ロゴ（`logo_dark.svg`、濃色＋赤）/ 区切り / ❀桜マップ（明朝）/ 右に SPOTS カウント（明朝・大） |
| フィルタバー | 地域チップ（横スクロール・件数バッジ・アクティブ=赤）＋ 検索 ＋ 絞り込み解除 |
| マーカー | ブルームクラスタ（放射グラデ＋赤コア・件数で44/54/66/78px）／ サムネピン（86×58・実YouTubeサムネ・県名縦帯・🌸・複数動画バッジ・下向きテイル） |
| 詳細パネル | 右スライドイン（モバイル=ボトムシート）。ポスター＋再生→iframe、県名タグ、明朝タイトル、メタ（本数・4K）、複数動画リスト、赤YouTube CTA、共有（リンクコピー/Web Share） |
| 一覧ドロワー | 左スライドイン。検索＋地域別グループ、サムネ＋名前 |
| 花びら | 16枚の ambient falling petals（`prefers-reduced-motion` で無効） |

## データ連携

- ソース: YouTube `@drone-entertainment` 全公開動画152本 → 地図掲載 **125スポット / 134動画**
- 除外16本: オンライン花見(2) / プロジェクト紹介・総集編(8) / 非桜FPV撮影(6)
- **同一スポットの複数動画**は1ピンに集約（`MERGE` で6グループ）。パネルで動画切替
- スポット形状: `{id,name,pref,city,region,type,lat,lng,videos:[{ytId,label,title}]}`
- **地域**: region id（hokkaido…kyushu、沖縄は kyushu に統合）
- サムネ: 実 YouTube サムネ（`img.youtube.com/vi/<id>/mqdefault.jpg`）
- 注: 桜の品種フィルタは v2.1 で削除（推定精度が不十分なため）。`type` フィールドはデータに残るが UI 未使用
- 座標: 市町村レベル概算（Nominatim、精度70%）

## ハンドオフからの主な相違（実データ適応）

- プレースホルダのグラデサムネ → **実YouTubeサムネ**に置換
- 汎用ペタルマーク → **会社公式ロゴ**（明色ヘッダー用に濃色＋赤の `logo_dark.svg`）
- `views`(再生数) は実データ無し → **捏造せず省略**（メタは「本の動画」「4K」の2項目）
- React+Babel プロトタイプ → **バニラJSで再実装**（単一HTML・GitHub Pages運用を維持）
- 淡/墨テーマ・Tweaksパネル・dotピンは**未実装**（雅/roseのみ）

## 公開・移植

- 共有URL: https://susax12.github.io/sakura-map/
- 共有用ディープリンク `?spot=<videoId>`
- 会社HP（WordPress）移植は iframe 先行 → 固定ページ化（推奨70%）

## 未確定・要判断（※要検証）

- [ ] 座標を実際の木の位置へ補正するか
- [ ] 再生数（views）を表示するか（YouTube Data API 連携 or 手入力）
- [ ] 淡/墨テーマや英語併記の要否
