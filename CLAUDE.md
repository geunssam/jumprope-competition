# CLAUDE.md - JumpRope Competition Project

Claude Code가 이 프로젝트에서 작업할 때 참고하는 지침 파일입니다.

---

## 📋 Project Overview

**프로젝트명**: 줄넘기 마스터 (JumpRope Master)
**목적**: 학교 줄넘기 연습 및 대회를 위한 종합 관리 시스템

### Current Status

#### v19 (Legacy - 현재 배포 중)
- **타입**: 단일 HTML 파일
- **배포**: https://jumpropecompetition.netlify.app
- **상태**: 유지 보수 모드 (백업용)

#### v20 (In Development - JumpRope Master)
- **타입**: React + Firebase 기반 대규모 시스템
- **개발 기간**: 4주 (중간 규모)
- **시작일**: 2025-01-20 (예정)
- **상태**: 계획 완료, 개발 대기

---

## 🏗️ Technology Stack

### v19 (Legacy)
- React 18 (CDN)
- Tailwind CSS (CDN)
- LocalStorage 기반 데이터 저장
- 단일 HTML 파일 (188KB)

### v20 (JumpRope Master)
- **Frontend**: React 19.1.1 + Vite
- **Backend**: Firebase (Authentication + Firestore)
- **UI Library**: Tailwind CSS + shadcn/ui (17개 컴포넌트)
- **Router**: React Router DOM v7
- **Charts**: Chart.js 또는 Recharts
- **Additional**: @dnd-kit, React Hot Toast, date-fns
- **Deployment**: Netlify

---

## 🎯 Architecture Reference

v20은 **baseball-firebase** 프로젝트의 아키텍처를 기반으로 합니다.

### Baseball-Firebase 위치
```
/Users/iwongeun/Desktop/필드형게임 마스터 보드/baseball-firebase
```

### 참고할 패턴
1. **Firebase 데이터 구조**: `users/{userId}/` 기반 격리
2. **컴포넌트 구조**: 기능별 폴더 분리 (50+ 컴포넌트)
3. **Context API**: AuthContext, GameContext 패턴
4. **서비스 계층**: firestoreService.js (98KB)
5. **배지 시스템**: 자동/커스텀 배지 로직
6. **통계 계산**: statsCalculator, mvpCalculator
7. **학생 뷰**: StudentAuthContext + CollectionGroup 쿼리

---

## 📁 File Organization

### 현재 구조
```
jumprope-competition/
├── index.html              # v19 레거시 (유지)
├── netlify.toml            # 배포 설정
├── .gitignore
├── README.md
├── CLAUDE.md               # 이 파일
└── docs/
    └── JUMPROPE_MASTER_PLAN.md    # v20 전체 계획서
```

### v20 개발 시 구조 (예정)
```
jumprope-competition/
├── index.html              # v19 백업용
├── src/                    # v20 소스 코드
│   ├── components/         # 50+ 컴포넌트
│   ├── contexts/           # Context API
│   ├── services/           # Firebase 서비스
│   ├── utils/              # 유틸리티 함수
│   └── App.jsx
├── public/
├── docs/
├── package.json
├── vite.config.js
└── netlify.toml
```

---

## 🎨 Design Philosophy

### 사용자 특성
- **주 사용자**: 초등학교 교사 (비전공자)
- **보조 사용자**: 초등학생 (3~6학년)
- **사용 환경**: 체육관, 교실 (아이패드/태블릿)

### 디자인 원칙
1. **미니멀리즘**: 군더더기 없는 깔끔한 UI
2. **세밀한 정렬**: 표, 텍스트가 픽셀 단위로 정렬
3. **줄바꿈 방지**: 단어/표현이 중간에 끊기지 않도록 (`단무\n지` ❌)
4. **터치 최적화**:
   - 터치 타겟 최소 44px (Apple 가이드라인)
   - 터치 피드백 제공
   - 드래그 앤 드롭 지원
5. **한눈에 보기**: 스크롤 최소화 (필요시 허용)

### 컬러 시스템
- 학년별 색상 구분
- 팀 구분 (예: 블루/레드)
- 배지 등급별 색상

---

## 🎯 Key Features (v20)

### 7개 메인 섹션
1. **메인 대시보드**: 빠른 시작, 최근 활동, 통계 위젯
2. **학급/학생 관리**: 학급 생성, 학생 등록, 코드 발급
3. **종목 관리**: 기본 16개 + 커스텀 종목
4. **연습/대회 관리**: 연습/대회 구분, 세션 관리
5. **기록 입력**: 타이머, 카운터, 실시간 배지 수여
6. **통계 & 순위**: 개인/팀/학급 통계, 차트
7. **학생 뷰**: 학생 코드 로그인, 개인 기록, 배지

### 특별 기능
- **배지 시스템**: 자동 15개 + 커스텀 무제한
- **타이머 시스템**: 준비(3초) → 카운트다운 → 진행 → 종료
- **전체화면 모드**: 타이머를 대형 화면에 표시
- **CSV 다운로드**: 전체 데이터 엑셀 내보내기

