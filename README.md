# poi — place data used by the mtagging (ARound) app / 장소 데이터

Version: **v1.4.0** (2026-11-14)

## English

This repository contains the place data (mountain peaks, stations and similar places in South Korea) that the **ARound** mobile app ships and uses to draw labels in its camera and map views. The data is derived from **OpenStreetMap** and is offered here under the **Open Database License (ODbL) 1.0** so that anyone can obtain a machine-readable copy free of charge.

- License: ODbL 1.0 — https://opendatacommons.org/licenses/odbl/1-0/
- Attribution: Contains information from OpenStreetMap, which is made available here under the Open Database License (ODbL). © OpenStreetMap contributors — https://www.openstreetmap.org/copyright
- The files in `data/` are byte-for-byte the files bundled in the app of this version (the files in `data/full/` are the complete, canonical lists; the app packs exactly the same records, split by region into compact tiles, and a test checks that the tiles contain exactly these records); their SHA-256 hashes are in `manifest.json`.
- Any derivative database you publicly use must also be offered under the ODbL (ODbL §4.4).

## 한국어

이 저장소에는 **ARound** 앱이 카메라·지도 화면의 라벨에 쓰기 위해 앱에 포함하는 장소 데이터(대한민국의 산 봉우리, 철도역 등)가 있습니다. 데이터는 **OpenStreetMap**에서 만들었고, 누구나 기계가 읽을 수 있는 사본을 무료로 받을 수 있도록 **Open Database License(ODbL) 1.0**으로 제공합니다.

- 라이선스: ODbL 1.0 — https://opendatacommons.org/licenses/odbl/1-0/
- 출처 표시: © OpenStreetMap contributors — https://www.openstreetmap.org/copyright
- `data/`의 파일은 이 버전의 앱에 들어 있는 파일과 바이트 단위로 같습니다(`data/full/`은 전체 정본이고, 앱은 같은 항목을 지역별 작은 타일로 나눠 담으며 타일이 이 항목들과 정확히 같은지 테스트로 확인합니다). SHA-256 해시는 `manifest.json`에 있습니다.
- 이 데이터로 만든 파생 데이터베이스를 공개적으로 쓰는 경우 ODbL로 제공해야 합니다(ODbL §4.4).

## Files / 파일

| Path | Content / 내용 | Count / 건수 | Fields / 필드 | SHA-256 |
|---|---|---:|---|---|
| `data/m.json` | 산(봉우리) / Mountains (peaks) | 561 | `name_ko, name_en, lat, lon, alt` | `56815e5e91cd…` |
| `data/s.json` | 지하철·철도역 등 장소 / Subway / railway stations and similar places | 1,247 | `name_ko, name_en, lat, lon, osm` | `2ac5262b03ce…` |
| `data/p.json` | 사찰·전망대·대피소/쉼터·화장실 / Temples, viewpoints, huts/shelters and toilets | 5,060 | `osm, k, name_ko, name_en, lat, lon, size` | `25dc87a71df6…` |
| `data/l.json` | 랜드마크(탑·등대·성곽·문화재·박물관·명소·경기장·케이블카·섬·댐·다리·폭포·해변·대학) / Landmarks (towers, lighthouses, castles, heritage sites, museums, attractions, stadiums, cable cars, islands, dams, bridges, waterfalls, beaches, universities) | 5,462 | `osm, sub, name_ko, name_en, lat, lon, size, wd` | `79875be683be…` |
| `data/full/bus.json` | 버스정류장 / Bus stops | 67,030 | `osm, name_ko, lat, lon` | `aa467d31a217…` |
| `data/full/life.json` | 약국·병원/의원·경찰/소방·관공서/우체국·주차장 / Pharmacies, hospitals/clinics, police/fire stations, offices/post offices and parking | 35,668 | `osm, k, name_ko, lat, lon, size` | `73174f94a0ac…` |

`lat`, `lon` are WGS84 degrees; `alt` is elevation in metres (peaks only). / `lat`·`lon`은 WGS84 도(degree), `alt`는 고도(m, 산만).

## Provenance and processing / 출처와 가공

- `data/m.json`
  - 한국어: OpenStreetMap의 natural=peak 중 이름이 있는 객체를 OSM Overpass API로 지역(행정구역) 단위로 조회한 뒤 선별했다(2026-09). 필드 alt는 OSM ele 태그의 고도(m)다.
  - English: Selected from named natural=peak objects in OpenStreetMap, queried region by region (administrative areas) via the OSM Overpass API (2026-09). The alt field is the elevation in metres from the OSM ele tag.
- `data/s.json`
  - 한국어: OpenStreetMap에서 만든 목록이다(2026-09 구축, 2026-11-10 출처 확인). 2026-11-08 Geofabrik 한국 추출의 railway=station 노드와 대조해(600m 안, 이름은 '역'·괄호 부기를 무시) 기존 항목에 OSM 노드 id(osm)를 붙이고, 기존에 없던 역(한글 이름이 있는 것)을 추가했다. 스크립트: scripts/build-poi-data.js.
  - English: A list built from OpenStreetMap (assembled 2026-09; source confirmed 2026-11-10). Checked against railway=station nodes in the Geofabrik South Korea extract of 2026-11-08 (within 600 m; names compared ignoring a trailing '역' and parenthetical notes): existing entries got their OSM node id (osm), and stations that were missing (with a Korean name) were added. Script: scripts/build-poi-data.js.
