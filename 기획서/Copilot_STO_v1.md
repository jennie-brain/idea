# 토큰증권 Product Governance Copilot 기획서 v0.1

> **작성 목적**  
> 2026-08-13까지의 조사·논의를 기준으로 현재까지 확정된 사실, 합리적 추론, 검증이 필요한 가설을 구분해 기록한다.  
> 이 문서는 완성된 사업계획서가 아니라 **Problem Discovery 및 MVP 가설 수립 단계의 Working Draft**다.
>
> **상태 표기**
> - **[FACT]** 공개 1차 자료 등으로 현재 확인된 사실
> - **[INFERENCE]** 확인된 사실을 바탕으로 한 합리적 추론
> - **[HYPOTHESIS]** 사용자 인터뷰·업무관찰·PoC 등 추가 검증이 필요한 가설
> - **[TBD]** 아직 조사하지 않았거나 결론을 유보한 항목

---

# 0. Project Definition

- **프로젝트명:** Token Securities Product Governance Copilot
- **프로젝트 유형:** AI 기능 / 신규 서비스 / 금융권 AX 업무자동화
- **한 줄 정의:**  
  토큰증권 상품 출시 과정에서 상품 구조와 최신 규제·내부정책을 사전 대조하여 누락정보, 규제 쟁점과 검토 필요사항을 근거와 함께 식별하고 관련 reviewer에게 연결함으로써, 후행 규제검토에서 발생하는 보완·재작업을 줄이는 **Human-in-the-loop Product Governance Copilot**
- **기획 기준일:** 2026-08-13
- **작성자 / 팀:** JENNIE / AI-PM-study

> **상위 Product Vision**
>
> 토큰증권 전용 도구 자체를 최종 제품으로 보지 않는다. 장기적으로는 **복잡한 금융상품의 기획·출시·변경 과정에서 규제, 내부정책, 상품구조, 운영요건을 연결하고 누락·리스크·검토사항을 식별해 인간의 의사결정을 지원하는 Product Governance Copilot**을 지향한다.
>
> 토큰증권은 규제 변화, 다부서 검토, 증권 규율과 기술·인프라 규율의 결합이 동시에 나타나는 영역이므로 **Initial Vertical / MVP Testbed**로 설정한다.

---

# 1. Background & Problem

## 1.1 Background

- **이 프로젝트를 검토하게 된 계기:**
  - **[FACT]** 금융권에서는 생성형 AI를 넘어 AI Agent를 내부 분석, 리스크 분석, 의사결정 보조 등 업무에 활용하려는 AX 전환이 진행되고 있다.
  - **[INFERENCE]** 금융상품의 기획·출시·변경과 같은 지식집약적 통제 업무도 향후 AI-assisted workflow의 주요 적용 대상이 될 가능성이 높다.
  - **[HYPOTHESIS]** 특히 규제와 내부정책을 지속적으로 확인하고 여러 reviewer가 참여하는 Product Governance 업무는 Copilot 적용 가치가 클 수 있다.

- **현재 시장 / 산업 상황:**
  - **[FACT]** 국내 토큰증권 제도화 관련 법률은 2026년 1월 국회를 통과했으며 2027년 2월 4일 시행 예정이다.
  - **[FACT]** 토큰증권은 자본시장법상 '증권'의 성격을 유지하면서 분산원장 기반의 발행·관리·유통 인프라가 결합되는 구조다.
  - **[FACT]** 금융당국은 2026년 토큰증권 협의체를 기술·인프라, 발행, 유통, 결제 영역으로 나누어 세부 제도와 운영 기준을 논의하고 있다.
  - **[FACT]** 2026년 5월 기준 기초자산 적격성, 증권신고서 공시, 조각투자 발행 모범규준, 기존 증권 토큰화, 온체인 결제, 장외거래소 인가, 겸영범위, 거래한도 등이 세부 논의 대상이었다.
  - **[INFERENCE]** 이는 상품 하나를 검토할 때 단일 법령 검색만으로 끝나기보다, 상품 구조에 따라 발행·공시·유통·투자자보호·기술/인프라 규율을 연결해 해석해야 할 가능성이 높다는 것을 의미한다.

- **주요 시장 규모 및 성장 추세:**
  - **[TBD]** 현 단계에서 시장규모는 핵심 Problem Evidence가 아니므로 우선순위를 낮춘다.
  - **[주의]** STO 시장 성장 전망을 MVP 선택의 주된 근거로 사용하지 않는다.

- **관련 산업·기술·정책·사용자 행동 변화:**
  - **[FACT]** 금융위원회는 2026년 금융권 AX 논의에서 AI Agent 활용 확대와 관련 테스트·제도 정비 방향을 제시했다.
  - **[FACT]** 금융분야 AI 원칙은 현 단계의 AI를 업무 보조수단으로 보고, 최종 의사결정과 책임을 임직원에게 두며 인적 개입, 신뢰성, 합법성, 보안 등을 강조한다.
  - **[INFERENCE]** 따라서 규제·리스크가 큰 금융상품 업무에서는 완전자동화보다 `AI Assistance → Human Review → Human Decision` 구조가 제도 방향과 더 정합적이다.

- **관련 사업 / 서비스 맥락:**
  - 기존 규제 대응 방식은 법령·가이드라인·사례·내부정책을 담당자가 조회하고, 상품기획·법무·준법·리스크·운영 등 관계부서가 검토하는 구조로 추정된다.
  - **[FACT]** 투자계약증권 초기 발행 과정에서 투자자보호 관련 주요 항목 기재가 미흡해 신고서 정정이 반복되고 발행 일정이 지연된 사례를 금융감독원이 공식적으로 확인했다.
  - **[FACT]** 이에 대한 감독당국의 주요 해결책은 작성 원칙, 모범규준, 작성예시, 정정요구 사례 등의 제공이었다.
  - **[HYPOTHESIS]** 이러한 현재 방식에는 규제 적용 판단, 누락정보 탐지, reviewer routing, 근거 기록을 더 앞단에서 구조화할 automation opportunity가 존재한다.

- **Why Now — 지금 검토해야 하는 이유:**
  1. **[FACT]** 금융권 AX와 AI Agent 도입이 정책·산업 차원에서 본격화되고 있다.
  2. **[FACT]** 토큰증권은 2027년 제도 시행을 앞두고 세부 규율과 운영방식이 계속 정비되는 과도기다.
  3. **[FACT]** 인접한 투자계약증권 발행에서 기재 미흡 → 정정 반복 → 발행 지연이라는 실제 regulatory rework가 확인됐다.
  4. **[INFERENCE]** 토큰증권은 '변화하는 규제를 실제 상품 의사결정과 운영행동으로 변환하는 능력'을 검증하기 좋은 초기 vertical이다.
  5. **[INFERENCE]** 금융상품 전반을 한 번에 다루기보다 토큰증권으로 좁혀 Product Governance Copilot의 핵심 원리와 통제설계를 검증하는 것이 MVP 관점에서 합리적이다.

## 1.2 Evidence