---

## 🗂️ Firebase Data Structure

```javascript
users/{userId}/
├── classes/         # 학급
├── students/        # 학생 (studentCode 포함)
├── events/          # 종목 (기본 + 커스텀)
├── sessions/        # 연습/대회 세션
├── records/         # 기록
├── badges/          # 학생별 배지
├── customBadges/    # 커스텀 배지
└── settings/        # 설정
```

---

## 📅 Development Roadmap

### Week 1: 기본 구조 + Firebase 설정
- Vite + React 프로젝트 생성
- Tailwind CSS + shadcn/ui 설정
- Firebase 연동 (Auth, Firestore)
- 기본 라우팅 및 레이아웃

### Week 2: 핵심 기능 구현
- 학급/학생/종목/세션 관리
- 기록 입력 시스템 (타이머 + 카운터)
- Firestore 데이터 모델 구축

### Week 3: 통계 + 배지 시스템
- 개인/팀/학급 통계
- 차트/그래프 연동
- 자동 배지 15개 + 커스텀 배지

### Week 4: 학생 뷰 + 최적화
- 학생 로그인 및 뷰
- 반응형 디자인 최적화
- 성능 최적화 및 배포

---

## 🚀 Deployment

### Platform
- **Netlify** (확정)

### Build Settings
```toml
[build]
  command = "npm run build"
  publish = "dist"

[build.environment]
  NODE_VERSION = "20"
```

### Environment Variables
```
VITE_FIREBASE_API_KEY=...
VITE_FIREBASE_AUTH_DOMAIN=...
VITE_FIREBASE_PROJECT_ID=...
VITE_FIREBASE_STORAGE_BUCKET=...
VITE_FIREBASE_MESSAGING_SENDER_ID=...
VITE_FIREBASE_APP_ID=...
```

---

## 🇰🇷 Korean Language Support

### 언어 사용
- **UI 텍스트**: 100% 한국어
- **코드 주석**: 한국어/영어 혼용 가능
- **문서**: 한국어 우선, 필요시 영어 병기

### 용어 설명
- IT 용어 사용 시 항상 쉬운 설명 제공
- 비유를 통한 설명 권장
- 비전공자도 이해 가능한 수준

### 예시
```javascript
// ❌ 나쁜 예
const handleClick = () => { ... }

// ✅ 좋은 예
const handleStudentAdd = () => {
  // 학생 추가 버튼 클릭 시 처리
  ...
}
```

---

## 💡 Development Guidelines

### 점진적 접근
1. **프로토타입 먼저**: 핵심 기능부터 구현
2. **기능 추가**: 단계별로 추가
3. **서버 구축**: 마지막에 최적화

### 오류 처리
1. 전체 코드 점검 (메타인지)
2. 문제 분석 (어디서, 왜)
3. 해결 방안 제시 (전체 vs 부분)
4. 상세 기획안 작성
5. 허가 후 수정 진행
6. **오류 기록**: 모든 오류와 해결 과정 문서화

### 코드 스타일
- **명확한 네이밍**: 기능이 드러나는 이름
- **컴포넌트 분리**: 단일 책임 원칙
- **주석 추가**: 복잡한 로직은 설명 필수
- **타입 안전**: (TypeScript 사용 시)

---

## 🎯 Workflow Principles

### 개발 6대 원칙

**1. 명확한 목표**
- 초등학교 줄넘기 **연습 기록** 및 **대회 진행**을 위한 시스템
- 교사와 학생이 모두 사용
- 아이패드/태블릿 터치 환경 최적화

**2. Baseball-Firebase 프로젝트 전체 참고**
- 위치: `/Users/iwongeun/Desktop/필드형게임 마스터 보드/baseball-firebase`
- 아키텍처, 패턴, 컴포넌트 구조 그대로 활용
- 매핑 가이드 참조 (아래 섹션)

**3. Phase별 Step-by-Step 순차 진행**
- 10개 Phase로 세분화 (아래 로드맵 참조)
- 각 Phase 완료 후 다음 Phase 진행
- 병렬 작업 금지 (순차적으로만)

**4. 목적에 맞는 함수 호출**
- Read: 기존 파일 확인, baseball-firebase 참고
- Write: 새 파일 생성
- Edit: 기존 파일 수정
- Grep: 코드 패턴 검색
- Bash: npm, git 명령어

**5. 필수 도구 적극 활용**
- **Task(Explore)**: baseball-firebase 코드 탐색
- **Task(Plan)**: 복잡한 기능 계획 수립
- **/sc:implement**: 기능 구현 시작
- **/sc:troubleshoot**: 오류 해결

**6. 승인 기반 워크플로우** ⭐ 가장 중요!
```
1. 사용자 요청
   ↓
2. Claude가 계획 제시 (Plan Mode)
   ↓
3. 사용자 허가 대기
   ↓
4. 코드 작업 실행
   ↓
5. Phase별 Git Push 여부 확인
   - 주요 마일스톤 완료 시마다 확인
   - 사용자가 원할 때만 Push
```

