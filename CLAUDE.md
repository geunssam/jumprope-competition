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

**Version**: 2.0
**Last Updated**: 2025-01-17
**Status**: v20 개발 계획 완료, 개발 대기 중
