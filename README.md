# idea

리서치·기획 아이디어 아카이브.

## 폴더 구조

| 폴더 | 용도 |
| --- | --- |
| [`research DB/`](./research%20DB) | AI 딥리서치(Deep Research) 산출물 모음 |
| [`proposal/`](./proposal) | 프로젝트 기획서(제안서) 초안 및 버전 관리 |

---

## 진행 중인 프로젝트

### 토큰증권 Product Governance Copilot

> AI 기능 / 신규 서비스 / 금융권 AX 업무자동화

**한 줄 정의:** 토큰증권 상품 출시 과정에서 상품 구조와 최신 규제·내부정책을 사전 대조하여 누락정보·규제 쟁점·검토 필요사항을 근거와 함께 식별하고 관련 reviewer에게 연결함으로써, 후행 규제검토에서 발생하는 보완·재작업을 줄이는 **Human-in-the-loop Product Governance Copilot**.

**관련 문서**
- 기획서: [`proposal/Copilot_STO_v1.md`](./proposal/Copilot_STO_v1.md) (v0.1, Working Draft)
- 배경 리서치: [`research DB/토큰증권(STO) 발행유통 프로세스와 해외 페인포인트 분석.md`](<./research DB/토큰증권(STO) 발행유통 프로세스와 해외 페인포인트 분석.md>)

**전체 진행률: 1/8 마일스톤 완료 (약 12%)**

`[■□□□□□□□]`

| # | 단계 | 산출물 | 상태 |
| --- | --- | --- | --- |
| 1 | Background + Evidence Map | Background & Problem, Evidence Map v0.1 | ✅ 완료 |
| 2 | AS-IS Workflow 조사 | 토큰증권 출시 AS-IS Workflow | 🔵 Next |
| 3 | Pain Evidence 정리 | Actor별 JTBD / Pain Evidence Map | ⬜ 예정 |
| 4 | 경쟁/대체재 분석 | 기존 대체수단·GRC·Legal AI 경쟁분석 | ⬜ 예정 |
| 5 | 검증 설계 | 실무자 인터뷰 설계 및 검증 | ⬜ 예정 |
| 6 | MVP 재확정 | MVP 상세 Scope 재확정 | ⬜ 예정 |
| 7 | PoC 설계 | Prototype + Golden Set PoC 설계 | ⬜ 예정 |
| 8 | KPI 확정 | KPI baseline 및 success threshold 설정 | ⬜ 예정 |

**기획서 목차 (v0.1 기준)**

- 0. Project Definition
- 1. Background & Problem
  - 1.1 Background · 1.2 Evidence · 1.3 Problem Statement · 1.4 Existing Solutions & Market Gap · 1.5 Focus Problem
- 2. Target & Usage Context
  - 2.1 Core Target · 2.2 Usage Context · 2.3 Platform / Channel
- 3. Project Goal & Success Criteria
  - 3.1 Project Goal · 3.2 Success Criteria · 3.3 Key Assumptions
- 4. Solution Direction
  - 4.1 As-is · 4.2 Solution Principle · 4.3 To-be
- 5. MVP Scope
  - 5.1 In Scope · 5.2 Out of Scope · 5.3 Feature Requirements (F-01~F-06)
- 6. End-to-End User Flow
  - 6.1 Main Flow · 6.2 Exception Flow · 6.3 Actor & Responsibility
- 7. Value & Business Logic
  - 7.1 Value Proposition · 7.2 Impact Chain · 7.3 Business Model
- 8. KPI & Measurement
  - 8.1 Primary Metric · 8.2 Driver Metrics · 8.3 Guardrail Metrics · 8.4 Event Instrumentation
- 9. Validation Plan
  - 9.1 Riskiest Assumption · 9.2 Validation Method · 9.3 Experiment Card · 9.4 Decision Rule
- 10. Risk & Compliance
  - 10.1 Common Risk · 10.2 AI / Model Risk · 10.3 Legal / Compliance
- 11. Execution Plan & Open Issues
  - 11.1 Milestones · 11.2 Open Questions · 11.3 Decision Log
- 12. AI Utilization Log
- Appendix A. Evidence Map Snapshot
- Appendix B. 내일 바로 재개할 지점
- Appendix C. 한 문장 요약

---

### 미래지출 결제설계 서비스

> 신규 핀테크 서비스 / 금융 의사결정 지원 *(Working Title: Planned Spend Payment Planner)*

**한 줄 정의:** 사용자의 현재 소비와 향후 고액지출 계획을 함께 분석하여, 보유 카드와 신규 카드 후보·할부·혜택 조건·결제시점을 비교하고 각 예정 지출을 무엇으로 어떻게 결제할지 사전에 설계하도록 돕는 서비스.

**관련 문서**
- 기획서: [`proposal/미래지출 결제설계 서비스 기획서 v0.1.md`](<./proposal/미래지출 결제설계 서비스 기획서 v0.1.md>) (v0.1, Working Draft)

**전체 진행률: 0/7 마일스톤 완료 (0%)**

`[□□□□□□□]`

| # | 단계 | 목적 | 상태 |
| --- | --- | --- | --- |
| 1 | Porter's Five Forces | 산업 경계와 구조적 매력도 검증 | 🔵 Next |
| 2 | Value Chain | 가치가 발생·누수되는 활동과 참여자 분석 | ⬜ 예정 |
| 3 | KSF | 이 시장에서 반드시 잘해야 할 조건 도출 | ⬜ 예정 |
| 4 | TAM-SAM-SOM + Market Segment Map | 시장 규모와 유망 Segment 구조화 | ⬜ 예정 |
| 5 | Persona Spectrum + CJM | 실제 고객군과 구매·결제 과정 구조화 | ⬜ 예정 |
| 6 | Opportunity Score | 우선 해결할 Pain/Segment 수렴 | ⬜ 예정 |
| 7 | JTBD | 최종 고객 Job과 진짜 전환 Trigger 검증 | ⬜ 예정 |

**기획서 목차 (v0.1 기준)**

- 0. Project Definition
- 1. Background & Problem
  - 1.1 Background · 1.2 Evidence · 1.3 Problem Statement · 1.4 Focus Problem
- 2. Target & Usage Context
  - 2.1 Core Target · 2.2 Usage Context · 2.3 Platform / Channel
- 3. Project Goal & Success Criteria
  - 3.1 Project Goal · 3.2 Success Criteria · 3.3 Key Assumptions
- 4. Solution Direction
  - 4.1 As-is · 4.2 Solution Principle · 4.3 To-be
- 5. MVP Scope
  - 5.1 In Scope · 5.2 Out of Scope
- 6. End-to-End User Flow
  - 6.1 Main Flow · 6.2 예산 변경 Scenario · 6.3 Recommendation 이후 Future Card Design
- 7. Value & Business Logic
  - 7.1 Value Proposition · 7.2 Business Model
- 8. KPI & Measurement
  - 8.1 Primary Metric · 8.2 Driver Metrics · 8.3 Guardrail
- 9. Validation Plan
  - 9.1 Riskiest Assumption · 9.2 Validation Method
- 10. Risk & Compliance
  - 10.1 Common Risk · 10.2 AI / Model Risk · 10.3 Legal / Compliance
- 11. Execution Plan & Open Issues
  - 11.1 분석 Milestone · 11.2 Open Questions · 11.3 현재 Decision Log
- 12. AI Utilization Log

---

> 상태 표기: **[FACT]** 확인된 사실 · **[INFERENCE]** 합리적 추론 · **[HYPOTHESIS]** 검증 필요 가설 · **[TBD]** 미조사/미결정