- `data/p.json`
  - 한국어: 2026-11-08 Geofabrik 한국 추출(OpenStreetMap)에서 뽑았다. k=temple: amenity=place_of_worship+religion=buddhist, viewpoint: tourism=viewpoint, shelter: amenity=shelter(정자·그늘막·버스 대기소·방공호 제외, 산장 tourism=alpine_hut|wilderness_hut 포함)과 이름이 대피소·산장·쉼터이거나 산악 형태인 것, toilet: amenity=toilets. 이름(name:ko→name)에 한글이 있는 것만 남기고 종류명뿐인 이름(예: '화장실')은 뺐으며, 같은 종류·이름이 100m 안이면 하나로 합쳤다. 화장실 이름 끝에는 '화장실'을 붙였다. 사찰은 면(way)으로만 그려진 것도 포함하며(osm이 w로 시작, 꼭짓점 평균을 대표점으로, size=경계 상자 대각선 m) 다른 종류는 점만 쓴다. 랜드마크와 이름이 같고 300m 안인 사찰·전망대는 l.json 쪽에만 둔다. 스크립트: scripts/build-poi-data.js.
  - English: Extracted from the Geofabrik South Korea extract of 2026-11-08 (OpenStreetMap). k=temple: amenity=place_of_worship + religion=buddhist; viewpoint: tourism=viewpoint; shelter: amenity=shelter (excluding gazebos, sun shelters, bus shelters and bomb shelters; including tourism=alpine_hut|wilderness_hut) kept only when it has a mountain-hut form or its name says shelter/hut; toilet: amenity=toilets. Only entries whose name (name:ko, else name) contains Hangul are kept; names that are just the category word (e.g. '화장실') are dropped; same kind and name within 100 m are merged; ' 화장실' is appended to toilet names. Temples mapped only as areas (ways) are included too (osm starting with w; the representative point is the mean of the outline vertices; size = bounding-box diagonal in metres); other kinds use points only. Temples and viewpoints with the same name within 300 m of a landmark are kept only in l.json. Script: scripts/build-poi-data.js.
- `data/l.json`
  - 한국어: 2026-11-08 Geofabrik 한국 추출(OpenStreetMap)의 노드(점)·way(면/선)·relation(경복궁 같은 멀티폴리곤)에서 뽑았다. osm은 n(점)·w(way)·r(relation)+OSM id. 면/선/관계는 꼭짓점 평균(다리·댐은 선의 중간 지점)을 대표점으로 하고 size에 크기를 적었다(다리는 길이 m, 그 밖은 경계 상자 대각선 m). sub: tower(man_made=tower 중 전망·통신탑), lighthouse, castle(historic=castle|fort|fortress), heritage(heritage 태그, 또는 이름이 궁·성·릉·사지 등인 historic=ruins|archaeological_site), bridge(man_made=bridge, 이름이 대교로 끝나 300m 이상이거나 교로 끝나 1km 이상, 램프·고가·육교 제외), dam, museum, attraction(tourism=attraction|theme_park|zoo|aquarium 중 위키 문서가 있거나 테마파크·동물원·수족관이거나 경계 상자 200m 이상), stadium, cablecar(aerialway=station), island, waterfall, beach, university(이름이 대학교·대학·캠퍼스로 끝나는 것). 이름(name:ko→name)에 한글이 있는 것만 남기고 같은 sub·이름이 300m 안이면 점을 남겨 하나로 합쳤다. wd=1은 OSM에 wikidata 또는 wikipedia 태그가 있다는 뜻이다. 스크립트: scripts/build-poi-data.js.
  - English: Extracted from nodes (points), ways (areas/lines) and relations (multipolygons such as Gyeongbokgung) of the Geofabrik South Korea extract of 2026-11-08 (OpenStreetMap). osm is n (node), w (way) or r (relation) plus the OSM id. For ways and relations the representative point is the mean of the outline vertices (the midpoint along the line for bridges and dams) and size gives the extent (bridges: length in metres; others: bounding-box diagonal in metres). sub: tower (man_made=tower observation/communication), lighthouse, castle (historic=castle|fort|fortress), heritage (heritage tag, or historic=ruins|archaeological_site whose name contains palace/fortress/tomb/temple-site words), bridge (man_made=bridge whose name ends in 대교 and is at least 300 m, or ends in 교 and is at least 1 km; ramps, flyovers and footbridges excluded), dam, museum, attraction (tourism=attraction|theme_park|zoo|aquarium that has a wiki page, is a theme park/zoo/aquarium, or has a bounding box of at least 200 m), stadium, cablecar (aerialway=station), island, waterfall, beach, university (names ending in 대학교/대학/캠퍼스). Only entries whose name (name:ko, else name) contains Hangul are kept; same sub and name within 300 m are merged, keeping the point. wd=1 means the OSM object has a wikidata or wikipedia tag. Script: scripts/build-poi-data.js.
