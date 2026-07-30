# SQL 작성 가이드

## Comment

- 주석(comment)은 개발자가 작성한 Query의 이해를 돕는 설명이나 디버깅을 위해 작성합니다.

---

### Query Description

- Query XML의 주석은 <!-- 로 시작하여 --> 로 끝납니다. Query에 대한 주석은 다음과 같은 정보를 포함합니다:
    - 설명: 쿼리가 처리하는 업무를 다른 개발자들이 이해할 수 있는 수준으로 간단 명료하게 작성합니다.
    - 작성일자: 쿼리를 작성한 일자를 기록합니다. (yyyy.mm.dd)
    - 작성자: 해당 쿼리를 작성한 사람의 이름을 입력

``` JAVA

xmlCopy code
<!--
    설명     : 건물 목록을 조회하는 쿼리입니다.
    작성일자 : 2026.07.28
    작성자   : 땡땡땡
-->
<select id="selectBldg" resultType="bldgDto">
    ...
    ...
    ...
</select>

```

---

### Query Inline Comment

- XML Query 내의 주석은 /* 로 시작하여 */ 로 끝납니다. Query 내의 주석은 다른 개발자들이 해당 쿼리를 이해할 수 있도록 comment를 남기기 위해 사용합니다. 
- 실행 쿼리 아이디를 주석으로 남깁니다. 아이디는 확장자를 제외한 xml 파일명 + ‘.’ + Query id를 사용합니다.

``` JAVA

xmlCopy code
<select id="selectSample" resultType="SampleEntity">
    SELECT /* SampleMapper.selectSample */
           seq
         , title
    FROM master_sample
</select>

```