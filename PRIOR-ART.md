# 先行例(prior art)

miso-geo の形式 —— Markdown に GeoJSON を埋め込み、Web 地図で見せる —— に、近い先行例があるかの調査記録。2026-11-20。標準の Web 検索(8回)と、EOxElements の資料の読み取り1回による。**どの道具も実際には動かしていない**。「見つからなかった」ことは、無いことの証明ではない。

## 先行例

| 先行例 | 位置の持ち方 | 本文と地図 | 備考 |
| --- | --- | --- | --- |
| [GitHub](https://github.blog/changelog/2022-03-17-mermaid-topojson-geojson-and-ascii-stl-diagrams-are-now-supported-in-markdown-and-as-files/) | Markdown のコードフェンス(`geojson` / `topojson`)に GeoJSON を直接 | 地図は、そのブロックの位置に出る。資料に同期の記述はない | Leaflet で描画。座標系は CRS84 のみ。約750を超えるマーカーはまとめて表示([GitHub Docs](https://docs.github.com/en/repositories/working-with-files/using-files/working-with-non-code-files)) |
| [Kartographer](https://www.mediawiki.org/wiki/Help:Extension:Kartographer)(Wikipedia、Wikivoyage) | wikitext の `<mapframe>` / `<maplink>` に GeoJSON を直接 | 本文の途中に地図を埋め込む | マーカーに title、description などの属性。MediaWiki のサーバーが要る |
| [Obsidian Map View](https://github.com/esm7/obsidian-map-view) | ノートの frontmatter の `location`、または本文中の `geo:` リンク | ノート単位でピンが並ぶ | 取得した資料には、点の例しかない |
| [Mapbox storytelling](https://github.com/mapbox/storytelling)、[opengeos/maplibre-gl-storymaps](https://ghproxy-9d2.pages.dev/opengeos/maplibre-gl-storymaps) | 章ごとの地図の視点を `config.js` に書く | スクロールで章ごとに flyTo | Markdown ではなく設定ファイル |
| [EOxElements `eox-storytelling`](https://github.com/EOX-A/EOxElements) | Markdown の見出しに、HTML コメントで地図の状態を付ける | **本文のスクロールと地図が同期する** | MIT。unpkg から読め、ビルド不要。地図のレイヤーは URL で指す形で、GeoJSON の直接埋め込みは確認できなかった。最新リリース 1.14.0(2026-11-09) |
| Quarto / Observable | コードのセルで JS にデータとして読み込む | 文書の中に地図のセル | コードの文書。静的に公開すると Python のカーネルがない([Quarto](https://prerelease.quarto.org/docs/interactive/widgets/jupyter.html)) |

MkDocs で `geojson` フェンスを描画するプラグインは、検索では見つからなかった(無い、と確認したわけではない)。

## miso-geo は何が違うか

調べた範囲で、次の組み合わせを1つでそろえたものは見つからなかった。

- プレーンな Markdown。
- GeoJSON を本文に直接埋め込む(GitHub と Kartographer は埋め込めるが、スクロール同期がない。EOx は同期するが、埋め込みは確認できなかった)。
- スクロール同期の Story Map 風の表示。
- サーバーなしで動く。

踏み跡ごとの状態(`verified` など)の記法は、EOx にも見当たらなかった。ただし、これは「見つからなかった」にとどまる。

## 示唆

- 「地図つきの Markdown」という発想自体は、新しくない。独立に何度も実現されている。需要の傍証でもある。
- **互換性で取り込める。** コードフェンスを `geojson` にすると、GitHub のプレビューで地図が出る。2026-11-20 に確認した: 素のジオメトリ(`Feature` で包まない)の `geojson` フェンスが、GitHub 上でピンつきの地図として描かれた(D18)。
- EOx とは機能が重なる。自作のビューアを続ける理由が、GeoJSON の直接埋め込みと、状態の表示にあるかを、見極める必要がある。

## この調査の限界

- EOx の README は 503 で読めなかった。使っている地図ライブラリや、flyTo の有無は未確認。
- どの道具も動かしていない。Kartographer、Obsidian、Mapbox 系の挙動は、資料の記述にとどまる。
