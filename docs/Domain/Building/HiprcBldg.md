# 고가건물

## 개요

고가건물의 가입정보를 바탕으로 **가입금액** 및 **최종 공제회비**를 산정합니다.

---

## 고가건물 계산 Method

| 클래스/파일명 | 메소드명 | 입력 타입 | 출력 타입 |
| :--- | :--- | :--- | :--- |
| `BuildingServiceImpl` | `hiprcBldgCal` | `Map<String, Object>` | `BuildingDto` |

### 입력 (Input)

| 항목 (Property) | 설명 | 데이터 타입 | 비고 / 예시 |
| :--- | :--- | :--- | :--- |
| `joinYr` | 가입년도 | `String` | YYYY (예: `"2026"`) |
| `bldgLdgrPcamt` | 건물대장가액 (원) | `BigDecimal` | 예: `10,000,000,000` |
| `archYr` | 건축년도 | `String` | YYYY (예:`"2026"`) |
| `muaJoinBgngMm` | 가입 시작월 | `String` | MM (예: `"01"`) |
| `muaJoinEndMm` | 가입 종료월 | `String` | MM (예: `"12"`) |

### 출력 (Output)

| 항목 (Property) | 설명 | 데이터 타입 | 산출 방식 |
| :--- | :--- | :--- | :--- |
| `hiprcBldgJoinAmt` | 가입금액 | `BigDecimal` | 건물대장가액 /  1-(0.02 * (가입연도-건축연도)) |
| `hiprcBldgMuaMbfeeAmt` | 공제회비 | `BigDecimal` | 가입금액  x (기본요율/100) x (기본 요율 - 환급요율 / 100)|

---

### 📸 화면 기준 산출 예시 (Example)

![고가건물 공제회비 계산 화면 스크린샷](/images/hiprc_bldg_cal_example.png)

> **[예시 시나리오]**<br>
> • **건물대장가액(`bldgLdgrPcamt`):** `10,000,000,000` 원<br>
> • **건축년도(`archYr`):** `"1999"` : 가입년도 - 건축년도 =>  **27** <br>
> • **가입 기간:** 1월 ~ 12월 (12개월 / 환급요율 0% 가정)

* **가입금액 산출:** `10,000,000,000` (대장가액) / (1 - (0.02 * `27`(가입연도-건축연도))) = **`21,739,130,434` 원**
* **공제회비 산출:** `21,739,130,434` (가입금액) × `(0.0134 / 100)` (기본요율) = **`2,913,040` 원**

> 📌 **참고:** 가입일자가 **12월 18일**인 경우 감면 정책(50%)이 적용되어 최종 공제회비는 `2,913,040 × 0.5` 원으로 산출됩니다.


## 참조 SQL

```SQL

/*연도별 월가입요율 및 단가조회*/
SELECT BSC_FRT, mua_frt1, mua_frt2 ...
  FROM TB_MA_HIPRC_BLDG_MUA_FRT_I
 WHERE substr(aplcn_bgng_dte,1,4)=#{joinYr}
   AND mas_no = '1'

/*연도별 월환급요율 및 단가조회*/
SELECT rmbr_frt1, rmbr_frt2 ...
  FROM tb_ma_hiprc_bldg_rmbr_frt_i
 WHERE substr(aplcn_bgng_dte,1,4)=#{joinYr}
   AND mas_no = '1'

```