# poi — place data used by the mtagging (ARound) app / 장소 데이터

Version: **v1.0.0** (2026-11-11)

## English

This repository contains the place data (mountain peaks, stations and similar places in South Korea) that the **ARound** mobile app ships and uses to draw labels in its camera and map views. The data is derived from **OpenStreetMap** and is offered here under the **Open Database License (ODbL) 1.0** so that anyone can obtain a machine-readable copy free of charge.

- License: ODbL 1.0 — https://opendatacommons.org/licenses/odbl/1-0/
- Attribution: Contains information from OpenStreetMap, which is made available here under the Open Database License (ODbL). © OpenStreetMap contributors — https://www.openstreetmap.org/copyright
- The files in `data/` are byte-for-byte the files bundled in the app of this version; their SHA-256 hashes are in `manifest.json`.
- Any derivative database you publicly use must also be offered under the ODbL (ODbL §4.4).

## 한국어

이 저장소에는 **ARound** 앱이 카메라·지도 화면의 라벨에 쓰기 위해 앱에 포함하는 장소 데이터(대한민국의 산 봉우리, 철도역 등)가 있습니다. 데이터는 **OpenStreetMap**에서 만들었고, 누구나 기계가 읽을 수 있는 사본을 무료로 받을 수 있도록 **Open Database License(ODbL) 1.0**으로 제공합니다.

- 라이선스: ODbL 1.0 — https://opendatacommons.org/licenses/odbl/1-0/
- 출처 표시: © OpenStreetMap contributors — https://www.openstreetmap.org/copyright
- `data/`의 파일은 이 버전의 앱에 들어 있는 파일과 바이트 단위로 같습니다. SHA-256 해시는 `manifest.json`에 있습니다.
- 이 데이터로 만든 파생 데이터베이스를 공개적으로 쓰는 경우 ODbL로 제공해야 합니다(ODbL §4.4).

## Files / 파일

| Path | Content / 내용 | Count / 건수 | Fields / 필드 | SHA-256 |
|---|---|---:|---|---|
| `data/m.json` | 산(봉우리) / Mountains (peaks) | 561 | `name_ko, name_en, lat, lon, alt` | `77146f1e8f7c…` |
| `data/s.json` | 지하철·철도역 등 장소 / Subway / railway stations and similar places | 944 | `name_ko, name_en, lat, lon` | `00b5fe2a25c8…` |

`lat`, `lon` are WGS84 degrees; `alt` is elevation in metres (peaks only). / `lat`·`lon`은 WGS84 도(degree), `alt`는 고도(m, 산만).

## Provenance and processing / 출처와 가공

- `data/m.json`
  - 한국어: OpenStreetMap의 natural=peak 중 이름이 있는 객체를 OSM Overpass API로 지역(행정구역) 단위로 조회한 뒤 선별했다(2026-09). 필드 alt는 OSM ele 태그의 고도(m)다.
  - English: Selected from named natural=peak objects in OpenStreetMap, queried region by region (administrative areas) via the OSM Overpass API (2026-09). The alt field is the elevation in metres from the OSM ele tag.
- `data/s.json`
  - 한국어: OpenStreetMap에서 만든 목록이다(2026-09 구축, 2026-11-10 출처 확인). 2026-11-08 Geofabrik 한국 추출 전체와 대조하면 944건 중 934건(99%)이 railway=station 객체와 600m 안에서 일치한다.
  - English: A list built from OpenStreetMap (assembled 2026-09; source confirmed 2026-11-10). Compared with the full Geofabrik South Korea extract of 2026-11-08, 934 of 944 entries (99%) match a railway=station object within 600 m.

Processing rules (cleaning, de-duplication, name normalisation) are applied when the lists are regenerated; each release records what was done in `CHANGELOG.md`. / 목록을 다시 만들 때 적용한 정제 규칙(중복 제거, 이름 정리 등)은 릴리스마다 `CHANGELOG.md`에 기록합니다.

## Versions / 버전

Every release is a git tag (`vMAJOR.MINOR.PATCH`) and is archived on Zenodo (DOI on the release page). Old tags are never removed, so the data used by older app versions stays available. / 모든 릴리스는 git 태그이며 Zenodo에도 보관됩니다(DOI는 릴리스 페이지). 이전 태그는 삭제하지 않으므로 구버전 앱이 쓰는 데이터도 계속 받을 수 있습니다.
