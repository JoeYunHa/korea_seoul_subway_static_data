Subway Dataset Documentation / 지하철 데이터셋 설명서

Here is the README file describing the uploaded subway datasets. It includes descriptions of the files, their columns, and the relationships between them in both English and Korean.

---

# Subway Data Overview / 지하철 데이터 개요

## Introduction / 소개

This dataset collection provides comprehensive information about the subway system, including line metadata, station details, connectivity (sections) between stations, and congestion levels by time.
이 데이터셋 컬렉션은 노선 메타데이터, 역 정보, 역 간 연결성(구간), 시간대별 혼잡도를 포함하여 지하철 시스템에 대한 포괄적인 정보를 제공합니다.

---

## File Descriptions / 파일 설명

### 1. `subway_line.csv`

Contains metadata for subway lines.
지하철 노선에 대한 메타데이터를 포함합니다.

| Column (컬럼)  | Description (English)                  | 설명 (Korean)             |
| -------------- | -------------------------------------- | ------------------------- |
| `line_id`      | Unique identifier for the line         | 노선 고유 식별자          |
| `line`         | Short name of the line (e.g., "1호선") | 노선 단축명 (예: "1호선") |
| `line_name`    | Full official name of the line         | 노선 공식 명칭            |
| `line_subname` | Specific branch or sub-name            | 지선 또는 세부 명칭       |
| `color`        | Color code representing the line (Hex) | 노선 대표 색상 코드 (Hex) |
| `created_at`   | Record creation timestamp              | 데이터 생성 일시          |
| `updated_at`   | Record update timestamp                | 데이터 수정 일시          |

### 2. `subway_station.csv`

Provides detailed information about individual subway stations, including their locations.
개별 지하철역에 대한 상세 정보와 위치 정보를 제공합니다.

| Column (컬럼)    | Description (English)                | 설명 (Korean)                |
| ---------------- | ------------------------------------ | ---------------------------- |
| `station_id`     | Unique identifier for the station    | 역 고유 식별자               |
| `line`           | Line the station belongs to          | 역이 속한 노선명             |
| `name`           | Station name (Korean)                | 역명 (한글)                  |
| `station_nm_eng` | Station name (English)               | 역명 (영문)                  |
| `station_cd`     | Station code used in the system      | 시스템에서 사용하는 역 코드  |
| `fr_code`        | Foreign code (often used on signage) | 외부 표기용 코드 (표지판 등) |
| `bldn_id`        | Building or facility ID              | 건물 또는 시설 ID            |
| `lat`            | Latitude                             | 위도                         |
| `lng`            | Longitude                            | 경도                         |
| `geom`           | Geometry point (WKT format)          | 위치 좌표 (WKT 형식)         |
| `created_at`     | Record creation timestamp            | 데이터 생성 일시             |
| `updated_at`     | Record update timestamp              | 데이터 수정 일시             |

### 3. `subway_section.csv`

Defines the connectivity between stations, representing the path (edges) of the subway network.
역 간의 연결성을 정의하며, 지하철 네트워크의 경로(edge)를 나타냅니다.

| Column (컬럼)       | Description (English)                   | 설명 (Korean)               |
| ------------------- | --------------------------------------- | --------------------------- |
| `section_id`        | Unique identifier for the section       | 구간 고유 식별자            |
| `line`              | Line the section belongs to             | 구간이 속한 노선명          |
| `up_station_name`   | Name of the previous (upstream) station | 이전 역(상행) 명칭          |
| `up_station_code`   | Code of the previous station            | 이전 역 코드                |
| `down_station_name` | Name of the next (downstream) station   | 다음 역(하행) 명칭          |
| `down_station_code` | Code of the next station                | 다음 역 코드                |
| `section_order`     | Order of the section within the line    | 노선 내 구간 순서           |
| `via_coordinates`   | List of coordinates for the path        | 경로를 구성하는 좌표 리스트 |
| `created_at`        | Record creation timestamp               | 데이터 생성 일시            |
| `updated_at`        | Record update timestamp                 | 데이터 수정 일시            |

### 4. `congestion_total.csv`

Contains congestion level data for stations at 30-minute intervals.
30분 간격의 역별 혼잡도 데이터를 포함합니다.

| Column (컬럼)          | Description (English)                  | 설명 (Korean)                |
| ---------------------- | -------------------------------------- | ---------------------------- |
| `요일구분`             | Day type (e.g., Weekday, Sunday)       | 요일 구분 (예: 평일, 일요일) |
| `호선`                 | Line name                              | 노선명                       |
| `역번호`               | Station number                         | 역 번호                      |
| `출발역`               | Station name                           | 역명                         |
| `상하구분`             | Direction (Up/Down line)               | 상하행 구분                  |
| `5시30분` ~ `00시30분` | Congestion level at specific times (%) | 특정 시간대의 혼잡도 (%)     |

---

## Data Relationships / 데이터 관계

