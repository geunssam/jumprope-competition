# 줄넘기 마스터 (JumpRope Master)

학교 줄넘기 연습 및 대회를 위한 종합 관리 시스템

---

## 🎯 프로젝트 상태

### 현재 버전
- **v19 (레거시)**: 단일 HTML 파일 - 현재 Netlify 배포 중
- **v20 (개발 중)**: JumpRope Master - React + Firebase 기반 대규모 업그레이드

### 배포 정보
- **URL**: https://jumpropecompetition.netlify.app
- **현재 배포**: v19 (index.html)
- **다음 배포**: v20 (JumpRope Master)

---

## 📁 프로젝트 구조

```
jumprope-competition/
├── index.html              # v19 레거시 버전 (현재 배포 중)
├── netlify.toml            # Netlify 배포 설정
├── .gitignore
├── README.md               # 이 파일
├── CLAUDE.md               # Claude Code 프로젝트 지침
└── docs/
    └── JUMPROPE_MASTER_PLAN.md    # v20 전체 개발 계획
```

---

## 🚀 v20 주요 업그레이드

### v19 → v20 비교

| 항목 | v19 (레거시) | v20 (JumpRope Master) |
|------|-------------|----------------------|
| **아키텍처** | 단일 HTML 파일 | React 19 + Vite + Firebase |
| **데이터** | LocalStorage | Firestore (클라우드) |
| **규모** | 1개 파일 (188KB) | 50+ 컴포넌트 시스템 |
| **사용자** | 교사만 | 교사 + 학생 분리 |
| **기록 관리** | 일회성 대회 | 일상 연습 + 대회 누적 |
| **배지** | 없음 | 자동 15개 + 커스텀 |
| **통계** | 간단한 순위 | 다층 통계 (개인/팀/학급) |
| **공유** | 없음 | 교사 간 협업 가능 |

### 핵심 기능 (v20)

#### 1. 학급/학생 관리
- 학년별 학급 생성 및 관리
- 학생 일괄/개별 등록
- 학생 코드 자동 발급 시스템

#### 2. 종목 관리
- 기본 종목 16개 (개인전, 단체전)
- 커스텀 종목 무제한 추가
- 종목별 설정 (시간, 점수 방식)

#### 3. 연습/대회 통합 운영
- 연습 모드 & 대회 모드
- 실시간 진행 현황
- 참가자 자동 배정

#### 4. 기록 입력 시스템
- 고급 타이머 (준비→카운트다운→진행)
- 카운터 입력 (+1, +10, -1, -10)
- 전체화면 타이머 모드
- 실시간 배지 수여 알림

#### 5. 통계 & 순위
- 개인/팀/학급 다층 통계
- 실시간 순위 업데이트
- 차트 및 그래프
- CSV 다운로드

#### 6. 배지 시스템
- 자동 배지 15개 (첫 기록, 마일스톤 등)
- 커스텀 배지 생성/수여
- 배지 도감 및 진행도
- 배지 획득 축하 애니메이션

#### 7. 학생 뷰
- 학생 코드 로그인
- 개인 기록 조회
- 배지 컬렉션
- 순위 확인

---

## 💻 기술 스택

### v19 (레거시)
- React 18 (CDN)
- Tailwind CSS (CDN)
- Font Awesome
- LocalStorage

### v20 (JumpRope Master)
- **Frontend**: React 19 + Vite + React Router
- **Backend**: Firebase (Auth + Firestore)
- **UI**: Tailwind CSS + shadcn/ui
- **Charts**: Chart.js / Recharts
- **Deployment**: Netlify

---

## 📖 문서

### 개발 계획
자세한 개발 계획은 [JUMPROPE_MASTER_PLAN.md](./docs/JUMPROPE_MASTER_PLAN.md) 참조

### 주요 섹션
- 프로젝트 개요
- 전체 화면 구조 (7개 메인 섹션)
- 상세 UI 설계
- Firebase 데이터 구조
- 컴포넌트 구조
- 4주 개발 로드맵

---

## 🔧 개발 환경 설정 (v20)

### 필수 요구사항
- Node.js 20+
- npm 또는 yarn
- Firebase 계정

### 초기 설정
```bash
# 의존성 설치 (개발 시작 시)
npm install

# 개발 서버 실행
npm run dev

# 프로덕션 빌드
npm run build

# 빌드 미리보기
npm run preview
```

### 환경 변수
`.env.local` 파일 생성:
```
VITE_FIREBASE_API_KEY=your_api_key
VITE_FIREBASE_AUTH_DOMAIN=your_auth_domain
VITE_FIREBASE_PROJECT_ID=your_project_id
VITE_FIREBASE_STORAGE_BUCKET=your_storage_bucket
VITE_FIREBASE_MESSAGING_SENDER_ID=your_sender_id
VITE_FIREBASE_APP_ID=your_app_id
```

---

## 📅 개발 로드맵

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

### Week 4: 학생 뷤 + 최적화
- 학생 로그인 및 뷰
- 반응형 디자인 최적화
- 성능 최적화 및 배포

---

## 🎯 사용 방법

### v19 (현재 배포 버전)
1. https://jumpropecompetition.netlify.app 접속
2. 대회 설정에서 학년, 반, 종목 설정
3. 선수 명단 입력
4. 경기 진행 및 점수 기록
5. 결과 발표

### v20 (개발 예정)
1. Google 계정으로 로그인
2. 학급/학생 등록
3. 연습 또는 대회 시작
4. 타이머로 기록 입력
5. 실시간 통계 및 배지 확인

---

## 📱 지원 환경

- 모바일/태블릿/데스크톱 반응형 지원
- **아이패드 터치 최적화**
  - 드래그앤드랍 터치 지원
  - 터치 타겟 최소 크기 44px
  - 터치 피드백 및 시각적 효과
- 최신 Chrome, Safari, Edge 브라우저 지원

---

## 🤝 기여 및 피드백

### 문의
프로젝트 관련 문의는 `CLAUDE.md` 파일 참조

### 개발 참고
- **아키텍처 기반**: baseball-firebase 프로젝트
  - 위치: `/Users/iwongeun/Desktop/필드형게임 마스터 보드/baseball-firebase`
- **디자인 철학**: 미니멀리즘, 세밀한 정렬, 터치 최적화

---

## 📝 라이선스

교육용 프로젝트입니다.

---

**개발**: 초등교사 개발자 이원근
**현재 버전**: v19 (레거시)
**개발 중**: v20 (JumpRope Master)
**최종 수정**: 2025-01-17