---

## 🏗️ Baseball-Firebase Mapping Guide

v20 개발 시 baseball-firebase 프로젝트를 참고하기 위한 1:1 매핑 가이드입니다.

### 핵심 컴포넌트 매핑

#### 메인 & 네비게이션
| Baseball | JumpRope | 역할 |
|----------|----------|------|
| MainApp.jsx | JumpRopeApp.jsx | 메인 대시보드, 모든 모달 관리 |
| App.jsx | App.jsx | 최상위 라우팅, Context Provider |

#### 학급/학생 관리
| Baseball | JumpRope | 역할 |
|----------|----------|------|
| ClassTeamManagementView.jsx | ClassStudentManagementView.jsx | 학급/학생 관리 (드래그앤드롭) |
| AddPlayerModal.jsx | AddStudentModal.jsx | 학생 추가 모달 |
| StudentCodeListModal.jsx | StudentCodeListModal.jsx | 학생 코드 일괄 조회 |

#### 경기/기록 진행
| Baseball | JumpRope | 역할 |
|----------|----------|------|
| **GameScreen.jsx** | **RecordScreen.jsx** | 🎯 핵심! 타이머+카운터 |
| CreateGameModal.jsx | CreateRecordModal.jsx | 기록 시작 모달 |
| GameEndModal.jsx | RecordEndModal.jsx | 기록 종료 모달 |

#### 통계 & 순위
| Baseball | JumpRope | 역할 |
|----------|----------|------|
| StatsView.jsx | StatsView.jsx | 통합 통계 뷰 |
| ClassRankingWidget.jsx | ClassRankingWidget.jsx | 학급 랭킹 위젯 |
| StudentHistoryModal.jsx | StudentHistoryModal.jsx | 학생 기록 히스토리 |

#### 배지 시스템 (그대로 활용)
| Baseball | JumpRope | 역할 |
|----------|----------|------|
| BadgeManagementModal.jsx | BadgeManagementModal.jsx | 배지 관리 |
| BadgeCreator.jsx | BadgeCreator.jsx | 커스텀 배지 생성 |
| ManualBadgeModal.jsx | ManualBadgeModal.jsx | 수동 배지 수여 |
| BadgeCollection.jsx | BadgeCollection.jsx | 배지 컬렉션 |
| BadgePopup.jsx | BadgePopup.jsx | 배지 획득 축하 |

### 데이터 구조 변환

#### Baseball Stats → JumpRope Stats
```javascript
// Baseball Player Stats
{
  single: 2,      // 1루타
  double: 1,      // 2루타
  homerun: 1,     // 홈런
  runs: 3,        // 득점
  goodDefense: 2  // 수비
}

// JumpRope Student Stats
{
  totalJumps: 150,      // 총 점프 횟수
  consecutiveMax: 45,   // 최대 연속 성공
  failCount: 5,         // 실패 횟수
  avgSpeed: 120,        // 평균 속도 (회/분)
  improvement: 15,      // 향상도 (%)
  bonusPoints: 2        // 보너스 점수
}
```

### 서비스 함수 매핑

| Baseball | JumpRope | Firebase 경로 |
|----------|----------|--------------|
| createTeam() | createClass() | users/{userId}/classes/ |
| createPlayer() | createStudent() | users/{userId}/students/ |
| createGame() | createRecord() | users/{userId}/records/ |
| finishGame() | finishRecord() | users/{userId}/records/ |
| subscribeToGames() | subscribeToRecords() | 실시간 리스너 |

### Context API 구조

```javascript
// Baseball: GameContext
// JumpRope: RecordContext

{
  // 공통 데이터
  classes,          // 학급 목록
  students,         // 학생 목록
  records,          // 진행 중 기록
  finishedRecords,  // 완료된 기록
  playerBadges,     // 학생 배지

  // 공통 함수
  createClass,
  createStudent,
  createRecord,
  finishRecord,
  savePlayerBadges
}
```

### 반드시 참고할 파일 TOP 10

1. **`src/services/firestoreService.js`** ⭐⭐⭐
   - Firebase CRUD 패턴의 정석
   - 모든 데이터베이스 작업의 기본

2. **`src/contexts/GameContext.jsx`** ⭐⭐⭐
   - 전역 상태 관리 패턴
   - RecordContext로 변경하여 사용

3. **`src/contexts/StudentAuthContext.jsx`** ⭐⭐⭐
   - 학생 코드 로그인 시스템
   - CollectionGroup 쿼리 사용법

4. **`src/components/GameScreen.jsx`** ⭐⭐⭐
   - 가장 복잡한 컴포넌트
   - RecordScreen의 기본 설계

5. **`src/utils/badgeSystem.js`** ⭐⭐⭐
   - 배지 정의 및 조건 체크
   - JumpRope용으로 배지만 변경

6. **`src/utils/autoBadgeChecker.js`** ⭐⭐
   - 자동 배지 수여 로직
   - 기록 입력 시 호출