- **Lines & Stations**: `subway_station.csv` and `subway_line.csv` are linked by the line name (`line` / `호선`).
- **Stations & Sections**: `subway_section.csv` connects stations found in `subway_station.csv` using station names and codes (`up_station_code`, `down_station_code`).
- **Congestion**: `congestion_total.csv` can be joined with `subway_station.csv` using the station name (`출발역` = `name`) and line (`호선` = `line`) to analyze congestion on a map.
- **노선 및 역**: `subway_station.csv`와 `subway_line.csv`는 노선명(`line` / `호선`)으로 연결됩니다.
- **역 및 구간**: `subway_section.csv`는 역 이름과 코드(`up_station_code`, `down_station_code`)를 사용하여 `subway_station.csv`에 있는 역들을 연결합니다.
- **혼잡도**: `congestion_total.csv`는 역명(`출발역` = `name`)과 노선(`호선` = `line`)을 사용하여 `subway_station.csv`와 결합해 지도상에서 혼잡도를 분석할 수 있습니다.

### 2. `subway_station.csv`

Provides detailed information about individual subway stations, including their locations.
개별 지하철역에 대한 상세 정보와 위치 정보를 제공합니다.

| Column (컬럼)    | Description (English)                | 설명 (Korean)                |
| ---------------- | ------------------------------------ | ---------------------------- |
| `station_id`     | Unique identifier for the station    | 역 고유 식별자               |
| `line`           | Line the station belongs to          | 역이 속한 노선명             |
| `name`           | Station name (Korean)                | 역명 (한글)                  |
| `station_nm_eng` | Station name (English)               | 역명 (영문)                  |
| `station_cd`     | Station code used in the system      | 시스템에서 사용하는 역 코드  |
| `fr_code`        | Foreign code (often used on signage) | 외부 표기용 코드 (표지판 등) |
| `bldn_id`        | Building or facility ID              | 건물 또는 시설 ID            |
| `lat`            | Latitude                             | 위도                         |
| `lng`            | Longitude                            | 경도                         |
| `geom`           | Geometry point (WKT format)          | 위치 좌표 (WKT 형식)         |
| `created_at`     | Record creation timestamp            | 데이터 생성 일시             |
| `updated_at`     | Record update timestamp              | 데이터 수정 일시             |

### 3. `subway_section.csv`

Defines the connectivity between stations, representing the path (edges) of the subway network.
역 간의 연결성을 정의하며, 지하철 네트워크의 경로(edge)를 나타냅니다.

| Column (컬럼)       | Description (English)                   | 설명 (Korean)               |
| ------------------- | --------------------------------------- | --------------------------- |
| `section_id`        | Unique identifier for the section       | 구간 고유 식별자            |
| `line`              | Line the section belongs to             | 구간이 속한 노선명          |
| `up_station_name`   | Name of the previous (upstream) station | 이전 역(상행) 명칭          |
| `up_station_code`   | Code of the previous station            | 이전 역 코드                |
| `down_station_name` | Name of the next (downstream) station   | 다음 역(하행) 명칭          |
| `down_station_code` | Code of the next station                | 다음 역 코드                |
| `section_order`     | Order of the section within the line    | 노선 내 구간 순서           |
| `via_coordinates`   | List of coordinates for the path        | 경로를 구성하는 좌표 리스트 |
| `created_at`        | Record creation timestamp               | 데이터 생성 일시            |
| `updated_at`        | Record update timestamp                 | 데이터 수정 일시            |

### 4. `congestion_total.csv`

Contains congestion level data for stations at 30-minute intervals.
30분 간격의 역별 혼잡도 데이터를 포함합니다.

| Column (컬럼)          | Description (English)                  | 설명 (Korean)                |
| ---------------------- | -------------------------------------- | ---------------------------- |
| `요일구분`             | Day type (e.g., Weekday, Sunday)       | 요일 구분 (예: 평일, 일요일) |
| `호선`                 | Line name                              | 노선명                       |
| `역번호`               | Station number                         | 역 번호                      |
| `출발역`               | Station name                           | 역명                         |
| `상하구분`             | Direction (Up/Down line)               | 상하행 구분                  |
| `5시30분` ~ `00시30분` | Congestion level at specific times (%) | 특정 시간대의 혼잡도 (%)     |

---

## Data Relationships / 데이터 관계

- **Lines & Stations**: `subway_station.csv` and `subway_line.csv` are linked by the line name (`line` / `호선`).
- **Stations & Sections**: `subway_section.csv` connects stations found in `subway_station.csv` using station names and codes (`up_station_code`, `down_station_code`).
- **Congestion**: `congestion_total.csv` can be joined with `subway_station.csv` using the station name (`출발역` = `name`) and line (`호선` = `line`) to analyze congestion on a map.
- **노선 및 역**: `subway_station.csv`와 `subway_line.csv`는 노선명(`line` / `호선`)으로 연결됩니다.
- **역 및 구간**: `subway_section.csv`는 역 이름과 코드(`up_station_code`, `down_station_code`)를 사용하여 `subway_station.csv`에 있는 역들을 연결합니다.
- **혼잡도**: `congestion_total.csv`는 역명(`출발역` = `name`)과 노선(`호선` = `line`)을 사용하여 `subway_station.csv`와 결합해 지도상에서 혼잡도를 분석할 수 있습니다.
