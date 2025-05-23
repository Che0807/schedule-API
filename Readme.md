# Lv 1 schedules API 명세서

<details> 
  <summary> 일정 생성 API </summary>

### 일정 생성 API (POST `/schedules`)

| 항목       | 설명                |
|----------|-------------------|
| URL      | `/schedules`      |
| Method   | `POST`            |
| 설명       | 새로운 일정을 생성합니다.    |
| Request  | JSON Body (아래 참고) |
| Response | 등록 성공 메시지 + ID    |
| Status   | `201 Created`     |

#### Request Body

|          필드명 | 타입       | 설명     | 필수 여부 |
|-------------:|----------|--------|-------|
|   `username` | `String` | 사용자 이름 | O     |
|     `tiltle` | `String` | 일정 제목  | O     |
|       `todo` | `String` | 일정 할일  | O     |
| `created_at` | `Date`   | 생성 시간  | O     |
| `updated_at` | `Date`   | 수정시간   | O     |

```json
{
  "username": "유정명",
  "title": "할일 제목",
  "todo": "할일 내용",
  "created_at": "2025-05-19",
  "updated_at": "2025-05-19"
}
```

#### Response Body (성공 시)

```json
{
  "id": 1,
  "username": "유정명",
  "title": "할일 제목",
  "todo": "할일 내용",
  "created_at": "2025-05-19",
  "updated_at": "2025-05-19"
}
```

---

### 상태 코드 요약

| 코드            | 의미       |
|---------------|----------|
| `201 Created` | 일정 등록 성공 |

---
</details>

<details>
<summary> 일정 다건 조회 </summary>

### 일정 전체조회 API (GET `/schedules`)

| 항목       |        설명         |
|----------|:-----------------:|
| URL      |    `/schedles`    |
| Method   |       `GET`       |
| 설명       | 등록된 일정을 다건 조회합니다. |
| Request  |        없음         |
| Response |      일정 리스트       |
| Status   |     `200 OK`      |

#### Response Body (성공 시)

```json
[
  {
    "id": 1,
    "username": "유정명",
    "title": "할일 제목",
    "todo": "할일 내용",
    "created_at": "2025-05-19",
    "updated_at": "2025-05-19"
  },
  {
    "id": 2,
    "username": "우정명",
    "title": "할일 제목",
    "todo": "할일 내용",
    "created_at": "2025-05-19",
    "updated_at": "2025-05-19"
  }
]

```

___

### 상태 코드 요약

| 코드       | 의미          |
|----------|-------------|
| `200 OK` | 전체 일정 조회 성공 |

</details>

<details>
<summary> 일정 단건 조회 </summary>

### 일정 단건조회 API (GET `/schedules/{id}`)

| 항목       |            설명             |
|----------|:-------------------------:|
| URL      |     `/schedles/{id}`      |
| Method   |           `GET`           |
| 설명       |     등록된 일정을 단건 조회합니다.     |
| Request  |      경로 파라미터{userID}      |
| Response |         해당 일정 정보          |
| Status   | `200 OK, 404 Not Found 등` |

#### Path Variable

| 파라미터명 | 타입   | 설명         | 필수 여부 |
|-------|------|------------|-------|
| `id`  | Long | 조회할 일정의 ID | O     |

#### Response Body (성공 시)

```json 
 {
  "id": 1,
  "username": "유정명",
  "title": "할일 제목",
  "todo": "할일 내용",
  "created_at": "2025-05-19",
  "updated_at": "2025-05-19"
}


```

___

### 상태 코드 요약

| 코드              | 의미            |
|-----------------|---------------|
| `200 OK`        | 전체 일정 조회 성공   |
| `404 Not Found` | 해당 ID의 일정이 없음 |

</details>

<details>
  <summary> 일정 수정 API</summary>

### 일정 수정 API 명세 (PATCH `/schedules/{id}`)

| 항목       | 설명                 |
|----------|--------------------|
| URL      | `/schedules/{id}`  |
| Method   | `PATCH`            |
| 설명       | 특정 ID의 일정을 수정합니다.  |
| Request  | JSON Body (아래 참고)  |
| Response | 수정된 일정 정보          |
| Status   | `200 OK` , `404` 등 |

#### Path Variable

| 이름   | 타입     | 설명         | 필수 여부 |
|------|--------|------------|-------|
| `id` | `Long` | 수정할 일정의 ID | O     |

#### Request Body

|          필드명 | 타입       | 설명     | 필수 여부 |
|-------------:|----------|--------|-------|
|   `username` | `String` | 사용자 이름 | O     |
|     `tiltle` | `String` | 일정 제목  | O     |
|       `todo` | `String` | 일정 할일  | O     |
| `created_at` | `Date`   | 생성 시간  | O     |
| `updated_at` | `Date`   | 수정시간   | O     |

```json
  {
  "id": 1,
  "username": "유정명",
  "title": "할일 제목",
  "todo": "할일 내용",
  "created_at": "2025-05-19",
  "updated_at": "2025-05-19"
}
```

#### Response Body (성공 시)

```json
  {
  "id": 1,
  "username": "수정된 유정명",
  "title": "수정된 할일 제목",
  "todo": "수정된 할일 내용",
  "created_at": "2025-05-19",
  "updated_at": "2025-05-20"
}
```

---

### 상태 코드 요약

| 코드              | 의미            |
|-----------------|---------------|
| `200 OK`        | 일정 수정 성공      |
| `404 Not Found` | 해당 ID의 일정이 없음 |

</details>

<details>
  <summary> 일정 삭제 API</summary>

### 일정 삭제 API 명세 (DELETE `/schedules/{id}`)

| 항목       | 설명                 |
|----------|--------------------|
| URL      | `/schedules/{id}`  |
| Method   | `DELETE`           |
| 설명       | 특정 ID의 일정을 삭제합니다.  |
| Request  | 없음                 |
| Response | 삭제 성공 메시지          |
| Status   | `200 OK` , `404` 등 |

#### Path Variable

| 파라미터명 | 타입   | 설명         | 필수 여부 |
|-------|------|------------|-------|
| `id`  | Long | 삭제할 일정의 ID | O     |

#### Response Body (성공 시)

```json
{
  "id": 1,
  "message": "일정이 성공적으로 삭제되었습니다."
}
```

---

### 상태 코드 요약

| 코드              | 의미                 |
|-----------------|--------------------|
| `200 OK`        | 일정 삭제 성공           |
| `404 Not Found` | 해당 ID의 일정이 존재하지 않음 |

</details>