7. **`src/components/ClassTeamManagementView.jsx`** ⭐⭐
   - 드래그앤드롭 패턴
   - 학생 관리 UI 참고

8. **`src/utils/statsCalculator.js`** ⭐⭐
   - 통계 계산 로직
   - 가중치만 JumpRope용으로 변경

9. **`src/components/MainApp.jsx`** ⭐⭐
   - 모달 관리 패턴
   - 뷰 전환 로직

10. **`src/utils/studentCodeGenerator.js`** ⭐
    - 학생 코드 생성 로직
    - 그대로 활용 가능

---

## 📅 10-Phase Development Roadmap

4주 개발 일정을 10개 Phase로 세분화한 로드맵입니다.

### Phase 1: 프로젝트 초기화 (1일)
**목표**: Git 브랜치 생성, Vite + React 프로젝트 초기화
- [ ] Git 브랜치 생성 (`feature/jumprope-master`)
- [ ] Vite 프로젝트 생성 (`npm create vite@latest`)
- [ ] 기본 폴더 구조 생성 (`src/components`, `src/contexts`, `src/services`, `src/utils`)
- [ ] .gitignore 업데이트
- [ ] 🚀 **Git Push**: 프로젝트 초기화 완료 시

### Phase 2: Firebase 설정 + 인증 (1일)
**목표**: Firebase 프로젝트 생성 및 Google 로그인 구현
- [ ] Firebase 프로젝트 생성 (Console)
- [ ] Firebase SDK 설치 (`npm install firebase`)
- [ ] `src/firebase/config.js` 작성
- [ ] `.env.local` 환경변수 설정
- [ ] AuthContext.jsx 작성 (Google 로그인)
- [ ] 🚀 **Git Push**: 로그인 동작 확인 후

### Phase 3: Tailwind + shadcn/ui 설정 (1일)
**목표**: UI 라이브러리 설치 및 기본 레이아웃
- [ ] Tailwind CSS 설치 및 설정
- [ ] shadcn/ui 초기화 (`npx shadcn-ui@latest init`)
- [ ] 17개 컴포넌트 설치 (Button, Dialog, Table, Input 등)
- [ ] 기본 레이아웃 컴포넌트 작성
- [ ] React Router DOM 설치 및 라우팅 설정
- [ ] 🚀 **Git Push**: UI 기본 설정 완료 시

### Phase 4: firestoreService + RecordContext (2일)
**목표**: Firebase 서비스 레이어 및 전역 상태 관리
- [ ] `src/services/firestoreService.js` 작성
  - baseball-firebase 참고
  - createClass, createStudent, createRecord 등
- [ ] RecordContext.jsx 작성
  - GameContext.jsx를 RecordContext로 변경
  - 실시간 리스너 구현
- [ ] App.jsx에 Context Provider 래핑
- [ ] 🚀 **Git Push**: Context API 동작 확인 후

### Phase 5: 학급/학생 관리 UI (3일)
**목표**: 학급 생성, 학생 추가/수정/삭제, 학생 코드 발급
- [ ] ClassStudentManagementView.jsx
  - ClassTeamManagementView.jsx 참고
  - 드래그앤드롭 (DnD Kit)
- [ ] AddStudentModal.jsx
- [ ] StudentCodeListModal.jsx
- [ ] studentCodeGenerator.js (그대로 복사)
- [ ] 🚀 **Git Push**: 학급/학생 CRUD 완료 시

### Phase 6: 종목 관리 + 세션 관리 (2일)
**목표**: 기본 16개 종목 설정, 연습/대회 세션 생성
- [ ] EventManagementView.jsx (새로 작성)
  - 기본 종목 16개 정의
  - 커스텀 종목 추가 기능
- [ ] SessionManagementView.jsx
  - CreateRecordModal.jsx
  - 연습/대회 구분
- [ ] 🚀 **Git Push**: 종목/세션 관리 완료 시

### Phase 7: 기록 시스템 (타이머 + 카운터) (4일) 🎯 **핵심!**
**목표**: RecordScreen 구현 - 타이머, 카운터, 실시간 기록
- [ ] RecordScreen.jsx
  - GameScreen.jsx 참고 (구조만)
  - 타이머 시스템 (준비 3초 → 카운트다운 → 진행 → 종료)
  - 카운터 입력 (+1, +10, -1, -10)
  - 전체화면 모드
- [ ] RecordEndModal.jsx
- [ ] 기록 자동 저장 (Firestore)
- [ ] 🚀 **Git Push**: 타이머 + 카운터 동작 확인 후

### Phase 8: 배지 시스템 (3일)
**목표**: 자동 배지 15개 + 커스텀 배지 + 축하 팝업
- [ ] badgeSystem.js 수정
  - JumpRope용 배지 15개 정의
  - 조건 변경 (안타/득점 → 점프 횟수/연속 성공)