| ID | 근거 유형 | 출처 | 확인된 사실 | 신뢰도 |
| --- | --- | --- | --- | --- |
| E-01 | 정부 정책 / 1차 자료 | 금융위원회, 「정부와 금융권이 함께 금융권 AX를 가속화…」, 2026-06-18 | 금융회사들이 생성형 AI를 넘어 AI Agent를 고객정보 분석, 리스크·데이터 분석, 의사결정 보조 등에 활용하고 있으며 금융당국도 AI Agent 테스트 및 제도 정비를 추진 | High |
| E-02 | 정부 가이드라인 / 1차 자료 | 금융위원회, 2026 금융분야 AI 관련 원칙 | AI는 현 단계에서 업무 보조수단이며 최종 의사결정과 책임은 임직원에게 있고, 인적 개입·합법성·신뢰성·보안 등을 요구 | High |
| E-03 | 법·정책 / 1차 자료 | 금융위원회, 토큰증권 제도화 법안 국회 통과 자료, 2026-01 | 토큰증권 관련 제도화 법률이 통과되었고 2027-02-04 시행 예정 | High |
| E-04 | 정책 운영 / 1차 자료 | 금융위원회, 토큰증권 협의체 Kick-off, 2026-03 | 토큰증권 제도·실무 논의를 기술·인프라 / 발행 / 유통 / 결제 4개 축으로 구성 | High |
| E-05 | 정책 운영 / 1차 자료 | 금융위원회, 토큰증권 협의체 2차 회의, 2026-05 | 기초자산, 공시, 모범규준, 기존 증권 토큰화, 온체인 결제, 장외거래소 인가, 겸영범위, 거래한도 등 세부 규율이 논의 중 | High |
| E-06 | 감독당국 문제 관찰 / 1차 자료 | 금융감독원, 투자계약증권 투자자보호 모범규준 관련 자료, 2024 | 초기 신고에서 주요 항목 기재 미흡으로 신고서 정정이 반복되고 발행 일정이 지연됐으며, 업계가 작성 원칙과 사례를 요청 | High |
| E-07 | 감독당국 대체수단 / 1차 자료 | 금융감독원 DART 공시업무 가이드 | 신고·공시 업무 지원을 위해 작성지침, 사례, 정정요구 관련 자료 등을 제공 | High |
| E-08 | 내부 workflow 정량 근거 | 공개자료 미확보 | 증권사 내부의 검토시간, 부서간 handoff 횟수, 재작업 빈도, 인건비 등은 현재 공개근거로 확인하지 못함 | Low / Not Verified |

### 1차 출처 링크

- 금융위원회 금융권 AX 자료: https://www.fsc.go.kr/po010101/87142
- 금융위원회 토큰증권 제도화 관련 자료: https://www.fsc.go.kr/no010101/86064
- 금융위원회 토큰증권 협의체 관련 자료: https://www.fsc.go.kr/no010101/86371
- 금융위원회 토큰증권 협의체 2차 회의 관련 자료: https://www.fsc.go.kr/no010101/86906
- 금융감독원 투자계약증권 투자자보호 모범규준 관련 자료: https://dart.fss.or.kr/dsaa003/selectBodoMain.ax?seqno=26541
- 금융감독원 DART 공시업무 가이드: https://dart.fss.or.kr/info/searchGuide02.do

## 1.3 Problem Statement

> **현재는 최종 Problem Statement가 아니라 검증 중인 Working Problem Statement다.**

| ID | 사용자 | 상황 | 목표 | 구조적 문제 | 손실·실패·불편 | 관련 Evidence ID |
| --- | --- | --- | --- | --- | --- | --- |
| P-01 | 토큰증권/신규 금융상품 기획·신사업 담당자 | 신규 상품을 설계하고 출시 전 검토를 준비할 때 | 출시 가능 구조와 필요한 검토사항을 빠짐없이 정리해 관련 부서와 검토를 진행 | 상품 구조에 적용되는 규제·가이드·내부정책을 연결하고 최신성·적용 여부를 판단해야 함 | **[HYPOTHESIS]** 누락, 반복 확인, reviewer 의존, 검토 지연 | E-03, E-04, E-05, E-08 |
| P-02 | 법무·준법·리스크 등 reviewer | 상품기획안/신고자료를 검토할 때 | 중요 리스크와 누락사항을 조기에 발견하고 판단근거를 남김 | 검토자료의 완결성과 규제 mapping이 앞단에서 충분히 구조화되지 않을 수 있음 | **[FACT+HYPOTHESIS]** 인접 투자계약증권에서는 기재 미흡→정정 반복→발행 지연이 확인됨. 증권사 내부 빈도·강도는 미검증 | E-06, E-08 |
| P-03 | 상품 출시 조직 전체 | 규제 변경 또는 신규 가이드라인이 발생할 때 | 변경사항이 자사 상품·운영에 미치는 영향을 빠르게 판단하고 필요한 action을 실행 | `Regulatory Change → Product Impact → Operational Action` 연결이 사람의 해석과 부서간 handoff에 의존할 가능성 | **[HYPOTHESIS]** 적용 누락, 영향분석 지연, 중복 검토, audit trail 분산 | E-01, E-02, E-05, E-08 |

권장 Working Problem Statement:

> **토큰증권 등 규제 변화가 큰 신규 금융상품을 기획·출시하는 담당자가 상품 구조와 최신 규제·내부정책을 대조해 출시 전 검토를 준비할 때, 적용 규칙·누락정보·부서별 확인사항을 구조화하고 연결해야 하는 복합적인 검토 업무 때문에 후행 reviewer 단계에서 보완·재작업과 검토 지연이 발생할 가능성이 있다.**

- **문제의 빈도:** **[TBD / 인터뷰 필요]**
- **문제의 심각도:** 인접 투자계약증권 신고에서 발행 일정 지연은 확인됨. 증권사 내부 영향 수준은 **[TBD]**
- **현재 사용자의 대체 행동 / 대체재:**
  - 법령·감독규정·가이드라인 조회
  - 금융감독원/금융위원회 모범규준 및 사례 활용
  - 내부 법무·준법·리스크 검토
  - 문서/메일/회의 기반 handoff **[HYPOTHESIS, 확인 필요]**
  - 기존 GRC / 법률정보 DB / 사내 검색시스템 활용 여부 **[TBD]**

## 1.4 Existing Solutions & Market Gap

### 현재 사용자 대체 행동

1. 규정·가이드라인을 담당자가 직접 조회
2. 과거 사례·모범규준·정정요구 사례 참고
3. 법무·준법·리스크 등 관계부서에 검토 요청
4. reviewer가 누락 또는 쟁점을 발견하면 보완
5. 반복 검토 후 승인·신고·출시

> 3~5단계의 실제 세부 프로세스는 공개자료가 부족하므로 **인터뷰로 검증해야 한다.**

### 기존 서비스/경쟁사

- **[TBD]** 국내 법률정보 DB
- **[TBD]** 금융회사 내부 GRC / 규제관리 솔루션
- **[TBD]** Legal AI / Regulatory Intelligence 솔루션
- **[TBD]** Workflow / Document Management System
- **[TBD]** 글로벌 RegTech / Product Governance 제품

### 해결되는 부분

- 규정 검색
- 가이드 및 사례 제공
- 문서관리
- 일부 workflow / 승인관리

### 해결되지 않는 부분 — 현재 가설

- **[HYPOTHESIS]** 특정 상품 구조에 어떤 규칙이 실제 적용되는지 자동 mapping
- **[HYPOTHESIS]** 제출·검토 전 누락정보 및 불명확 사항 선제 식별
- **[HYPOTHESIS]** 이슈별 reviewer 자동 routing
- **[HYPOTHESIS]** 규제 변경이 기존 상품·운영에 미치는 영향분석
- **[HYPOTHESIS]** 근거, 규정 버전, 시행일, reviewer 판단을 하나의 audit trail로 연결

