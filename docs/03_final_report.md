# 03. Final report (2026-10-29)

## Datasets and fixed revisions

| dataset | GitHub | Hugging Face | fixed revision | content |
| --- | --- | --- | --- | --- |
| akita-vegetation-2024 | https://github.com/yuiseki/akita-vegetation-2024 | https://huggingface.co/datasets/yuiseki/akita-vegetation-2024 | `b3b36a0fb6ff027fb1f483be3288df2df76c0cf3` | 174,576 polygons (235 MB, GeoParquet, EPSG:6668) |
| akita-forest-resource-mesh-2026 | https://github.com/yuiseki/akita-forest-resource-mesh-2026 | https://huggingface.co/datasets/yuiseki/akita-forest-resource-mesh-2026 | `1cad01a041ad2e1bfc2fa9ba35bd1385070d3f5f` | 29,088,595 cells in 60 files (278 MB in all, GeoParquet, EPSG:6678) |

Both were read back from the Hub at these revisions (checksums of every file, rows, schema, CRS, extent, validity, value counts, NULL counts) and matched the local copies and the profiles. Both were also checked against the raw sources with a second engine (DuckDB spatial): zero differences in the selected rows, the attributes and the geometry.

## 1. Licence and redistribution

- 現存植生図2024: 公共データ利用規約 第1.0版 (PDL1.0), stated on the data record; CC BY 4.0 compatible. Redistribution of a processed Akita extract is allowed with the source and a processing notice. Done.
- 全国森林資源メッシュ (and the 森林計画対象森林レイヤ used for ownership and municipality): PDL1.0 with the Forestry Agency 重要情報 and a 利用規約 with disclaimers. Redistribution of a processed extract is allowed with the source, a processing notice and the disclaimers (carried in the card). The CKAN licence field says 政府標準利用規約, the text and the PDF say PDL1.0. Done.
- Not redistributed: the data definition PDF of the Forestry Agency (it forbids reproduction). Its checksum is kept; the earlier commit 10e80df of this repository still contains the PDF in its history, because a history rewrite was not carried out.

## 2. 現存植生図2024: how far beech and oak can be told apart in Akita

- By legend name, directly: ブナ in 4 legends (チシマザサ－ブナ群団, スギ－ブナ群落, ブナ－ミズナラ群落, ブナ二次林), ミズナラ in 5 (ホツツジ－ミズナラ群集, ブナ－ミズナラ群落, スギ－ミズナラ群落, オオバクロモジ－ミズナラ群集, ミズナラ群落（V）), コナラ in 2 (コナラ群落（V）, オクチョウジザクラ－コナラ群集). ミヤマナラ (190100) matches ナラ but is neither. 11 legends in all, 36,259 polygons.
- A polygon is a community, not a species share; the legends overlap in meaning, so areas must not be summed as one class.
- Survey years of the polygons are 2001 to 2022. The map covers all land with no gaps against the N03 boundary and has no NULL.

## 3. 全国森林資源メッシュ: how far tree species can be told apart in Akita

- Only coarse classes: スギ, ヒノキ類, マツ類, カラマツ, ヒバ, エゾマツ, その他針葉樹, 広葉樹, タケ, その他, 伐採跡地. All broad-leaved trees are 広葉樹. ブナ, ミズナラ, ナラ and コナラ are not identifiable (0 cells).
- スギ is identifiable: 9,875,955 cells as 森林簿樹種1.
- The laser-derived columns (レーザ解析樹種, 樹冠高, 立木密度, 平均標高, 計測年月日) are NULL in every Akita cell.

## 4. Private-forest coverage and main gaps (mesh)

- 林種 is non-NULL in 74.2% of the Akita cells (the forest register area). 民有林 11,248,619 cells (林種 non-NULL in 98.0%), 国有林 9,643,128 cells (100%).
- Yuzawa private forest: 176,552 of 829,185 cells (21%) have no register value; 八峰町 and 能代市 have a few percent; the other municipalities are almost complete.
- 森林簿樹種2 and 3 are present in 24.7% and 9.7% of cells, much more often in 国有林 (森林簿樹種2 69%) than in 民有林 (4%).
- `#N/A` as a text value in 207,673 cells; 林齢 above 200 in 723,712 cells (up to 2023, which looks like a year); 林齢 0 in 432,421 cells; 2 duplicated cell positions in the source.

## 5. Data limits to keep in mind for later analysis

- The two products answer different questions: community names (vegetation) against register classes (mesh). They have different dates (survey years 2001 to 2022 against register dates 2019 to 2024) and different grains (polygons against 20 m cells).
- Cells are assigned to Akita by their centre, vegetation polygons are clipped at the N03 boundary; edges at the prefecture line are an administrative boundary and not a survey line.
- Ownership and municipality in the mesh are not in the source mesh; they come from the 森林計画対象森林レイヤ by cell centre, and 931,623 cells have a register value but no layer polygon.
- Neither product proves present-day state; the Forestry Agency terms say explicitly that the mesh is not a proof of ownership, boundary, area or timber value.
- Not checked: any condition that Akita Prefecture itself attaches to its register (the Forestry Agency terms state none), and whether the base map of the 1/25,000 vegetation survey carries Geospatial Information Authority limits (not stated for the polygons).