- [ ] autoBadgeChecker.js (그대로 복사)
- [ ] BadgeManagementModal.jsx (그대로 복사)
- [ ] BadgeCreator.jsx (그대로 복사)
- [ ] ManualBadgeModal.jsx (그대로 복사)
- [ ] BadgePopup.jsx (그대로 복사)
- [ ] RecordScreen에 배지 수여 로직 통합
- [ ] 🚀 **Git Push**: 배지 시스템 동작 확인 후

### Phase 9: 통계 & 차트 (3일)
**목표**: 개인/학급 통계, 순위, 차트 연동
- [ ] StatsView.jsx (그대로 복사 후 수정)
- [ ] statsCalculator.js 수정
  - JumpRope용 가중치 변경
- [ ] ClassRankingWidget.jsx (그대로 복사)
- [ ] Chart.js 또는 Recharts 설치
- [ ] 차트 컴포넌트 작성
- [ ] CSV 다운로드 기능
- [ ] 🚀 **Git Push**: 통계 화면 완성 시

### Phase 10: 학생 뷰 + 최적화 + 배포 (3일)
**목표**: 학생 로그인, 개인 기록 조회, Netlify 배포
- [ ] StudentAuthContext.jsx (그대로 복사)
- [ ] StudentView.jsx (새로 작성)
  - 개인 기록 조회
  - 배지 컬렉션
  - 학급 순위
- [ ] 반응형 디자인 최적화 (모바일/태블릿)
- [ ] 성능 최적화 (코드 스플리팅, Lazy Loading)
- [ ] Netlify 배포 설정
  - `netlify.toml` 주석 해제
  - 환경변수 설정
- [ ] 🚀 **Git Push**: 최종 배포 완료 시

---

## 🛠️ Phase-by-Phase Development Guide

각 Phase별 상세 개발 가이드입니다. (접기 가능)

<details>
<summary><b>Phase 1: 프로젝트 초기화</b></summary>

### 사용할 도구
- **Bash**: `git checkout -b`, `npm create vite`, `mkdir`
- **Write**: `.gitignore`, `README.md`

### 체크리스트
```bash
# 1. Git 브랜치 생성
git checkout -b feature/jumprope-master

# 2. Vite 프로젝트 생성
npm create vite@latest . -- --template react

# 3. 의존성 설치
npm install

# 4. 폴더 구조 생성
mkdir -p src/components src/contexts src/services src/utils src/firebase

# 5. 개발 서버 실행 테스트
npm run dev
```

### Git Push 타이밍
- ✅ `package.json` 생성 확인
- ✅ `src/` 폴더 구조 생성 확인
- ✅ 개발 서버 정상 동작 확인

</details>

<details>
<summary><b>Phase 2: Firebase 설정 + 인증</b></summary>

### 참고 파일
- `baseball-firebase/src/firebase/config.js`
- `baseball-firebase/src/contexts/AuthContext.jsx`

### 사용할 도구
- **Bash**: `npm install firebase`
- **Task(Explore)**: Firebase 설정 패턴 탐색
- **Write**: `src/firebase/config.js`, `src/contexts/AuthContext.jsx`, `.env.local`

### 체크리스트
```bash
# 1. Firebase SDK 설치
npm install firebase

# 2. Firebase Console에서 프로젝트 생성
# - https://console.firebase.google.com
# - 프로젝트 이름: jumprope-master
# - Firestore, Authentication 활성화

# 3. .env.local 작성
VITE_FIREBASE_API_KEY=...
VITE_FIREBASE_AUTH_DOMAIN=...
VITE_FIREBASE_PROJECT_ID=...
```

### 구현 순서
1. `src/firebase/config.js` - Firebase 초기화
2. `src/contexts/AuthContext.jsx` - Google 로그인
3. `src/App.jsx` - AuthContext Provider 래핑
4. 로그인 UI 테스트

### Git Push 타이밍
- ✅ Google 로그인 성공
- ✅ Firebase Console에서 사용자 확인

</details>

<details>
<summary><b>Phase 3: Tailwind + shadcn/ui</b></summary>

### 사용할 도구
- **Bash**: `npm install`, `npx shadcn-ui@latest`
- **Write**: `tailwind.config.js`, `src/index.css`

### 체크리스트
```bash
# 1. Tailwind CSS 설치
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p

# 2. shadcn/ui 초기화
npx shadcn-ui@latest init

# 3. 17개 컴포넌트 설치
npx shadcn-ui@latest add button
npx shadcn-ui@latest add dialog
npx shadcn-ui@latest add table
npx shadcn-ui@latest add input
# ... (나머지 13개)

# 4. React Router 설치
npm install react-router-dom
```

### Git Push 타이밍
- ✅ shadcn/ui 컴포넌트 정상 렌더링
- ✅ Tailwind CSS 적용 확인

</details>

<details>
<summary><b>Phase 4: firestoreService + RecordContext</b></summary>

### 참고 파일 ⭐⭐⭐
- `baseball-firebase/src/services/firestoreService.js` (핵심!)
- `baseball-firebase/src/contexts/GameContext.jsx`