- `data/full/bus.json`
  - 한국어: 2026-11-08 Geofabrik 한국 추출(OpenStreetMap)의 highway=bus_stop 노드와 amenity=bus_station(터미널)에서 뽑았다. 이름(name:ko→name)에 한글이 있는 것만 남기고, 끝의 정류장 번호 "(02-005)"를 지우고 이름에 정류장·터미널·역이 없으면 " 정류장"을 붙였다. 옛 시설 표기((구)·(삭제) 등)는 뺐고, 같은 이름이 80m 안(도로 양쪽 쌍)이면 하나로 합쳤다. 노선·도착 정보는 없다. 좌표는 소수 5자리. 앱에는 같은 항목이 위도 0.2° × 경도 0.25° 격자 타일로 들어 있다. 스크립트: scripts/build-poi-data.js.
  - English: Extracted from highway=bus_stop nodes and amenity=bus_station (terminals) of the Geofabrik South Korea extract of 2026-11-08 (OpenStreetMap). Only entries whose name (name:ko, else name) contains Hangul are kept; a trailing stop number such as "(02-005)" is removed and " 정류장" (bus stop) is appended unless the name already says stop/terminal/station. Former-facility markers such as (구)/(삭제) are dropped and the same name within 80 m (the two sides of a road) is merged. There is no route or arrival information. Coordinates have 5 decimals. The app ships the same records as tiles of 0.2° latitude × 0.25° longitude. Script: scripts/build-poi-data.js.
- `data/full/life.json`
  - 한국어: 2026-11-08 Geofabrik 한국 추출(OpenStreetMap)의 점·면(way)·관계(relation)에서 뽑았다. k=pharmacy: amenity=pharmacy / hospital: amenity=hospital|clinic|doctors, healthcare=hospital|clinic / police: amenity=police|fire_station(이름에 경찰·파출소·지구대·치안센터·소방·119·안전센터·구조대) / office: amenity=townhall, office=government, amenity=post_office(이름에 시청·구청·군청·도청·청사·주민센터·행정복지센터·사무소·우체국 등) / parking: amenity=parking(사유지·노상 주차 제외, 이름 없는 것은 경계 상자 120m 이상 또는 수용 50대 이상만 "주차장"으로, 아파트 동 내부 시설 제외). 이름에 한글이 있는 것만 남기고(주차장 예외), 이름 끝 영문 표기를 지우고, 옛 시설 표기((구) 등)와 종류명뿐인 이름은 뺐으며, 같은 종류·이름이 100m(주차장 60m) 안이면 하나로 합쳤다. 면·관계는 꼭짓점 평균을 대표점으로 하고 size에 경계 상자 대각선(m)을 적었다. 위치만 있고 영업 여부·운영 시간은 없다. 좌표는 소수 5자리. 앱에는 같은 항목이 격자 타일로 들어 있다. 스크립트: scripts/build-poi-data.js.
  - English: Extracted from nodes, ways and relations of the Geofabrik South Korea extract of 2026-11-08 (OpenStreetMap). k=pharmacy: amenity=pharmacy; hospital: amenity=hospital|clinic|doctors, healthcare=hospital|clinic; police: amenity=police|fire_station (name must mention police/koban/fire/119/rescue words); office: amenity=townhall, office=government, amenity=post_office (name must be a city/district/county/provincial hall, community centre, office or post office); parking: amenity=parking (private and on-street excluded; unnamed lots only if their bounding box is at least 120 m or capacity at least 50, labelled "주차장"; apartment-block internal lots excluded). Only entries whose name contains Hangul are kept (parking excepted); trailing romanization is removed; former-facility markers such as (구) and names that are just the category word are dropped; the same kind and name within 100 m (60 m for parking) are merged. For ways and relations the representative point is the mean of the outline vertices and size is the bounding-box diagonal in metres. Locations only: no opening hours or whether the place is still operating. Coordinates have 5 decimals. The app ships the same records as region tiles. Script: scripts/build-poi-data.js.

Processing rules (cleaning, de-duplication, name normalisation) are applied when the lists are regenerated; each release records what was done in `CHANGELOG.md`. / 목록을 다시 만들 때 적용한 정제 규칙(중복 제거, 이름 정리 등)은 릴리스마다 `CHANGELOG.md`에 기록합니다.

## Versions / 버전

Every release is a git tag (`vMAJOR.MINOR.PATCH`) and is archived on Zenodo (DOI on the release page). Old tags are never removed, so the data used by older app versions stays available. / 모든 릴리스는 git 태그이며 Zenodo에도 보관됩니다(DOI는 릴리스 페이지). 이전 태그는 삭제하지 않으므로 구버전 앱이 쓰는 데이터도 계속 받을 수 있습니다.
