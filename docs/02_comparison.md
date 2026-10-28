# 02. Comparison of the two candidates for Akita (measured on the real files, 2026-10-28)

What the data can say. No choice of a main dataset is made here.
Detailed profiles: `akita-vegetation-2024` docs/akita_profile.md and `akita-forest-resource-mesh-2026` docs/akita_profile.md.

| item | 現存植生図2024 | 全国森林資源メッシュ |
| --- | --- | --- |
| Akita coverage | whole prefecture: 174,576 polygons whose area is 11,635.884 km2, against 11,635.886 km2 for the N03 polygon (no gaps against that boundary) | 29,088,595 cells of 20 m cover 11,635.4 km2 of land, but the attributes exist only in forest-register cells: 林種 is non-NULL in 74.2% of cells |
| spatial grain | polygons of the 1/25,000 vegetation survey; polygon sizes vary | regular 20 m cells (400 m2) |
| identifies beech (ブナ) directly | yes, through the legend name: ブナ群団, ブナ群落, ブナ二次林 and mixed legends with ブナ: 4 legends (チシマザサ－ブナ群団 110100, スギ－ブナ群落 110103, ブナ－ミズナラ群落 220100, ブナ二次林 220104) | no. The tree columns hold 広葉樹 as one class; no value contains ブナ |
| identifies mizunara (ミズナラ) directly | yes: 220100 ブナ－ミズナラ群落, 220103 オオバクロモジ－ミズナラ群集, 220101 スギ－ミズナラ群落, 110501 ホツツジ－ミズナラ群集, 221100 ミズナラ群落（V） | no |
| only as far as oak class (ナラ類) | the matching is by legend name; ミヤマナラ (190100) matches ナラ but is a different thing and is not mizunara or konara | not even that: 広葉樹 only |
| konara (コナラ) | yes: 220501 オクチョウジザクラ－コナラ群集, 220500 コナラ群落（V） | no |
| unit of the information | the community (plant-sociological legend, 134 legends in Akita), the polygon is one community, not a species share | up to three tree classes per cell, ranked by area share of the register (樹種1, 2, 3) |
| private forest | all land is covered whatever the owner, the data do not say the owner | 民有林 cells (by the 森林計画対象森林レイヤ): 11,248,619; 林種 non-NULL in 98.0% of them; 国有林 cells: 9,643,128, 100% |
| missing attributes | none: 0 NULL in every column of the Akita polygons | the laser-derived columns (レーザ解析樹種, 樹冠高, 立木密度, 平均標高, 計測年月日) are 100% NULL in Akita; 森林簿樹種2 24.7% and 樹種3 9.7% non-NULL; Yuzawa private forest lacks the register in about 21% of its cells (176,552 of 829,185 cells); the text `#N/A` is a value in 207,673 cells of 森林簿樹種1 |
| data time | 作成年度 2001 to 2022 per polygon (the legends of beech and oak run over the same years; 2020 holds the most polygons) | 森林簿年月日 2019/4/1 to 2024/4/1 (mostly 2024/3/31 for private forest and 2023/4/1, 2020/4/1 for national forest); no laser date |
| licence | 公共データ利用規約 第1.0版 (PDL1.0), CC BY compatible, stated on the data record | PDL1.0 with the Forestry Agency 重要情報 and a 利用規約 with disclaimers (CKAN field says 政府標準利用規約) |
| derived redistribution on Hugging Face | allowed with attribution and a processing notice | allowed with attribution, a processing notice and the disclaimers |
| size of the Akita extract | 174,576 polygons | 29.1 million cells, about 265 MB as zstd GeoParquet |

Reading notes, still without analysis:

- The vegetation map names communities (群集, 群落); it is not a species map. Its Akita legends that contain the search words number 11, together 36,259 polygons.
- The mesh is a stand register (樹種 as a coarse class), so within it beech and oak are not separable in Akita.
- Both products state the date of each original; neither is a present-day state.