### 사용할 도구
- **Task(Explore)**: firestoreService 패턴 분석
- **Read**: 위 2개 파일 정독
- **Write**: `src/services/firestoreService.js`, `src/contexts/RecordContext.jsx`

### 체크리스트
1. **firestoreService.js 작성**
   ```javascript
   class FirestoreService {
     getUserCollection(collectionName) { ... }
     createClass(classData) { ... }
     createStudent(studentData) { ... }
     createRecord(recordData) { ... }
     subscribeToRecords(callback) { ... }
   }
   ```

2. **RecordContext.jsx 작성**
   ```javascript
   const RecordContext = createContext();

   export function RecordProvider({ children }) {
     const [classes, setClasses] = useState([]);
     const [students, setStudents] = useState([]);
     const [records, setRecords] = useState([]);
     // ...
   }
   ```

3. **App.jsx 래핑**
   ```javascript
   <AuthProvider>
     <RecordProvider>
       <BrowserRouter>
         <Routes>...</Routes>
       </BrowserRouter>
     </RecordProvider>
   </AuthProvider>
   ```

### Git Push 타이밍
- ✅ Firebase에 더미 데이터 저장 성공
- ✅ 실시간 리스너 동작 확인

</details>

<details>
<summary><b>Phase 5: 학급/학생 관리 UI</b></summary>

### 참고 파일
- `baseball-firebase/src/components/ClassTeamManagementView.jsx`
- `baseball-firebase/src/components/AddPlayerModal.jsx`
- `baseball-firebase/src/utils/studentCodeGenerator.js`

### 사용할 도구
- **Task(Explore)**: 드래그앤드롭 패턴 분석
- **Bash**: `npm install @dnd-kit/core @dnd-kit/sortable`
- **Write**: `ClassStudentManagementView.jsx`, `AddStudentModal.jsx`

### 구현 순서
1. DnD Kit 설치
2. ClassStudentManagementView.jsx 작성
3. AddStudentModal.jsx 작성
4. StudentCodeListModal.jsx 작성
5. studentCodeGenerator.js 복사

### Git Push 타이밍
- ✅ 학급 생성/수정/삭제 동작
- ✅ 학생 추가/삭제 동작
- ✅ 학생 코드 발급 확인

</details>

<details>
<summary><b>Phase 6: 종목 관리 + 세션 관리</b></summary>

### 새로 작성 (baseball-firebase에 없음)

### 사용할 도구
- **Write**: `EventManagementView.jsx`, `SessionManagementView.jsx`

### 기본 종목 16개 정의
```javascript
const DEFAULT_EVENTS = [
  // 개인전
  { id: 'individual_basic', name: '기본뛰기 (30초)', duration: 30 },
  { id: 'individual_run', name: '달리기뛰기 (30초)', duration: 30 },
  { id: 'individual_backward', name: '뒤로뛰기 (30초)', duration: 30 },
  { id: 'individual_cross', name: '교차뛰기 (30초)', duration: 30 },
  { id: 'individual_double', name: '2단뛰기 (30초)', duration: 30 },
  { id: 'individual_endurance_1min', name: '오래뛰기 (1분)', duration: 60 },
  { id: 'individual_endurance_3min', name: '오래뛰기 (3분)', duration: 180 },

  // 짝뛰기
  { id: 'pair_basic', name: '짝 기본뛰기 (30초)', duration: 30 },
  { id: 'pair_run', name: '짝 달리기뛰기 (30초)', duration: 30 },

  // 단체줄
  { id: 'group_8jump', name: '8자뛰기 (2분)', duration: 120 },
  { id: 'group_long', name: '긴줄뛰기 (2분)', duration: 120 },
  { id: 'group_double_dutch', name: '더블더치 (2분)', duration: 120 },

  // 자유형
  { id: 'freestyle', name: '자유연기 (1분)', duration: 60 },
  { id: 'relay', name: '계주뛰기 (3분)', duration: 180 },
  { id: 'creative', name: '창작뛰기 (2분)', duration: 120 },
  { id: 'timed_challenge', name: '시간제한 도전 (5분)', duration: 300 },
];
```

### Git Push 타이밍
- ✅ 종목 생성/수정 동작
- ✅ 세션 생성 (연습/대회 구분) 확인

</details>

<details>
<summary><b>Phase 7: 기록 시스템 (핵심!)</b></summary>

### 참고 파일
- `baseball-firebase/src/components/GameScreen.jsx` (구조만 참고)

### 사용할 도구
- **Task(Plan)**: RecordScreen 설계 계획 수립
- **Write**: `RecordScreen.jsx`, `RecordEndModal.jsx`

### 타이머 시스템 설계
```javascript
// 타이머 상태
const TIMER_STATES = {
  READY: 'ready',           // 준비 (3초 카운트다운)
  COUNTDOWN: 'countdown',   // 시작 카운트다운 (3, 2, 1)
  RUNNING: 'running',       // 진행 중
  PAUSED: 'paused',         // 일시정지
  FINISHED: 'finished'      // 종료
};

// 타이머 흐름
// READY (3초) → COUNTDOWN (3, 2, 1) → RUNNING → FINISHED

// 상태 관리
const [timerState, setTimerState] = useState(TIMER_STATES.READY);
const [elapsedTime, setElapsedTime] = useState(0);
const [jumpCount, setJumpCount] = useState(0);
const [consecutiveCount, setConsecutiveCount] = useState(0);
```