### 왜 문제가 지속되는가 — 현재 가설

- 규제와 상품 정보가 비정형 문서로 분산
- 규칙의 적용 여부에 맥락적 판단이 필요
- 법규·가이드·내부정책의 버전과 시행시점 관리 필요
- 여러 조직의 전문성이 동시에 필요
- 최종 판단은 AI에 위임하기 어려워 human control이 필수

## 1.5 Focus Problem

이번 프로젝트에서 우선 해결할 문제:

- **[대상 Problem ID: P-01]**
- **[대상 Problem ID: P-02]**

선정 근거:
1. 투자계약증권에서 `기재 미흡 → 정정 반복 → 발행 지연`이라는 실제 downstream rework가 공개적으로 확인됐다.
2. 토큰증권은 제도 시행 전 세부규율이 지속적으로 정비되는 영역이어서 최신 규칙과 상품 구조의 연결 문제가 두드러질 가능성이 높다.
3. 규제 답변 챗봇보다 `사전검토 → 누락 탐지 → reviewer 연결 → 근거 기록`의 workflow가 문제·성과지표·Human-in-the-loop 구조를 더 명확히 정의할 수 있다.

이번에 다루지 않는 문제:

| Problem ID | 제외 이유 |
| --- | --- |
| P-03 전체 | Regulatory Change Management 전체를 MVP에 포함하면 범위가 과도하게 넓어짐. 초기 MVP에서는 '신규 토큰증권 상품 출시 전 사전검토'에 집중하고 향후 확장 검토 |
| 신규 금융상품 전체 | 규칙과 상품 유형의 범위가 지나치게 넓어 MVP 검증이 어려움. 토큰증권 vertical로 우선 검증 |
| 자동 법률판단 / 자동 출시승인 | 금융권 AI의 책임·통제 원칙과 상충 가능성이 높고, 치명적 false negative 위험이 큼 |

---

# 2. Target & Usage Context

## 2.1 Core Target

- **핵심 사용자:**  
  **1차 가설:** 증권사/금융회사 내 토큰증권·디지털자산·신사업·상품기획 담당 PM/실무자  
  **주요 reviewer:** 준법감시, 법무, 리스크, 운영, IT/보안 담당자

- **사용자 특성:**
  - 신규 금융상품 구조와 사업모델을 설계
  - 외부 법규와 내부 정책을 동시에 고려
  - 여러 전문부서와 협업해 출시 의사결정을 준비
  - 판단 근거와 승인 이력을 남겨야 할 가능성이 높음

- **현재 행동:** **[TBD / 인터뷰 필요]**
  - 규제 조회
  - 과거 사례·모범규준 참고
  - 사내 reviewer에 검토 요청
  - 수정·보완 후 재검토

- **주요 니즈 — 가설:**
  1. 상품 구조에 적용되는 규칙을 빠르게 식별
  2. 검토 전 누락정보를 발견
  3. 어떤 부서가 무엇을 확인해야 하는지 명확히 분리
  4. 모든 AI 제안의 근거·출처·시행일·버전을 확인
  5. 최종 판단은 담당 reviewer가 유지

- **제외 사용자:**
  - 개인투자자
  - 단순 투자정보 탐색 사용자
  - 일반 법률 Q&A 사용자
  - 자동투자/자동매매 목적 사용자

## 2.2 Usage Context

- **When:** 신규 토큰증권 상품의 구조를 설계하거나 출시 전 사전검토를 준비할 때
- **Where:** 금융회사 내부 업무환경 / B2B Web / 사내 시스템
- **Trigger:**
  - 신규 상품기획안 작성
  - 기초자산 또는 증권 구조 변경
  - 발행·유통 방식 변경
  - reviewer 검토 전 pre-check
  - **향후:** 관련 규제·가이드 변경
- **Goal:** 후행 reviewer가 발견할 수 있는 누락·쟁점을 더 앞단에서 식별하고, 검토에 필요한 evidence와 task를 구조화
- **Constraint:**
  - 규정 최신성 및 시행일
  - 내부기밀 상품정보
  - 개인정보·보안
  - 법률 판단의 불확실성
  - hallucination / false negative
  - 사내 시스템 접근권한
  - human approval 필요

## 2.3 Platform / Channel

- **App / Web / Admin / Offline / B2B 등:** B2B Internal Web / 금융회사 내부 업무시스템 연계
- **주요 진입 채널:** **[TBD]**
  - 상품기획 시스템
  - 내부 GRC/준법 시스템
  - 문서 업로드 기반 독립 PoC
  - 향후 API/워크플로우 연계

---

# 3. Project Goal & Success Criteria

## 3.1 Project Goal

- **[대상 Problem ID: P-01, P-02]**
- **사용자 관점 목표:** reviewer에게 제출하기 전에 상품 구조, 적용 규칙, 누락정보, 검토 이슈를 근거와 함께 확인할 수 있게 한다.
- **사업 관점 목표:** **[현 단계에서는 외부 SaaS 매출보다 내부 AX/Product Governance 효율성 검증을 우선]**
- **운영 / 리스크 관점 목표:** AI가 최종 법률판단을 대신하지 않으면서 검토의 일관성, 근거추적성, auditability를 높인다.

> **핵심 성과 개념:** `Preventable Rework Reduction`

## 3.2 Success Criteria

| 구분 | 성공 기준 | 측정 방법 |
| --- | --- | --- |
| User | 사전검토 결과가 reviewer의 실제 검토 준비에 유용함 | 사용자 인터뷰, prototype test, reviewer 평가 |
| User | 검토 준비 및 first-pass review에 걸리는 시간을 감소 | 기존 workflow 대비 task completion time |
| Operation | downstream에서 발견되는 단순 누락/보완 항목 감소 | AI 사용 전후 rework count 비교 |
| Risk | 중요 규제 이슈의 false negative를 허용 임계치 이하로 통제 | Golden Set 기반 critical issue recall |
| Risk | 모든 주요 AI 출력에 확인 가능한 출처·조문·시행일·버전이 연결 | Evidence coverage / citation validity |
| Governance | 최종 승인·예외판단이 human reviewer에게 유지 | workflow audit log |

## 3.3 Key Assumptions

| ID | 가정 | 관련 Problem ID | 중요도 | 검증 필요 여부 |
| --- | --- | --- | --- | --- |
| A-01 | 토큰증권 상품 출시 전 검토에서 규제 확인·누락정보 보완·부서간 handoff가 유의미한 workload를 만든다 | P-01, P-02 | High | Yes |
| A-02 | downstream reviewer 단계에서 발견되는 문제 중 일부는 앞단의 구조화된 pre-review로 예방 가능하다 | P-02 | High | Yes |
| A-03 | 기존 법률DB/GRC/문서관리 도구만으로는 상품구조→적용규칙→검토과제 연결이 충분하지 않다 | P-01, P-02 | High | Yes |
| A-04 | LLM+Rule+Workflow+Evidence 구조가 단순 RAG 챗봇보다 해당 업무에 적합하다 | P-01, P-02 | High | Yes |
| A-05 | 사용자는 AI의 완전자동 판단보다 근거 기반 recommendation + human review 방식을 신뢰·수용한다 | P-01, P-02 | High | Yes |
| A-06 | 토큰증권 vertical에서 검증한 Product Governance 방식은 향후 다른 복잡한 금융상품으로 확장 가능하다 | P-01 | Mid | Yes |
| A-07 | 규정 버전·시행일·적용범위 관리가 실제 사용가치의 핵심 요소다 | P-01 | High | Yes |

