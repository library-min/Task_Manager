# Task Manager

**생산성 향상을 위한 웹 기반 할 일 관리 도구**
**개인 프로젝트**

---

## 내가 한 일

**모든 기능을 처음부터 설계하고 구현했습니다.**

* **화면 설계**: 사용자가 필요한 모든 페이지 기획 및 UI/UX 설계
* **React 개발**: 모든 컴포넌트 및 기능 직접 작성
* **스타일링**: Tailwind CSS로 반응형 디자인 구현
* **상태 관리**: Context API로 효율적인 전역 상태 관리
* **기능 최적화**: useMemo, useCallback으로 성능 최적화

**결과**: 완전한 웹 기반 할 일 관리 도구 완성

---

## 주요 기능 & 스크린샷

### 1️⃣ 메인 화면 (라이트 모드)

[![메인 화면](public/To-Do List_2 Full Page (Light).png)](./public/To-Do%20List_2%20Full%20Page%20(Light).png)

---

### 2️⃣ 대시보드 (통계 시각화)

[![대시보드](./public/To-Do%20List_2%20Dash.png)](./public/To-Do%20List_2%20Dash.png)

**설계한 것**

* 5개의 통계 카드 (전체/남은/완료 할 일, 완료율, 카테고리 수)
* Chart.js로 실시간 통계를 시각화하는 구조
* 할 일 변경 시 즉시 반영되는 동적 업데이트

```
// 통계를 useMemo로 메모이제이션
const stats = useMemo(() => ({
  total: todos.length,
  remaining: todos.filter(t => !t.completed).length,
  completed: todos.filter(t => t.completed).length
}), [todos]);
```

**결과**

* 모든 통계 정보를 한눈에 파악 가능
* 모바일/태블릿/PC 모두 반응형 작동

---

### 3️⃣ 할 일 관리 시스템

[![할 일 목록](public/To-Do List_2 Full Page (Light).png)](./public/To-Do%20List_2%20Full%20Page.png)

**설계한 것**

* 할 일 목록을 카드 형식으로 표시
* 우선순위별 색상 구분 (높음/보통/낮음)
* 검색 & 필터링 기능
* 완료/미완료 토글

```
// 필터링을 useMemo로 최적화
const filteredTodos = useMemo(() => {
  return todos
    .filter(t => selectedCategory === 'all' || t.category === selectedCategory)
    .filter(t => t.text.includes(searchQuery))
    .sort(sortComparator);
}, [todos, selectedCategory, searchQuery, sortComparator]);
```

**결과**

* 직관적인 할 일 관리 인터페이스
* 검색과 필터링으로 빠른 접근

---

### 4️⃣ 테마 & 다크모드

[![다크 모드](public/To-Do List_2 Full Page.png)](./public/To-Do%20List_2%20Full%20Page.png)

**설계한 것**

* 다크/라이트 모드 (시스템 설정 감지 + 수동 토글)
* 7가지 컬러 팔레트 (블루, 그린, 퍼플, 핑크, 옐로우, 오렌지, 레드)
* CSS Variable로 동적 테마 관리
* 완전 반응형 (모바일 320px ~ 데스크톱 1920px+)

```
<!-- 테마 변경 시 자동으로 CSS 업데이트 -->
<script>
const changeTheme = (newColor) => {
  document.documentElement.setAttribute('data-color', newColor);
  localStorage.setItem('theme-color', newColor);
};
</script>
```

**결과**

* 사용자가 선호하는 테마로 커스터마이징 가능
* 모든 디바이스에서 최적의 경험 제공

---

## 성과

| 지표 | 개선 내용 |
| --- | --- |
| **기능 완성도** | 11개 주요 기능 모두 구현 |
| **성능 최적화** | useMemo/useCallback으로 불필요한 리렌더링 제거 |
| **디자인** | 다크모드 + 7가지 테마 + 완전 반응형 |
| **사용자 경험** | 직관적인 인터페이스 + 부드러운 애니메이션 |

---

## 🛠 기술 스택

**Frontend (내가 구현)**

* React 19.1.1 (Hooks & Context API)
* Vite 7.1.2 (빌드 도구)
* Tailwind CSS 3.4.15 (반응형 디자인)
* JavaScript ES6+ (동적 기능)
* Chart.js (데이터 시각화)