### 카운터 입력 UI
```javascript
// 버튼 레이아웃
[  -10  ] [  -1  ] [ 성공 +1 ] [  +10  ]
[       실패       ] [    라운드 종료    ]
```

### 전체화면 모드
- 타이머 대형 표시 (체육관에서 학생들이 볼 수 있게)
- ESC 키로 전체화면 종료

### Git Push 타이밍
- ✅ 타이머 정확히 작동
- ✅ 카운터 입력 동작
- ✅ 전체화면 모드 동작
- ✅ 기록 Firebase 저장 확인

</details>

<details>
<summary><b>Phase 8: 배지 시스템</b></summary>

### 참고 파일 (모두 그대로 복사 후 수정)
- `baseball-firebase/src/utils/badgeSystem.js` ⭐
- `baseball-firebase/src/utils/autoBadgeChecker.js`
- `baseball-firebase/src/components/BadgeManagementModal.jsx`
- `baseball-firebase/src/components/BadgeCreator.jsx`

### 사용할 도구
- **Read**: 위 4개 파일
- **Write**: `src/utils/badgeSystem.js` (JumpRope용 배지 15개)

### JumpRope용 배지 15개 예시
```javascript
export const JUMPROPE_BADGES = {
  FIRST_RECORD: {
    id: 'first_record',
    name: '첫 도전',
    icon: '🎽',
    tier: BADGE_TIERS.BEGINNER,
    description: '첫 기록 도전!',
    condition: (stats) => stats.totalRecords >= 1
  },

  JUMPS_50: {
    id: 'jumps_50',
    name: '50개 돌파',
    icon: '🏃',
    tier: BADGE_TIERS.BEGINNER,
    description: '50개 성공!',
    condition: (stats) => stats.totalJumps >= 50
  },

  CONSECUTIVE_30: {
    id: 'consecutive_30',
    name: '연속 30',
    icon: '🔥',
    tier: BADGE_TIERS.SKILLED,
    description: '30회 연속 성공!',
    condition: (stats) => stats.consecutiveMax >= 30
  },

  // ... (나머지 12개)
};
```

### Git Push 타이밍
- ✅ 자동 배지 수여 동작
- ✅ 커스텀 배지 생성 동작
- ✅ 수동 배지 수여 동작
- ✅ 배지 획득 축하 팝업 확인

</details>

<details>
<summary><b>Phase 9: 통계 & 차트</b></summary>

### 참고 파일
- `baseball-firebase/src/components/StatsView.jsx`
- `baseball-firebase/src/utils/statsCalculator.js`
- `baseball-firebase/src/utils/mvpCalculator.js`

### 사용할 도구
- **Task(Explore)**: 통계 계산 로직 분석
- **Bash**: `npm install chart.js react-chartjs-2` 또는 `recharts`
- **Write**: `StatsView.jsx`, `jumpropeStatsCalculator.js`

### 통계 가중치 변경
```javascript
// Baseball MVP 가중치
const MVP_WEIGHTS = {
  single: 1,
  homerun: 5,
  runs: 2
};

// JumpRope 점수 가중치
const JUMPROPE_WEIGHTS = {
  totalJumps: 1,
  consecutiveMax: 2,
  improvement: 3,
  teamwork: 1
};
```

### Git Push 타이밍
- ✅ 개인 통계 표시
- ✅ 학급 통계 표시
- ✅ 차트 렌더링
- ✅ CSV 다운로드 동작

</details>

<details>
<summary><b>Phase 10: 학생 뷰 + 배포</b></summary>

### 참고 파일
- `baseball-firebase/src/contexts/StudentAuthContext.jsx` (그대로 복사)
- `baseball-firebase/src/components/StudentView.jsx`

### 사용할 도구
- **Read**: 위 2개 파일
- **Write**: `StudentView.jsx`
- **Bash**: `npm run build`, Netlify 배포

### 학생 로그인 흐름
```javascript
// 1. 학생이 코드 입력 (예: abc123-456789)
// 2. CollectionGroup 쿼리로 전체 students 컬렉션 검색
// 3. 학생 정보 + 기록 조회
// 4. StudentView 렌더링
```

### Netlify 배포
```bash
# 1. 빌드 테스트
npm run build

# 2. netlify.toml 주석 해제
# [build]
#   command = "npm run build"
#   publish = "dist"

# 3. Git Push
git add .
git commit -m "feat: v20 JumpRope Master 완성"
git push origin feature/jumprope-master

# 4. Netlify Dashboard
# - Environment Variables 설정
# - Build & Deploy 확인
```

### Git Push 타이밍
- ✅ 학생 로그인 동작
- ✅ 학생 뷰 정상 렌더링
- ✅ Netlify 배포 성공
- ✅ **최종 배포 URL 확인!**

