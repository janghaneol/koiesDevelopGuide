# 개발 표준 가이드

## 개요

최초배포(2026.07.28 장한얼)

### 목적

- 개발 표준 가이드는 프로그래밍 시 지켜야 할 형식적인 규칙을 정의하고, Coding Style을 표준화 하여 제공함으로써 향후 효율적인 프로그램 유지 보수와 가독성을 최대화 하고, 모든 개발자가 상호 간 Code를 읽고 이해하기 쉽게 함으로써 그에 따른 비용을 최소화 할 수 있다.
  
### 범위

- 본 문서가 배포되는 날짜(2026.07.28 작성중) 이후의 신규 개발되는 시스템을 범위로 하며, 기존 프로그램은 해당 양식에 맞게 변환

---

## Naming Rule 가이드

### Naming 표기법

#### 기본 Naming Rule

- 이해가 가능한 Full English Description 방식을 사용합니다.
- 독립어나 두 단어가 조합될 경우 두 번째 명사의 시작 문자는 대문자로 시작합니다.
- 상수는 영문 대문자 스네이크 표기법을 사용한다. ex) CONTENT_MANAGEMENT
- 변수, 함수에는 카멜 표기법을 사용한다.
 
---

## Java Programming Naming Rule

### Package

- Package 명은 반드시 소문자만 사용합니다.
- Package를 정의할 때는 레벨화하여 명명함을 기본으로 합니다.
- Class 이름은 간단하고 명시적으로 작성합니다.
- Class 이름은 각 단어를 대문자로 표기하는 PascalCase로 작성합니다.

---

### Method

- 일반적으로 Method는 클래스의 여러 가지 행위를 나타내는 것이기 때문에 첫 단어는 동사로 시작합니다.
- 동사만으로 의미 전달이 불명확한 경우에는 동사 + 명사 형태로 표기합니다.
- CamelCase로 작성합니다.
  
| Method명칭 | 설명 |
|---|---|
| getMethod | – 특정 상세 조회 <br> – 특정 Entity / Field의 값을 설정 |
| setMethod | 특정 Entity / Field의 값을 설정 |
| selectMethod | 목록 조회 |
| insertMethod | 데이터 등록 (Insert Transaction) |
| deleteMethod | 데이터 삭제 (Delete Transaction) |
| updateMethod | 데이터 업데이트 (Update Transaction) |
| isMethod | 특정 속성 여부 검사 |
| hasMethod | 특정 속성 소유 검사 |

---

## 변수

- 변수 이름을 정의할 때는 약어 사용은 자제하며, 되도록 변수명만 보고 의미를 알 수 있도록 단어 그대로 사용하는 것을 권장합니다.
- CamelCase로 작성합니다.
- 첫 글자는 밑줄(_)이나 달러 문자로 ($) 시작하지 않습니다.

---

## 상수

- 상수 선언은 반드시 "static final"을 사용합니다.
- 상수는 전부 대문자 스네이크 표기법으로 표기합니다.
- 단어와 단어 사이는 밑줄로 (_) 연결합니다.
- 누구나 이해할 수 있는 영문 이름을 사용합니다.
- 첫 글자는 밑줄(_)이나 달러 문자로 ($) 시작하지 않습니다.

---

## Mapping XML

- Map XML 파일은 기본적으로 Mapper 인터페이스당 하나를 생성하도록 합니다.
- 파일명은 "Mapper" 접미사를 사용하여 인터페이스와 XML 파일을 동일하게 생성합니다. (예: MasterSampleMapper.java > MasterSampleMapper.xml)
- 확장자는 "xml"만 사용합니다.