---

# 4. Solution Direction

## 4.1 As-is

- **[대상 Problem ID: P-01, P-02]**

현재 사용자 흐름 — **Working Hypothesis**

```text
상품 아이디어/구조 설계
→ 관련 규제·가이드 조회
→ 내부 검토자료 작성
→ 법무/준법/리스크 등 reviewer 검토 요청
→ 누락·쟁점 발견
→ 수정/보완
→ 재검토
→ 승인
→ 신고/출시
```

문제가 발생하는 지점:

- **Step:** 규제·가이드 조회
  - **Pain:** 어떤 규칙이 해당 상품 구조에 적용되는지 판단 필요
  - **원인:** 규칙·상품정보가 여러 문서에 분산되고 맥락적 적용 판단 필요

- **Step:** reviewer 검토
  - **Pain:** 누락정보·쟁점이 늦게 발견될 경우 재작업 발생
  - **원인:** 앞단에서 상품구조와 요구사항이 충분히 mapping되지 않았을 가능성
  - **Evidence:** 투자계약증권 초기 신고에서 유사한 기재 미흡→정정 반복→발행 지연 확인

- **Step:** 수정/보완
  - **Pain:** 반복 검토와 일정 지연
  - **원인:** downstream 발견
  - **증권사 내부 빈도/시간:** **[TBD]**

## 4.2 Solution Principle

- **[대상 Problem ID: P-01, P-02]**
- **핵심 해결 원리:**  
  **Downstream reviewer가 뒤늦게 발견하던 누락·규제 쟁점을 상품 출시 workflow의 앞단에서 evidence-linked AI pre-review로 구조화해 발견하고, 최종 판단은 인간 reviewer에게 유지한다.**

- **보조 해결 원리:**
  1. 규제 검색이 아니라 `Product Structure → Applicable Rule → Requirement → Issue → Reviewer Task`로 연결
  2. 규칙마다 source / clause / effective date / version / applicability를 추적
  3. 명확한 hard rule은 Rule Engine, 비정형 문서 이해·설명은 LLM, routing·approval은 Workflow Engine으로 분리
  4. 모든 주요 판단 후보는 Human Review 대상으로 제공
  5. 최종 법률판단·예외승인·출시결정은 자동화하지 않음

## 4.3 To-be

개선 후 흐름:

```text
상품기획서/구조 입력
→ Product Structure Extraction
→ Applicable Rule Mapping
→ Requirement Check
→ Missing / Ambiguous Information Detection
→ Risk & Issue Flag
→ Reviewer Task Generation / Routing
→ Human Review
→ 수정/보완
→ Human Approval
→ Evidence + Decision Log
```

| Problem ID | Pain | 원인 | 변경 원리 | 기대 변화 |
| --- | --- | --- | --- | --- |
| P-01 | 적용 규칙·요건 탐색의 복잡성 | 상품정보와 규제가 분산 | 상품구조 기반 rule mapping | first-pass 검토 준비시간 감소 **[가설]** |
| P-02 | 누락·쟁점의 늦은 발견 | 앞단 pre-check 부족 | evidence-linked gap detection | preventable rework 감소 **[가설]** |
| P-02 | reviewer별 검토과제 불명확 | issue와 책임부서 연결 부족 | issue→reviewer task orchestration | handoff 명확화 **[가설]** |
| P-02 | 판단 근거 추적 어려움 | 문서/의사결정 분산 | evidence/version/decision log | auditability 향상 **[가설]** |

---

# 5. MVP Scope

> **현재 MVP Scope는 가설 단계이며, AS-IS workflow 인터뷰 후 확정한다.**

## 5.1 In Scope

| ID | 기능 | 대상 Problem ID | 관련 Assumption ID | MVP 포함 이유 | 우선순위 |
| --- | --- | --- | --- | --- | --- |
| F-01 | Product Structure Extraction | P-01 | A-02, A-04 | 비정형 상품기획서를 규제 검토 가능한 구조로 변환하는 첫 단계 | Must |
| F-02 | Applicable Rule & Evidence Mapping | P-01 | A-03, A-04, A-07 | 단순 검색이 아닌 상품구조→적용규칙 연결 검증 | Must |
| F-03 | Missing / Ambiguous Information Detection | P-02 | A-02, A-04 | preventable rework 감소 가설의 핵심 기능 | Must |
| F-04 | Review Issue & Task Generation | P-01, P-02 | A-01, A-02 | 누가 무엇을 검토해야 하는지 구조화 | Must |
| F-05 | Human Review / Override | P-01, P-02 | A-05 | 금융 AI의 Human-in-the-loop 원칙 및 책임통제 | Must |
| F-06 | Evidence / Version / Decision Log | P-02 | A-05, A-07 | 근거추적·감사·검증 가능성을 확보 | Must |

## 5.2 Out of Scope

| 기능 / 아이디어 | 제외 이유 | 추후 검토 시점 |
| --- | --- | --- |
| 모든 금융상품 지원 | MVP 검증범위가 과도하게 넓어짐 | 토큰증권 PoC 후 |
| AI의 최종 출시 가능/불가 법률판단 | 치명적 오류 및 책임 문제 | 원칙적으로 human decision 유지 |
| 자동 신고서 제출 | 문제검증보다 execution integration이 앞서는 기능 | 이후 단계 |
| B2G 감독당국 SupTech 버전 | 증권사 내부 사용자와 목표·workflow가 다름 | 별도 제품가설로 분리 |
| 규제 변경 자동 영향분석 전체 | 범위가 넓음 | Phase 2 |
| 온체인 거래/결제 기능 | Product Governance 문제와 직접 무관 | 별도 프로젝트 |

## 5.3 Feature Requirements

### F-01. Product Structure Extraction

- **[대상 Feature ID: F-01]**
- **[대상 Problem ID: P-01]**
- **[관련 Assumption ID: A-02, A-04]**
- **목적:** 비정형 상품기획 문서에서 규제검토에 필요한 구조화 필드를 추출
- **대상 사용자:** 토큰증권 상품기획자 / 신사업 담당자
- **Trigger:** 상품기획서 또는 구조정보 입력
- **Main Flow:** 문서 입력 → 정보 추출 → 사용자 확인/수정 → 구조화 spec 생성
- **Business Rule:** AI 추출값은 확정정보가 아니며 사용자가 확인 가능해야 함
- **Success State:** 필수 상품 구조 필드가 검토 가능한 형태로 구조화됨
- **Empty State:** 문서 없음 / 필수정보 없음
- **Error State:** 파싱 실패 / 불확실 정보
- **Permission / Eligibility:** 사내 권한 기반
- **필요 데이터:** 상품기획서, 상품구조 schema
- **로그 이벤트:** document_uploaded, structure_extracted, field_corrected
- **Acceptance Criteria:** **[TBD / Golden Set 필요]**

### F-02. Applicable Rule & Evidence Mapping

