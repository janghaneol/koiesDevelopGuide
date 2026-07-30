# 교육시설공제 업무 Wiki

<div class="hero" markdown>

## NGMA Documentation
교육시설공제 업무 시스템의 아키텍처 · 업무 도메인 · 계산 정책 · 개발 규칙을 관리합니다.
</div>


---

## 📚 업무 영역


<div class="grid cards" markdown>

-   :material-code-braces:{ .lg .middle } **Development**

    ---

    개발 표준 및 운영 규칙입니다.

    **개발 문서**

    - 개발 표준 가이드
    - SQL 작성 가이드

    [:octicons-arrow-right-24: 개발 규칙](Convention/CodingConvention.md)

-   :material-sitemap:{ .lg .middle } **Architecture**

    ---

    시스템 구조와 업무 흐름을 관리합니다.

    **포함 문서**

    - 시스템 아키텍처
    - 업무 흐름

    [:octicons-arrow-right-24: 문서 보기](Architecture/Architecture.md)


-   :material-package-variant-closed:{ .lg .middle } **Domain**

    ---

    교육시설공제 핵심 업무 영역입니다.

    **주요 도메인**

    - 일반건물
    - 고가건물
    - 물품
    - 부속물
    - 배상책임
    - 전기위험

    [:octicons-arrow-right-24: Domain 보기](Domain/Building/)


-   :material-file-document-check:{ .lg .middle } **Business Rule**

    ---

    업무 계산 기준과 정책을 관리합니다.

    **주요 정책**

    - 회비 계산
    - 할인 정책
    - 반액 처리

    [:octicons-arrow-right-24: 정책 보기](Policy.md)


</div>


---

## 🚀 변경 이력

--8<-- "History/latest.md"

---

## 🔗 Quick Links


<div class="grid" markdown>


[:material-database-search: SQL Convention](Convention/SqlConvention.md)


[:material-code-tags: Coding Convention](Convention/CodingConvention.md)


[:material-file-tree: Business Flow](Architecture/BusinessFlow.md)


</div>


---

## 🏗 System Stack


| 영역 | 기술 |
|---|---|
| Frontend | Nexacro |
| Backend | Spring Boot |
| Persistence | MyBatis |
| Database | Oracle |
| Build | Maven |
| Deployment | Jenkins |


---

<div class="footer-note" markdown>

**NGMA Wiki**

교육시설공제 업무 시스템 개발 문서

Last Updated : 2026-07

</div>