**Storage & State**

* Local Storage API (데이터 영속성)
* Context API (전역 상태 관리)
* React Router (페이지 네비게이션)

---

## 배운 점

### 문제 1: React Hooks로 효율적인 상태 관리

**상황**: 할 일, 카테고리, 필터 등 여러 상태를 관리해야 함  
**해결**: useState와 useContext로 전역 상태 중앙화  
**결과**: 상태 관리 코드 간결화, props drilling 제거

### 문제 2: 성능 최적화

**상황**: 할 일이 많아지면서 리렌더링으로 인한 성능 저하  
**해결**: useMemo로 통계 계산, useCallback으로 이벤트 핸들러 메모이제이션  
**결과**: 불필요한 리렌더링 제거, 부드러운 UX 유지

### 문제 3: Local Storage로 데이터 영속성 구현

**상황**: 브라우저 새로고침 후 데이터가 사라짐  
**해결**: Local Storage API로 JSON 직렬화/역직렬화  
**결과**: 브라우저 재시작 후에도 데이터 유지

### 문제 4: 다크모드 + 다중 테마 관리

**상황**: 다크/라이트 모드와 7가지 컬러를 모두 지원하려면 CSS 작성량이 기하급수적으로 증가  
**해결**: CSS Variable + React Context로 동적 테마 관리  
**결과**: 테마 전환 시 즉시 UI 반영, 사용자 선택 저장

### 문제 5: 반응형 디자인

**상황**: 모바일/태블릿/PC 모두에서 최적의 경험 제공 필요  
**해결**: Tailwind CSS 반응형 유틸리티 클래스 활용  
**결과**: 모든 해상도에서 완벽한 반응형 작동

### 문제 6: 사용자 경험 개선

**상황**: 단순 기능만으로는 사용자가 만족하지 못함  
**해결**: 부드러운 애니메이션, 토스트 알림, 직관적인 인터페이스 추가  
**결과**: 사용자가 즐겁게 사용하는 도구

---

## 구현한 기능 목록

| 기능 | 설명 | 기술 |
| --- | --- | --- |
| **사용자 인증** | 이메일 기반 회원가입 & 로그인 | React Context |
| **할 일 관리** | 추가/수정/삭제/완료 처리 | useState |
| **카테고리 시스템** | 기본 4개 + 커스텀 카테고리 | Context API |
| **우선순위 & 마감일** | 3단계 우선순위 + 날짜 설정 | Date API |
| **검색 & 필터링** | 실시간 검색 + 상태/카테고리 필터 | useMemo |
| **일괄 작업** | 다중 선택으로 한 번에 처리 | useState |
| **대시보드** | 5개 통계 카드 + Chart.js 시각화 | Chart.js |
| **다크/라이트 모드** | 시스템 설정 감지 + 수동 토글 | CSS Variable |
| **7가지 컬러 팔레트** | 사용자 선택 테마 | CSS Variable |
| **반응형 디자인** | 모바일 ~ 데스크톱 최적화 | Tailwind CSS |
| **Local Storage** | 데이터 영속성 | Local Storage API |

---

## 핵심 역량

✅ **React Hooks 숙련도**: useState, useContext, useCallback, useMemo 활용  
✅ **상태 관리**: Context API로 복잡한 전역 상태 효율적 관리  
✅ **CSS & Tailwind**: 반응형 디자인 & 다크모드 구현  
✅ **성능 최적화**: 메모이제이션으로 불필요한 렌더링 방지  
✅ **UX/UI**: 사용자 경험을 고려한 인터페이스 설계  
✅ **Local Storage**: 브라우저 저장소를 활용한 데이터 관리  

---

## 향후 개발 로드맵

### Phase 1: PWA 지원
* Service Worker 구현
* 오프라인 모드 지원
* 앱 설치 프롬프트

### Phase 2: 고급 기능
* 드래그 앤 드롭 순서 변경
* 할 일 복제 기능
* 파일 첨부 지원
* 태그 시스템

### Phase 3: 협업 & 클라우드
* Firebase/Supabase로 실시간 동기화
* 팀 워크스페이스
* 할 일 공유 및 할당