- **[대상 Feature ID: F-02]**
- **[대상 Problem ID: P-01]**
- **[관련 Assumption ID: A-03, A-04, A-07]**
- **목적:** 상품 구조와 관련 법령·감독규정·가이드·내부정책 후보를 연결
- **대상 사용자:** 상품기획자, 준법/법무 reviewer
- **Trigger:** 구조화된 상품 spec 생성
- **Main Flow:** product attributes → rule retrieval → applicability 후보 → evidence 표시 → human confirm
- **Business Rule:** 출처·조문·시행일·버전 없는 규제 판단은 확정 제안으로 표시하지 않음
- **Success State:** reviewer가 주요 적용 rule 후보와 근거를 검토 가능
- **Empty State:** 관련 rule 검색 결과 없음
- **Error State:** 상충 규정 / 구버전 / 적용범위 불명확
- **Permission / Eligibility:** 법규 KB / 내부정책 접근권한 필요
- **필요 데이터:** 법령, 감독규정, 가이드라인, 내부정책, version metadata
- **로그 이벤트:** rule_retrieved, evidence_opened, applicability_confirmed, rule_rejected
- **Acceptance Criteria:** **[TBD]**

### F-03. Missing / Ambiguous Information Detection

- **[대상 Feature ID: F-03]**
- **[대상 Problem ID: P-02]**
- **[관련 Assumption ID: A-02, A-04]**
- **목적:** 후행 검토에서 발견될 가능성이 있는 누락/불명확 정보를 사전 탐지
- **대상 사용자:** 상품기획자, reviewer
- **Trigger:** rule mapping 완료
- **Main Flow:** requirement → current evidence comparison → gap detection → severity 표시 → user/reviewer 확인
- **Business Rule:** critical issue는 자동 통과 불가
- **Success State:** 누락/불명확 후보가 근거와 함께 제시됨
- **Empty State:** 미발견
- **Error State:** false positive / false negative
- **Permission / Eligibility:** 관련 문서 및 규칙 접근권한
- **필요 데이터:** 상품 spec, 규정 requirement, 과거 검토 사례 **[가능 시]**
- **로그 이벤트:** gap_flagged, gap_confirmed, gap_dismissed, gap_resolved
- **Acceptance Criteria:** critical issue recall을 우선 평가 **[임계치 TBD]**

### F-04. Review Issue & Task Generation

- **[대상 Feature ID: F-04]**
- **[대상 Problem ID: P-01, P-02]**
- **[관련 Assumption ID: A-01, A-02]**
- **목적:** 발견된 issue를 검토 담당 역할과 확인과제로 변환
- **대상 사용자:** 상품기획자, 준법/법무/리스크/운영/IT·보안 reviewer
- **Trigger:** issue/gap 생성
- **Main Flow:** issue → reviewer role suggestion → task → 담당자 확인/수정 → 할당
- **Business Rule:** reviewer mapping은 조직별 R&R에 맞게 구성
- **Success State:** 모든 중요 issue에 owner와 review action이 지정
- **Acceptance Criteria:** **[TBD / 실제 조직 R&R 조사 필요]**

### F-05. Human Review / Override

- **[대상 Feature ID: F-05]**
- **[대상 Problem ID: P-01, P-02]**
- **[관련 Assumption ID: A-05]**
- **목적:** AI를 보조수단으로 제한하고 인간이 최종 판단·책임을 유지
- **Main Flow:** AI 제안 → reviewer 검토 → 승인 / 수정 / 반려 / 예외
- **Business Rule:** AI 단독 최종 승인 금지
- **Success State:** 최종 판단 주체와 근거가 명확히 기록됨

### F-06. Evidence / Version / Decision Log

- **[대상 Feature ID: F-06]**
- **[대상 Problem ID: P-02]**
- **[관련 Assumption ID: A-05, A-07]**
- **목적:** 규제 근거, 버전, 시행일, AI 제안, human decision을 연결해 추적
- **Business Rule:** superseded rule과 current rule을 구분
- **Success State:** 특정 결정이 어떤 정보·규정·reviewer 판단을 근거로 내려졌는지 재현 가능

---

# 6. End-to-End User Flow

## 6.1 Main Flow

- **[관련 Feature ID: F-01 ~ F-06]**

```text
상품기획 문서 입력
→ 상품 구조 추출·확인
→ 적용 규제 및 evidence mapping
→ requirement 대조
→ 누락·불명확 정보 탐지
→ 검토 issue 및 reviewer task 생성
→ human review
→ 수정 / 보완
→ human approval
→ decision & evidence log
```

## 6.2 Exception Flow

- **[관련 Feature ID: F-01 ~ F-06]**
- **실패:** 문서 파싱 실패, rule retrieval 실패, 내부자료 접근 실패
- **취소:** 사용자 사전검토 종료
- **재시도:** 문서 수정/추가 후 재분석
- **추가 정보 필요:** 누락필드 질의
- **운영자 개입:** KB 버전 오류, 규정 충돌, 모델 이상
- **외부 파트너 / API 장애:** **[TBD]**

## 6.3 Actor & Responsibility

| 단계 | 관련 Feature ID | 사용자 | 시스템 | 운영자 | 외부 파트너 |
| --- | --- | --- | --- | --- | --- |
| 상품정보 입력 | F-01 | 문서 제공·추출결과 확인 | 구조 추출 |  |  |
| Rule Mapping | F-02 | 적용 후보 검토 | 검색·mapping·근거표시 | KB 관리 | 법규/데이터 Source |
| Gap Detection | F-03 | gap 확인·보완 | 누락/불명확 후보 탐지 | 모델/규칙 운영 |  |
| Task Routing | F-04 | 담당자 확인 | reviewer/task 제안 | R&R 관리 |  |
| Review | F-05 | 승인/수정/반려/예외 | evidence 제공 |  |  |
| Audit | F-06 | 필요 시 이력 조회 | decision/evidence 기록 | 로그 관리 |  |

---

# 7. Value & Business Logic [조건부]

## 7.1 Value Proposition

- **[관련 Problem ID: P-01, P-02]**
- **[관련 Feature ID: F-01 ~ F-06]**
- **사용자 가치:** 규제검토 준비에 필요한 정보와 이슈를 한 번에 구조화하고 reviewer와 동일 evidence를 공유
- **공급자 / 파트너 가치:** **[TBD]**
- **사업 가치:** 신규 금융상품 Product Governance 업무의 AX 적용 가능성 검증
- **운영 효율 / 리스크 감소:** preventable rework 감소, 검토과정의 일관성·추적성 향상 **[검증 필요]**

## 7.2 Impact Chain

- **[관련 Feature ID: F-01 ~ F-06]**

```text
Evidence-linked pre-review
→ 상품기획 단계에서 누락/쟁점을 더 일찍 발견
→ reviewer 재작업 및 검토 대기 감소
→ review cycle time / preventable rework 감소
→ 빠르고 일관된 상품검토
→ 금융회사 Product Governance 효율 + 통제 가능성 향상
```

> **현재는 전체 chain이 Hypothesis이며 PoC/업무데이터로 검증해야 한다.**

## 7.3 Business Model [신규/BM 조건부]

