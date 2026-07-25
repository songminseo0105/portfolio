# Symbolic Regression Study

> Doowon Choi 교수 연구실 학부연구생 활동 (2026.06 ~ 현재)
> 공정 데이터에 Symbolic Regression을 적용하기 앞서, 알려진 물리 법칙 데이터로 방법론을 검증·학습한 기록입니다.

## 개요
Decision Tree로 데이터를 물리적 영역(regime)별로 분리한 뒤, 각 영역에 대해 Symbolic Regression을 적용해 해석 가능한 수식을 도출하는 연구를 진행 중입니다. 실제 공정 데이터 적용 전 단계로, 만유인력 법칙·유체 항력·이상기체 방정식 등 정답 수식을 아는 물리 데이터를 생성해 방법론을 검증했습니다.

## 진행 순서

### 1. `2_GPlearn.ipynb` — 라이브러리 기반 SR 베이스라인
- `gplearn`을 사용해 Symbolic Regression의 기본 동작 방식(유전 알고리즘 기반 수식 탐색) 학습

### 2. `3_pySR.ipynb` — PySR + Decision Tree 기반 영역 분리
- 유체 항력 데이터(레이놀즈 수 기준 층류/난류 전환)를 `DecisionTreeClassifier`로 물리적 영역(regime)별로 분리
- 분리된 그룹별로 `PySR`을 적용해 각 영역에 맞는 수식을 독립적으로 도출
- 단조성 제약조건(monotonic constraints)을 반영한 커스텀 objective function 설계
- `safe_log`, `safe_sqrt` 등 도메인에 안전한 커스텀 연산자 정의

### 3. `1_my_program.ipynb` — 직접 구현한 Symbolic Regression
- 라이브러리 없이 유전 알고리즘 기반 SR을 직접 구현
  - Node 기반 수식 트리 구조 설계 (변수/상수/연산자 노드)
  - Tournament Selection, Crossover, Simulated Annealing 기반 Mutation
  - SciPy 기반 상수 최적화(Constant Optimization)
  - SymPy를 통한 수식 단순화 및 파레토 프론트(복잡도 대비 성능) 관리
  - Julia(Zygote) 연동을 통한 미분 기반 단조성 제약 평가
- 만유인력 법칙, 유체 항력(층류/난류), 이상기체 방정식 데이터로 검증

## 사용 기술
Python, NumPy, Pandas, SciPy, SymPy, Scikit-learn(Decision Tree), gplearn, PySR, Julia(Zygote 연동)

## 현재 진행 중
Symbolic Regression을 Clustering과 결합하는 방법, 다양한 constraints 조건 적용을 논문 조사와 함께 실험 중입니다.
