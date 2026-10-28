# 01. Official sources and licences (investigated 2026-10-28)

Scope: spatial data on beech (ブナ) and oak (ミズナラ・ナラ類) in Akita Prefecture. No analysis here.
Every statement below was read on the pages and files kept under `evidence/`; the retrieval date is 2026-10-28.

## A. 現存植生図2024 (Ministry of the Environment, Biodiversity Center of Japan)

| item | finding | evidence |
| --- | --- | --- |
| official name | 現存植生図2024 (the whole country finished in 2024, hence the name) | evidence/pages/biodic_veg2024_storymap.json |
| owner | 環境省 自然環境局 生物多様性センター | same; evidence/ckan_biodic_veg2024.json (organization, author) |
| official entry points | Biodic vegetation page `https://www.biodic.go.jp/kiso/vg/vg_kiso.html` links to 環境ジオポータル, G空間情報センター and the story map; the story map says the GIS data can be viewed and downloaded at G空間情報センター, いきもの地図 and 環境ジオポータル | evidence/pages/biodic_vg_kiso.html |
| bulk download used here | G空間情報センター dataset `biodic_veg2024` (https://www.geospatial.jp/ckan/dataset/biodic_veg2024), 13 GeoPackage files by regional block; Tohoku is `veg2024bk2a.gpkg` (947,036,160 bytes) and `veg2024bk2b.gpkg` (975,659,008 bytes) | evidence/ckan_biodic_veg2024.json |
| dates | CKAN record created 2026-01-23, metadata modified 2026-08-27; the Tohoku files were last modified 2026-04-14. The CKAN record has no version field | same |
| format | GeoPackage, Polygon, UTF-8, JGD2011 (EPSG:6668) | CKAN notes |
| coverage | all Japan, by region block (1 Hokkaido, 2 Tohoku, ...) | CKAN notes |
| scale | 1/25,000 vegetation maps (maintained 1999 to 2024) | story map |
| survey years | 調査年度 2000-2023 (business years 1999-2024) | CKAN notes |
| attributes (per CKAN) | fid, 植生区分コード (I-X), 大区分コード, 中区分コード, 細区分コード, 凡例コード (6 digits), 凡例名 (876 legends), 植生自然度, 植生自然度区分, 植生区分, 作成年度, 地域ブロック | CKAN notes |
| licence | 公共データ利用規約 第1.0版 (PDL1.0), stated on the data record itself (`license_id: public-data-license-v1.0`). PDL1.0 states that it is compatible with CC BY 4.0 | evidence/ckan_biodic_veg2024.json; evidence/pages/digital_go_jp_pdl_v1.0.html |
| redistribution and derivatives | PDL1.0 allows use by anyone under 1.1 to 1.7 (attribution, no infringing third-party rights, legal limits, no endorsement as if made by the State). Editing and processing are allowed; the processed data must say that it was processed and by whom, and must not look like an unprocessed State product | PDL1.0 text; Biodic site rules (別紙 重要情報) |
| attribution required | Yes. Biodic's example: "1/25,000植生図「…」GISデータ(環境省生物多様性センター)を使用し、(作成者)が作成・加工したものである。(URL or download date)" | evidence/pages/biodic_terms_of_service.html |
| third-party or other limits | Biodic names two: no infringement of third-party rights, and legal limits such as the Survey Act (測量法) when a GSI map is used inside the content. The G空間情報センター record states no third-party material for this data. Whether the base topographic map of the 1/25,000 survey carries GSI limits is not stated for the polygons, and is recorded here as unknown | biodic_terms_of_service.html |
| decision | Licence confirmed on the data itself. Redistribution of a processed Akita extract is allowed with attribution and a processing notice. Proceed. | |

Caveat kept for the card: Biodic's site-wide rules are PDL1.0 with the 別紙 list of contents under its control; the licence of this data rests on the licence field of the G空間情報センター record published by the Biodiversity Center and on the Biodic page that points to that record.

## B. 全国森林資源メッシュ (Forestry Agency, MAFF)

| item | finding | evidence |
| --- | --- | --- |
| official name | 全国森林資源メッシュ (20 m mesh forest resource information) | evidence/ckan_mesh_10.json |
| owner | 林野庁 森林整備部 計画課 全国森林計画班 (CKAN author); the originals come from the Forestry Agency's regional offices (国有林) and the prefectures (民有林) | docs/ terms of use |
| official bulk download | G空間情報センター, organisation 林野庁, one dataset per Plane Rectangular CS zone `mesh_1` to `mesh_19`. Akita is in zone X: `mesh_10` (青森, 秋田, 山形, 岩手, 宮城) https://www.geospatial.jp/ckan/dataset/mesh_10 | evidence/ckan_mesh_10.json |
| files | 240 `.7z` archives (GeoPackage per 国土基本図図郭 quarter-sheet, `fr_mesh20m_<sheet>_2025`), plus the index GeoPackage and PDFs. CRS JGD2011 / Plane Rectangular CS X (EPSG:6678) | CKAN notes |
| dates | CKAN record created 2025-12-03, metadata modified 2026-07-27; the `.7z` files were last modified 2026-04-23; data definition dated 2026-03-23. The data are named `_2025`. The record has no version field. Originals were collected in FY2024 (令和6年度); each row carries its own 森林簿年月日 and 計測年月日 | CKAN, terms of use |
| spatial extent | land of national forest and of regional-plan private forest only (not all land) | terms of use |
| resolution | 20 m mesh polygons | notes |
| attributes (data definition) | fid, 林種, 森林簿樹種１, 森林簿樹種２, 森林簿樹種３, 林齢, 森林簿年月日, 樹冠高, レーザ解析樹種, 立木密度, 平均標高, 計測年月日. No 市町村 column and no 民国別 column in the mesh. 民国別 and 市町村 exist in the separate 森林計画対象森林レイヤ (`fr_layer_<pref>_2025`, per prefecture) | evidence/docs/data_dictionary_20260323.pdf |
| note on names | the user asked for 解析樹種; the column is named レーザ解析樹種 in the definition | |
| nulls by design | where the forest register or the laser data do not exist, the attribute is Null | CKAN notes |
| licence | The page and its licence resource name 公共データ利用規約 第1.0版 (PDL1.0) with a Forestry Agency 重要情報 PDF. The CKAN `license_id` field says `ogl` with the title 政府標準利用規約 (the predecessor of PDL1.0); the two disagree on the label but both are CC BY compatible. Recorded as PDL1.0, the one that the page text and the 重要情報 PDF state | evidence/ckan_mesh_10.json; important_notes PDF |
| attribution required | Yes: 出典：林野庁（当該ページの URL）、PDL1.0（規約原文ページの URL）. Processed data must say that it was edited and by whom, and must not look as if the Forestry Agency made it | evidence/docs/important_notes_on_public_data_usage_mesh_terms_v1.0.pdf |
| redistribution and derivatives | allowed under PDL1.0 with the two notices above. A separate 全国森林資源メッシュの利用規約 adds disclaimers: not a proof of ownership, boundaries, area, tax or timber value; the data show the time of each original, not today; errors can arise when the original holders prepare their originals; laser-derived information has no guaranteed accuracy; no liability | evidence/docs/national_forest_resource_mesh_terms_of_use.pdf |
| third-party or other limits | personal information law applies if the data are matched with a personal-information database | important_notes PDF |
| decision | Licence confirmed on the data itself (record, 重要情報 PDF, 利用規約 PDF). Redistribution of a processed Akita extract is allowed with attribution and a processing notice. Proceed. | |

The mesh is an edited product of the Forestry Agency built from prefectural registers. Akita private forest comes from the Akita register (the data definition lists Akita as type B: small-compartment polygons merged).

## Open points carried to the next steps

- Akita boundary used for clipping: to be taken from an official source (KSJ N03) and used only as a cutter; it is not republished.
- Prefecture-specific conditions on the Akita register itself: none stated in the Forestry Agency terms. Not checked on Akita Prefecture's own pages (listed as unknown).
- The vegetation record has no 重要情報 PDF; none was found.