- **수익 구조:** **[TBD — 본 프로젝트는 startup SaaS 사업성보다 금융회사 내부 AX use case를 우선 검증]**
- **비용 구조:** 모델 운영, 지식베이스 구축/업데이트, 보안·권한·감사, 시스템 통합
- **주요 파트너:** 법무/준법/리스크 조직, 내부 IT/보안, 규제정보/법률정보 source
- **가치 교환 구조:** **[TBD]**
- **Unit Economics 검토 필요 여부:** 외부 SaaS 사업화 시 Yes / 내부 AX 프로젝트로 진행 시 별도 ROI 모델 필요

---

# 8. KPI & Measurement

## 8.1 Primary Metric

- **[관련 Goal: 3.1]**
- **[관련 Feature ID: F-01 ~ F-06]**
- **핵심 지표:** Preventable Rework Rate / Review Cycle Time
- **정의:** AI pre-review 적용 전후, 후행 reviewer가 발견한 단순 누락·요건 미충족으로 인한 보완·재검토의 비율 또는 건수
- **현재값:** TBD
- **목표값:** TBD — 실제 baseline 확보 후 설정

## 8.2 Driver Metrics

| KPI ID | 관련 Feature ID | KPI | 정의 | 현재값 | 목표값 | 측정 방법 |
| --- | --- | --- | --- | --- | --- | --- |
| K-01 | F-01~F-04 | Time to First Issue | 상품입력 후 첫 유효 issue가 제시될 때까지 시간 | TBD | TBD | 시스템 로그 |
| K-02 | F-03 | Confirmed Gap Precision | AI가 제시한 gap 중 reviewer가 유효하다고 확인한 비율 | TBD | TBD | reviewer label |
| K-03 | F-03 | Critical Issue Recall | Golden Set 중요 이슈 중 시스템이 발견한 비율 | TBD | TBD | 평가셋 |
| K-04 | F-02 | Evidence Coverage | 주요 제안 중 출처/조문/시행일/버전이 연결된 비율 | TBD | TBD | 자동검사 |
| K-05 | F-02 | Citation Validity | 제시 근거가 실제 해당 판단을 지지하는 비율 | TBD | TBD | reviewer audit |
| K-06 | F-05 | Reviewer Override Rate | AI 제안 중 reviewer가 수정/반려한 비율 | TBD | TBD | 로그 |
| K-07 | F-04 | Task Closure Time | review task 생성부터 종결까지 소요시간 | TBD | TBD | workflow 로그 |

## 8.3 Guardrail Metrics

| KPI ID | 관련 KPI ID | Guardrail | 왜 필요한가 | 허용 범위 / 임계치 |
| --- | --- | --- | --- | --- |
| G-01 | K-03 | Critical False Negative | 중요 규제 이슈 누락은 출시 리스크로 연결 가능 | 매우 낮게 설정 / 구체값은 PoC 후 |
| G-02 | K-05 | Unsupported Citation | 근거가 틀리면 reviewer 오판 유도 | 0에 가깝게 |
| G-03 | K-04 | Outdated Rule Usage | 시행종료/구버전 규정 적용 방지 | current rule 기준 검증 |
| G-04 | K-06 | Unreviewed Final Decision | AI가 human 승인 없이 최종 판단하면 안 됨 | 0건 |
| G-05 | F-01~F-06 | Sensitive Data Leakage | 금융상품/내부정보 보호 | 0건 |

## 8.4 Event Instrumentation

| Event ID | 관련 Feature ID | Event | 발생 조건 | 주요 Property |
| --- | --- | --- | --- | --- |
| EVT-01 | F-01 | document_uploaded | 상품문서 입력 | doc_type, user_role |
| EVT-02 | F-01 | structure_confirmed | 추출값 확인 완료 | corrected_field_count |
| EVT-03 | F-02 | rule_mapped | rule 후보 연결 | rule_id, version, effective_date |
| EVT-04 | F-03 | gap_flagged | gap 후보 생성 | severity, requirement_id |
| EVT-05 | F-03 | gap_reviewed | reviewer가 gap 확인 | confirm/dismiss |
| EVT-06 | F-04 | review_task_created | 검토 task 생성 | reviewer_role, issue_type |
| EVT-07 | F-05 | ai_suggestion_overridden | reviewer가 AI 제안 수정/반려 | reason |
| EVT-08 | F-05 | human_decision_recorded | human 최종 판단 | decision_type |
| EVT-09 | F-06 | evidence_opened | 근거 조회 | source_id |
| EVT-10 | F-06 | review_completed | 전체 검토 종료 | cycle_time, rework_count |

---

# 9. Validation Plan

## 9.1 Riskiest Assumption

- **[검증 대상 Assumption ID: A-01]**
- **관련 Problem ID:** P-01, P-02
- **관련 Feature ID:** F-02, F-03, F-04

## 선정 이유:

공개자료는 인접 투자계약증권에서 regulatory rework와 발행 지연이 존재했음을 보여주지만, **증권사 토큰증권 실무에서 규제 탐색·부서간 handoff·재작업이 얼마나 자주, 얼마나 심각하게 발생하는지 정량적으로 확인하지 못했다.**  
따라서 A-01이 성립하지 않으면 별도의 Product Governance Copilot이 필요한 이유가 약해진다.

## 9.2 Validation Method

- **[검증 대상 Assumption ID: A-01]**
- 1차: **실무자 인터뷰**
- 2차: **업무 artifact / process walkthrough**
- 3차: **Prototype / Concierge Pre-review Test**
- 4차: **Golden Set 기반 AI evaluation**

## 선택 이유:

현재 가장 큰 evidence gap은 기술 가능성이 아니라 **실제 AS-IS workflow와 pain frequency/severity**다.

## 9.3 Experiment Card

- **[검증 대상 Assumption ID: A-01, A-02]**
- **[관련 KPI ID: K-01, K-02, K-03 / G-01]**
- **Hypothesis:** 토큰증권/유사 신규 금융상품의 출시 전 검토에서 후행 reviewer가 발견하는 반복적·구조화 가능한 누락/규제 확인사항이 존재하며, 일부는 AI pre-review로 조기 탐지할 수 있다.
- **Target:** 증권사 STO/디지털자산/신사업/상품기획 + 법무/준법/리스크 reviewer
- **Method:** ① 인터뷰 ② 실제/비식별 샘플 문서 walkthrough ③ prototype pre-review 비교
- **Sample:** **TBD**
- **Duration:** **TBD**
- **Primary Metric:** preventable rework 발견 여부 / review preparation time
- **Guardrail:** critical false negative
- **Success Threshold:** **baseline 확인 후 설정**
- **Failure Threshold:** 아래 Decision Rule 참고

## 9.4 Decision Rule

- **[검증 대상 Assumption ID: A-01, A-02, A-03]**
- **결과가 성공 기준 이상이면:** 토큰증권 pre-review MVP를 구체화하고 실제 데이터셋/평가셋 구축
- **결과가 애매하면:** 문제를 규제 검색이 아닌 다른 handoff/knowledge management 병목으로 재정의하거나 target role을 수정
- **결과가 실패 기준 이하이면:**
  - 업무 빈도가 매우 낮음
  - 기존 GRC/법률DB/내부 프로세스로 충분히 해결
  - downstream rework 중 사전 탐지 가능한 비중이 낮음
  - 핵심 판단 대부분이 표준화 불가능한 고도의 개별 법률판단
  - 데이터 접근·통합비용이 효율효과보다 큼

  → 별도 Copilot 구축을 중단하거나 더 넓은 Product Governance 문제로 pivot

---

