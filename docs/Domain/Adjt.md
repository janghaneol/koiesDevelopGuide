# 부속물

부속물 도메인은 학교의 부속물 구분에 따른 일반부속물, 비탈면으로 분류하여 가입금액을 산출한 뒤 공제회비를 계산합니다.

- 부속물 : **취득단가**를 기준으로 가입금액을 산정합니다.
- 비탈면 : **경사도**와 **대지면적**을 기준으로 가입금액을 산정합니다.

---

## 1. 구성 요소 (Components)

| 구분 | 클래스/파일명 | 역할 및 기능 |
| :--- | :--- | :--- |
| **Service** | `AdjtService` | 가입 요청 수신, 도메인 계산 호출, 결과 반환 |
| **Domain** | `AdjtServiceImpl` | 부속물,비탈면 회비/가입금액 산정 및 연도별 정책 적용 |
| **Mapper** | `AdjtMapper` | 부속물 기준 단가 조회 및 산출 결과 Return |
| **DTO** | `AdjtDto` | 부속물 계산 입/출력 데이터 전송 객체 |

---

## 2. 부속물 가입금액 계산 Method (`selectAdjtMuaJoinAmt`)

| 클래스/파일명 | 메소드명 | 입력 타입 | 출력 타입 |
| :--- | :--- | :--- | :--- |
| `AdjtServiceImpl` | `selectAdjtMuaJoinAmt` | `Map<String, Object>` | `AdjtDto` |

### 입력 (Input)

#### 비탈면 가입금액 산출

| 항목 (Property) | 설명 | 데이터 타입 | 비고 / 예시 |
| :--- | :--- | :--- | :--- |
| `joinYr` | 가입년도 | `String` | YYYY (예: `"2026"`) |
| `ecvtJoinArea` | 대지면적 (㎡) | `BigDecimal` | 예: `1500.50` |
| `siEcvtGrdtCd` | 비탈면경사도 | `String` | 예: 비탈면경사도구분코드(`"1"`) |

#### 부속물 가입금액 산출

| 항목 (Property) | 설명 | 데이터 타입 | 비고 / 예시 |
| :--- | :--- | :--- | :--- |
| `joinYr` | 가입년도 | `String` | YYYY (예: `"2026"`) |
| `acqsDte` | 취득일자 | `String` | YYYYMMDD(예: `"20260803"`) |
| `acqsUntprc` | 취득단가 | `BigDecimal` | 예: `"24,252"` |
| `acqsQty` | 취득수량 | `int` | 예: `"211"` |


### 출력 (Output)

| 항목 (Property) | 설명 | 데이터 타입 | 산출 방식 |
| :--- | :--- | :--- | :--- |
| `adjtMuaJoinAmt` | 가입금액 | `BigDecimal` | 비탈면, 부속물 각각의 산출식에 따른 가입금액 |

---

## 3. 부속물 공제회비 계산 Method (`selectFunctionAdjtMuaMbfeeAmt`)

| 클래스/파일명 | 메소드명 | 입력 타입 | 출력 타입 |
| :--- | :--- | :--- | :--- |
| `AdjtServiceImpl` | `selectFunctionAdjtMuaMbfeeAmt` | `PMSCOMVO` | `BigDecimal` |

### 입력 (Input)

| 항목 (Property) | 설명 | 데이터 타입 | 비고 / 예시 |
| :--- | :--- | :--- | :--- |
| `mbrNo` | 회원번호 | `String` | 예: `"M0000"` |
| `joinYr` | 가입년도 | `String` | YYYY (예: `"2026"`) |
| `muaJoinSqno` | 공제가입순번 | `int` | 예: `1` |
| `schlNo` | 학교번호 | `String` | 예: `"S00000"` |
| `schlJoinSqno` | 학교가입순번 | `int` | 예: `1` |
| `siAdjtSeCd` | 부속물구분코드 | `String` | (1:부속물 3:비탈면) 예: `"1"` |



### 출력 (Output)

| 항목 (Property) | 설명 | 데이터 타입 | 산출 방식 |
| :--- | :--- | :--- | :--- |
| `adjtMuaMbfeeAmt` | 공제회비 | `BigDecimal` | 비탈면, 부속물 각각의 산출식에 따른 공제회비 |

---

## 참조 SQL

```SQL
  /*연도별 부속물 월가입요율 및 단가조회*/
  SELECT *
    FROM TB_MA_ADJT_MUA_FRT_I
    WHERE MAS_NO='1'
      AND APLCN_BGNG_DTE <= '가입년도' || '1231'
      
  /*연도별 부속물 월환급요율 조회*/
  SELECT *
    FROM TB_MA_ADJT_RMBR_FRT_I
    WHERE MAS_NO='1'
      AND APLCN_BGNG_DTE <= '가입년도' || '1231'
```