</details>

---

## 📊 Development Progress Tracker

### Phase별 완료 현황
```
Phase 1:  프로젝트 초기화         [ ] 0%
Phase 2:  Firebase 설정 + 인증    [ ] 0%
Phase 3:  Tailwind + shadcn/ui    [ ] 0%
Phase 4:  Service + Context       [ ] 0%
Phase 5:  학급/학생 관리 UI       [ ] 0%
Phase 6:  종목/세션 관리          [ ] 0%
Phase 7:  기록 시스템 (타이머)    [ ] 0%  ⭐ 핵심!
Phase 8:  배지 시스템             [ ] 0%
Phase 9:  통계 & 차트             [ ] 0%
Phase 10: 학생 뷰 + 배포          [ ] 0%
```

### 전체 진행률
```
전체: 0/10 Phase 완료 (0%)
```

### 주요 마일스톤 체크리스트
- [ ] M1: Google 로그인 성공 (Phase 2)
- [ ] M2: Firebase CRUD 동작 (Phase 4)
- [ ] M3: 학생 코드 발급 (Phase 5)
- [ ] M4: 타이머 시스템 완성 (Phase 7) ⭐
- [ ] M5: 배지 자동 수여 (Phase 8)
- [ ] M6: 통계 화면 완성 (Phase 9)
- [ ] M7: 학생 로그인 동작 (Phase 10)
- [ ] M8: Netlify 배포 완료 (Phase 10)

---

## 📖 Documentation

### 필수 문서
- [JUMPROPE_MASTER_PLAN.md](./docs/JUMPROPE_MASTER_PLAN.md): 전체 개발 계획
- README.md: 프로젝트 개요 및 사용 방법
- CLAUDE.md: 이 파일 (Claude 지침)

### 개발 시 추가 문서 (선택)
- UI_MOCKUPS.md: UI 스크린샷 및 설명
- DATABASE_SCHEMA.md: Firebase 스키마 상세
- IMPLEMENTATION_GUIDE.md: 구현 가이드

---

## ⚙️ Special Considerations

### Baseball-Firebase와의 차이점
1. **종목**: 야구(9이닝) → 줄넘기(16종목)
2. **점수**: 타격 결과 → 개수/시간 카운트
3. **타이머**: 없음 → 핵심 기능 (30초, 1분, 3분 등)
4. **팀 구성**: 고정 → 개인/짝/단체 혼합

### 유지할 패턴
- Firebase 데이터 구조
- Context API 사용
- shadcn/ui 컴포넌트
- 배지 시스템 로직
- 학생 코드 시스템

### 새로 구현할 것
- 타이머 시스템 (핵심!)
- 카운터 입력 UI
- 종목별 설정 관리
- 연습/대회 구분

---

## 🤖 Notes for Claude Code

### 작업 방식
1. **소크라테스적 대화**: 질문을 통한 이해도 확인
2. **점진적 설명**: 단계별로 난이도 상승
3. **비유 활용**: 기술 개념을 쉽게 설명
4. **메타인지**: 전체 맥락 먼저, 세부 사항 나중

### 커뮤니케이션
- 용어 설명 필수 (IT 용어, 약어 등)
- "왜 이렇게 해야 하는지" 이유 설명
- 복잡한 개념은 비유로 설명
- 시간적 맥락: 2025년 기준 최신 정보

### 코딩 지원
- 코드 작성 전 설명 먼저
- 주요 로직에 주석 추가
- 오류 발생 시 원인 분석 후 수정
- 대안이 있으면 여러 옵션 제시

### 프로젝트 관리
- TODO 리스트 적극 활용
- 진행 상황 체계적 관리
- 마일스톤 단위 확인
- 피드백 즉시 반영

---

## 🎯 Success Criteria

### 기능적 요구사항
- [ ] 교사가 학급/학생을 관리할 수 있다
- [ ] 연습과 대회를 구분하여 진행할 수 있다
- [ ] 타이머로 시간을 측정하고 기록을 입력할 수 있다
- [ ] 배지가 자동으로 수여된다
- [ ] 통계와 순위를 확인할 수 있다
- [ ] 학생이 자신의 기록을 확인할 수 있다

### 비기능적 요구사항
- [ ] 모바일/태블릿에서 원활하게 작동
- [ ] 3초 이내 페이지 로드
- [ ] 직관적인 UI/UX
- [ ] Firebase 비용 월 10달러 이내

---

## 📞 Contact & Support

### 개발자
- **이름**: 이원근
- **직업**: 초등교사 + 대학원생
- **전문**: 체육 교육, AI 활용

### 관련 프로젝트
- ACE PE Canvas: 체육 수업 설계 웹앱
- baseball-firebase: 필드형 게임 마스터 보드
- 블로그/브런치: AI 시대 교사 살아남기

---

**Version**: 3.0
**Last Updated**: 2025-01-18
**Status**: v20 워크플로우 & 10-Phase 로드맵 완성, 개발 준비 완료