# 10. Risk & Compliance [필수 / AI·규제 조건부 확장]

## 10.1 Common Risk

| ID | 관련 Feature ID | Risk | 발생 가능성 | 영향도 | 대응 / Control | Owner |
| --- | --- | --- | --- | --- | --- | --- |
| R-01 | F-02, F-03 | 중요 규제 이슈 false negative | Mid | High | human review, golden set, rule-based hard checks | AI/Product + Compliance |
| R-02 | F-02 | 구버전/시행전/폐지 규정 오적용 | Mid | High | effective date / version / superseded rule 관리 | KB Owner |
| R-03 | F-02, F-03 | hallucination / unsupported legal reasoning | Mid | High | evidence required, abstain, confidence, reviewer confirmation | AI/Product |
| R-04 | F-01~F-06 | 내부 상품정보 유출 | Low~Mid | High | 사내환경, access control, encryption, logging | Security |
| R-05 | F-04 | 잘못된 reviewer routing | Mid | Mid | 조직별 R&R rule, user override | Operation |
| R-06 | F-05 | AI output 과신 / automation bias | Mid | High | Human decision UI, rationale, counter-evidence, mandatory review | Compliance/Product |
| R-07 | F-06 | audit trail 누락/변조 | Low | High | immutable/controlled log, versioning | IT/Operation |

검토 영역:

- [x] Product
- [ ] Privacy
- [x] Security
- [ ] Fraud / Abuse
- [x] Operational
- [ ] Partner / External API
- [x] Reputation

## 10.2 AI / Model Risk [AI 조건부]

- **[관련 Feature ID: F-01 ~ F-06]**
- **AI 사용이 필요한 이유:** 비정형 상품·규제 문서의 구조화, 관련 규정 후보 탐색, 누락/쟁점 설명 등 전통적 deterministic rule만으로 처리하기 어려운 지식업무 보조
- **입력 데이터:** 상품기획서, 상품 구조정보, 법령/가이드/내부정책, 과거 검토사례 **[접근 가능 시]**
- **출력:** 구조화 상품정보, 적용 규칙 후보, evidence, 누락/불명확 정보 후보, reviewer task 후보
- **허용 가능한 오류:** 낮은 중요도의 false positive — reviewer가 쉽게 dismiss 가능한 수준
- **허용 불가능한 오류:** 중요 규제이슈 누락, 존재하지 않는 규정 인용, 구버전 규정 확정 적용, AI 단독 최종 승인
- **Human Review 시점:** 적용규칙 확정, critical issue 처리, 예외, 최종 출시판단
- **Evaluation Set:** 토큰증권/투자계약증권 규정 및 검토 사례 기반 Golden Set **[구축 필요]**
- **Monitoring:** precision/recall, citation validity, override rate, outdated rule use, abstention
- **Fallback:** 신뢰도 부족/규정충돌/근거부족 시 `판단 보류 → human escalation`

### 권장 AI System Architecture

```text
[Product Documents]
        ↓
LLM: 구조화 / 비정형 분석 / 이슈 설명
        ↓
Knowledge & Evidence Layer
- 법령
- 감독규정
- 가이드라인
- 내부정책
- 유권해석 / 사례
- version / effective date
        ↓
Rule Engine
- 명시적 금지
- 숫자 조건
- 필수 문서
- 인가/자격 요건
        ↓
Workflow Engine
- reviewer routing
- approval / escalation
- SLA / status
        ↓
Human Reviewer
- 법률판단
- 예외승인
- 리스크 수용
- 최종 출시결정
        ↓
Evidence / Decision Log
```

## 10.3 Legal / Compliance [규제 조건부]

- **[관련 Feature ID: F-02 ~ F-06]**
- **법적 지위:** 내부 업무지원 Copilot을 우선 가정. 외부 SaaS 제공 시 별도 법적 검토 필요
- **필요한 인허가 / 신고 / 등록:** **TBD**
- **자금 / 데이터 흐름:** 자금 이동 없음. 상품·내부정책 등 민감한 업무데이터 처리 가능성 존재
- **책임 주체:** 최종 판단은 인간 임직원 / reviewer가 담당하는 구조를 원칙으로 설정
- **법무 / 컴플라이언스 확인 필요 사항:**
  - AI output을 법률의견으로 볼 수 있는 범위
  - 내부통제 및 책임분배
  - 외부 LLM/API 사용 가능 범위
  - 데이터 반출/보관
  - model governance / recordkeeping
- **검토 기준일:** 2026-08-13
- **1차 출처:** 금융위원회 금융분야 AI 원칙, 토큰증권 제도화 및 협의체 자료

---

# 11. Execution Plan & Open Issues [필수]

## 11.1 Milestones

| 단계 | 관련 섹션 / ID | 산출물 | Owner | 목표일 | 상태 |
| --- | --- | --- | --- | --- | --- |
| 1 | 1.1~1.2 | Background + Evidence Map v0.1 | JENNIE | 2026-08-13 | 완료 |
| 2 | P-01, P-02 / A-01 | 토큰증권 출시 AS-IS Workflow | JENNIE | 다음 세션 | **Next** |
| 3 | P-01, P-02 | Actor별 JTBD / Pain Evidence Map | JENNIE | TBD | 예정 |
| 4 | A-01, A-03 | 기존 대체수단 / GRC / Legal AI 경쟁분석 | JENNIE | TBD | 예정 |
| 5 | A-01 | 실무자 인터뷰 설계 및 검증 | JENNIE | TBD | 예정 |
| 6 | F-01~F-06 | MVP 상세 Scope 재확정 | JENNIE | TBD | 예정 |
| 7 | A-02, A-04 | Prototype + Golden Set PoC 설계 | JENNIE | TBD | 예정 |
| 8 | K-01~G-05 | KPI baseline 및 success threshold 설정 | JENNIE | TBD | 예정 |

## 11.2 Open Questions

| ID | 관련 대상 ID | 확인 필요 사항 | Owner | 확인 방법 | 기한 |
| --- | --- | --- | --- | --- | --- |
| Q-01 | A-01 / P-01 | 실제 토큰증권 상품기획자가 어떤 문서와 규정을 확인하는가? | JENNIE | 공개자료 + 인터뷰 | 다음 |
| Q-02 | A-01 / P-02 | 법무/준법/리스크/IT/운영 중 실제 reviewer는 누구이며 어떤 순서로 참여하는가? | JENNIE | 인터뷰 / workflow 조사 | 다음 |
| Q-03 | A-01 | 검토 1건의 평균 cycle, handoff, rework 횟수는? | JENNIE | 인터뷰 / 내부 데이터 | TBD |
| Q-04 | A-03 | 현재 사용하는 법률DB, GRC, 문서·승인 시스템은 무엇인가? | JENNIE | 경쟁/대체재 조사 | TBD |
| Q-05 | A-03 | 현행 시스템이 해결하지 못하는 핵심 gap은 실제 존재하는가? | JENNIE | 인터뷰 + 제품조사 | TBD |
| Q-06 | A-02 | downstream issue 중 사전 탐지 가능한 유형/비중은? | JENNIE | 사례 분류 / PoC | TBD |
| Q-07 | A-07 | 규제 변경 추적이 실제 업무 pain인가, 단순히 우리가 중요하다고 가정한 것인가? | JENNIE | 인터뷰 | TBD |
| Q-08 | A-04 | LLM이 필요한 부분과 deterministic rule로 처리해야 할 부분은 어디인가? | JENNIE | PoC / architecture design | TBD |
| Q-09 | R-01 | Critical false negative의 허용 가능한 수준은? | JENNIE | Compliance review | TBD |
| Q-10 | F-02 | 2026년 하위법규·가이드라인의 실제 최신 발표 상태는? | JENNIE | 금융위 1차자료 재확인 | 다음 |
| Q-11 | A-06 | 토큰증권 이후 어떤 금융상품으로 확장 가능한가? | JENNIE | 후속 전략분석 | Later |
| Q-12 | Business | 이 제품을 내부 AX 시스템으로 볼지, SaaS/RegTech로 볼지 최종 사업모델은? | JENNIE | Problem validation 이후 | Later |

