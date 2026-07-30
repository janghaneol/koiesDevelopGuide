# 부속물 계산

부속물 도메인은 학교 일반건물 개별 단위의 면적, 고가건물 개별 단위의 대장가액, 가입 기간, 적용 요율을 바탕으로 **가입금액** 및 **최종 공제회비**를 산정합니다.

---

## 1. 구성 요소 (Components)

| 구분 | 클래스/파일명 | 역할 및 기능 |
| :--- | :--- | :--- |
| **Service** | `BuildingService` | 가입 요청 수신, 도메인 계산 호출, 결과 반환 |
| **Domain** | `BuildingServiceImpl` | 건물 회비/가입금액 산정 및 연도별 Policy 적용 |
| **Mapper** | `BuildingMapper` | 건물 기준 단가 조회 및 산출 결과 저장 |
| **DTO** | `BuildingDto` | 건물 계산 입/출력 데이터 전송 객체 |

---

## 2. 일반건물 계산 Method (`genrBldgCal`)

| 클래스/파일명 | 메소드명 | 입력 타입 | 출력 타입 |
| :--- | :--- | :--- | :--- |
| `BuildingServiceImpl` | `genrBldgCal` | `Map<String, Object>` | `BuildingDto` |

### 입력 (Input)

| 항목 (Property) | 설명 | 데이터 타입 | 비고 / 예시 |
| :--- | :--- | :--- | :--- |
| `joinYr` | 가입년도 | `String` | YYYY (예: `"2026"`) |
| `genrBldgJoinArea` | 건축면적 (㎡) | `BigDecimal` | 예: `1500.50` |
| `siBldgUsgSeCd` | 건물보유구분 | `String` | 예: 건물보유구분코드(`"101"`) |
| `muaJoinBgngMm` | 가입 시작월 | `String` | MM (예: `"01"`) |
| `muaJoinEndMm` | 가입 종료월 | `String` | MM (예: `"12"`) |

### 출력 (Output)

| 항목 (Property) | 설명 | 데이터 타입 | 산출 방식 |
| :--- | :--- | :--- | :--- |
| `genrBldgJoinAmt` | 가입금액 | `BigDecimal` | 면적 × 연도별 지급한도액 |
| `genrBldgMuaMbfeeAmt` | 공제회비 | `BigDecimal` | 면적 x 연도별 기준단가 × (기본 요율 - 환급요율 / 100)|

### 💡 주요 계산 정책 (Business Rules)

* **12월 17일 이후 가입 건 공제회비 감면**
  * 가입일자(`joinDte`)가 **12월 17일 이후**인 경우, 산출된 최종 공제회비의 **50%를 적용 (산출금액 × 0.5)**합니다.

---

## ⚙️후처리 로직 (Post-Processing Flow)

### **배상책임 회비 재계산 및 UPDATE**
   - **조건:** 건물 등록 성공 시 무조건 실행
   - **내용:** 등록된 건물의 면적 및 용도 코드를 기반으로 배상책임 회비 산출 후 `TB_MS_CMPNS_RSPN_JOIN_D` 테이블 업데이트
   - [배상책임 등록](Cmpns.md)

---

## 참조 SQL

```SQL

SELECT BASE_UNIT_PRICE
  FROM TB_BLDG_FEE_RATE
 WHERE JOIN_YR = #{joinYr}
   AND USE_YN  = 'Y'

```