## 11.3 Decision Log

| 날짜 | 관련 대상 ID | 결정 | 선택지 | 선택 이유 | 근거 |
| --- | --- | --- | --- | --- | --- |
| 2026-08-13 | Project | 장기 제품 비전을 'Token Securities Copilot'이 아니라 'Financial Product Governance Copilot'으로 설정 | STO 전용 / 전 금융상품 / Product Governance + STO MVP | 특정 시장 성장에 종속되지 않고 금융권 AX의 구조적 업무문제를 다룸 | E-01, E-02 |
| 2026-08-13 | MVP | 첫 vertical을 토큰증권으로 유지 | 모든 금융상품 / 토큰증권 | 신규 제도, 세부 규율 변화, 다영역 검토가 동시에 존재해 검증환경으로 적합 | E-03~E-05 |
| 2026-08-13 | P-02 | 핵심 outcome을 '법률답변 정확도'보다 'Preventable Rework Reduction'으로 설정 | 규제 Q&A / 신고서 작성 / Pre-review | 실제 감독자료에서 기재 미흡→정정 반복→발행 지연 확인 | E-06 |
| 2026-08-13 | F-05 | Human-in-the-loop를 기능이 아닌 governance requirement로 설정 | 완전자동화 / HIL | 금융분야 AI 원칙과 미션크리티컬 업무의 책임성 | E-02 |
| 2026-08-13 | Solution | 단순 RAG 챗봇이 아니라 LLM + Rule + Workflow + Evidence 구조를 가설로 채택 | Chatbot / 복합 workflow | 규제검색보다 product impact 및 operational action 연결이 핵심 | E-02, E-04, E-05 |
| 2026-08-13 | Research | 다음 단계에서 시장규모보다 AS-IS workflow를 우선 조사 | TAM/SAM/SOM / Workflow | 가장 큰 미검증 영역이 실제 업무빈도·재작업·handoff이기 때문 | E-08 |

---

# 12. AI Utilization Log [조건부]

| 작업 | 관련 대상 ID | 사용 자료 | AI / 도구 | 결과 | 인간 검증 | 최종 반영 |
| --- | --- | --- | --- | --- | --- | --- |
| 초기 아이디어 구조화 | Project / P-01 | 사용자 아이디어 | ChatGPT | Token Securities 규제 Copilot 초기 가설 | 사용자 검토 | 수정 반영 |
| 제품 비전 확장 | Project | 금융권 AX 맥락 + 토큰증권 가설 | ChatGPT | Financial Product Governance Copilot + STO vertical | 사용자 동의 | 반영 |
| 공개근거 조사 | E-01~E-07 | 금융위·금감원 1차자료 중심 | ChatGPT Web Research | 금융권 AX, HIL, STO 제도 변화, 투자계약증권 rework evidence | 출처별 사실/추론 분리 | 반영 |
| Problem Evidence Map | P-01~P-03 / A-01~A-07 | 공개근거 + 사용자 논의 | ChatGPT | Fact / Inference / Hypothesis 분리 | 미검증 항목 명시 | 반영 |
| 기획서 Working Draft | 전체 | PM 프로젝트 실무 템플릿 | ChatGPT | v0.1 작성 | 다음 세션에서 사용자 리뷰 예정 | 현재 문서 |

---

# Appendix A. Evidence Map Snapshot

| Hypothesis | 검증하려는 주장 | 현재 판정 |
| --- | --- | --- |
| H1 | 토큰증권 담당자는 지속적인 rule update를 따라가야 한다 | **강함** |
| H2 | 여러 규제영역을 동시에 검토해야 한다 | **강함** |
| H3 | 금융상품 출시 자체가 통제 workflow다 | **강함** |
| H4 | 실제 regulatory rework가 발생한다 | **인접 투자계약증권에서 매우 강함** |
| H5 | 현재 해결방식은 사람+가이드 중심이다 | **중간~강함 / 내부 시스템 추가조사 필요** |
| H6 | AI-assisted Copilot이 해당 workflow에 적합하다 | **중간~강함 / 실제 효과 PoC 필요** |
| H7 | Human-in-the-loop가 필요하다 | **매우 강함** |
| H8 | 실제 증권사에서 pain의 빈도·심각도가 크다 | **미검증** |
| H9 | 별도 Copilot이 기존 GRC/Legal DB보다 낫다 | **미검증** |
| H10 | 경제적 효과가 충분히 크다 | **미검증** |

---

# Appendix B. 내일 바로 재개할 지점

## 다음 질문

> **실제 토큰증권 상품 출시 조직에서는 규제정보가 어떤 경로로 Product Decision으로 변환되는가?**

## 다음 조사 순서

1. **Actor 확정**
   - STO/디지털자산/신사업/상품기획
   - 준법감시
   - 법무
   - 리스크
   - 운영
   - IT/보안

2. **AS-IS Workflow 조사**
   - Trigger
   - Input
   - 규제/가이드 조회
   - reviewer
   - handoff
   - decision
   - rework
   - evidence / 기록
   - 현재 도구

3. **Pain Evidence 수집**
   - 존재 여부
   - 빈도
   - 심각도
   - 현재 해결법
   - 시간/인력/일정 영향
   - 기존 시스템의 미해결 영역

4. **Falsification Check**
   - workflow가 저빈도인가?
   - 기존 GRC로 충분한가?
   - 사전탐지 가능한 issue가 적은가?
   - 개별 법률판단 비중이 너무 높은가?
   - 데이터/통합비용이 효과보다 큰가?

5. **검증 후에만**
   - 최종 Problem Statement
   - Core Persona/JTBD
   - MVP 기능 우선순위
   - KPI target
   - 경쟁/대체재 gap
   - PoC 설계

## 내일 시작하지 말아야 할 것

- TAM/SAM/SOM부터 계산
- “STO 시장이 성장하므로 필요하다”는 식의 논리
- AI가 80% 시간을 줄인다는 임의의 목표 설정
- 증권사 내부 pain을 공개자료 없이 사실로 단정
- 단순 RAG 챗봇을 solution으로 고정
- B2G SupTech와 증권사 내부 Copilot을 하나의 PRD로 혼합

---

# Appendix C. 현재 프로젝트를 한 문장으로 설명한다면

> **금융권 AX 시대에 복잡한 금융상품의 출시 검토를 AI-assisted workflow로 전환하는 Product Governance Copilot을 설계하고, 첫 MVP로 제도 변화와 다부서 검토가 동시에 존재하는 토큰증권을 선택해 downstream regulatory rework를 얼마나 앞단에서 예방할 수 있는지 검증한다.**
