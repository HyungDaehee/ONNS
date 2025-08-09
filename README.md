# 옷늘날씨 (ONNS)
<img width="300" height="300" alt="Icon" src="https://github.com/user-attachments/assets/3d475598-9fcc-40f4-8981-2e5e1359db6b" />

> “오늘 날씨 뭐 입지?”  
> 실시간 체감온도와 사용자들의 옷차림 데이터를 기반으로  
> 기온별 코디를 공유하고 참고할 수 있는 날씨 OOTD 커뮤니티입니다.<br><br>

> 개발기간 : 2025.07.01 ~ 2025.07.21<br>
> 배포 URL : https://onns.vercel.app

---

## 목차
- [프로젝트 목표](#프로젝트-목표)  
  - [사용자 관점](#사용자-관점)  
  - [개발자 관점](#개발자-관점)  
- [팀원 소개](#팀원-소개)
- [기술 스택](#기술-스택)  
- [핵심 기능 요약](#핵심-기능-요약)  
- [디렉토리 구조](#디렉토리-구조)  
- [설치 및 실행](#설치-및-실행)  
- [환경 변수](#환경-변수)  
- [API 문서](#api-문서)  


---

## 프로젝트 목표

> **“기온과 체감온도에 따라 사람들이 실제로 입은 옷차림을 공유하고 참고할 수 있는 커뮤니티”** 를 구현합니다.

### 사용자 관점
- 오늘 날씨에 맞는 **실제 코디**를 쉽게 참고  
- 사람들의 옷차림 데이터를 통해 **기온별 스타일 레퍼런스** 구축  
- **체감온도와 실제 옷차림의 간극**을 줄이는 서비스 제공  

### 개발자 관점
- **협업과 유지보수가 용이한 구조** (Clean Architecture, Git Flow) 적용 학습  
- **Next.js 15 / TypeScript / Tailwind CSS / Supabase** 핵심 기술 역량 강화  
- **PR 리뷰, Issue 기반 작업 분배** 등 팀 개발 워크플로우 경험  
- Figma 디자인 시안과 **동일한 UI** 구현 및 **REST API 명세** 문서화  

---

## 팀원 소개
| 이름        | GitHub         | 역할                    |
| -----------|----------------|----------------------- |
| 송가은    | gn-ioeo   | 로그인 기능 / 회원 관리(생성,삭제)/ 알림 기능 / 좋아요 기능  |
| 송진호    | jaino-song    | 마이페이지 / 게시글 조건 조회 / API 설계  | 회원관리 (수정, 조회)
| 신주현    | Shin363   | 메인 페이지 / 댓글 관리 기능 / OpenWeather API, GeoLocation API 도입   |
| 형대희    | HyungDaehee   | OOTD / 게시글 조회 기능 / 필터 기능 / 게시글 조회(상세), 삭제 기능    |

---

## 기술 스택

| 영역          | 사용 기술                                                        |
| --------------------------------------------------------------------------- | ----------------------------------------------------------------------------- |
| Frontend    | Next.js 15 (App Router), React, TypeScript, Tailwind CSS, Axios, Zustand                                                                       |
| Backend     | Supabase (PostgreSQL, Storage), OpenWeather API, GeoLocation API  |
| Styling     | Tailwind CSS                                                  |
| Dev Tools   | ESLint, Prettier, Husky, Commitlint, Git Flow                 |
| 배포         | Vercel                                                        |

---

## 핵심 기능 요약

| 시스템     | 주요 기능                                                                                                                   |
| ---------- | --------------------------------------------------------------------------------------------------------------------------- |
| 회원       | 가입, 로그인, 탈퇴                                                                                       |
| OOTD       | 게시글 작성·수정·삭제, 목록/상세 조회, 날씨 정보 표시, 정렬(최신/좋아요), 필터(계절/체감온도)                                      |
| 좋아요     | 등록/삭제, 내가 좋아요한 글 조회                                                                                             |
| 댓글       | 등록·조회·수정·삭제                                                                                                        |
| 날씨       | 외부 API 호출 → 체감온도 저장, 메인에 오늘 날씨 표시                                                                         |
| 마이페이지 | 내가 작성한 글 / 좋아요한 글 목록 / 프로필 조회 및 수정                                               |

---

## 디렉토리 구조

```plaintext
ONNS/
├── (backend)/                  # Clean Architecture 백엔드 레이어 (DTO, Use Cases 등)
├── .github/                    # GitHub 워크플로우 및 이슈 템플릿
├── .husky/                     # Git hooks
├── app/                        # Next.js App Router (페이지 및 컴포넌트)
│   ├── ootd/                   # OOTD 관련 페이지 및 컴포넌트
│   ├── mypage/                 # 마이페이지 컴포넌트
│   └── …  
├── hooks/                      # 커스텀 React Hooks
├── lib/                        # 공용 라이브러리 유틸
├── public/                     # 정적 자산 (이미지, 아이콘)
│   └── assets/
├── stores/                     # Zustand 전역 상태 관리
├── types/                      # TypeScript 타입 정의
├── utils/                      # Axios 인스턴스, API 헬퍼 함수
├── OOTD-Permissions-Test.postman_collection.json  # Postman API 컬렉션
├── next.config.ts              # Next.js 설정
├── middleware.ts               # Next.js 미들웨어
├── vercel.json                 # Vercel 배포 설정
├── package.json                # 종속성 및 스크립트 정의
└── tsconfig.json               # TypeScript 설정
```
---

## 개발한 페이지 및 기능
  ### [OOTD 페이지]
  - OOTD 페이지는 사용자들이 자신의 코디를 자유롭게 공유하고 소통할 수 있는 공간입니다.
  - 사용자는 현재 날씨에 맞는 옷차림을 더 정확히 찾기 위해 필터 기능을 사용할 수 있습니다.
<img width="500" height="700" alt="image" src="https://github.com/user-attachments/assets/5b40ffa2-f429-4b7e-b8a7-749cf8935734" />

  
- **계절별 필터 기능**
  - **봄·여름·가을·겨울**의 4계절로 나누어 **월별 분기**로 구분하였습니다.
  - ex) **봄**: 3월 ~ 5월, **여름**: 6월 ~ 8월, **가을**: 9월 ~ 11월, **겨울**: 12월 ~ 2월
  - 게시글의 **생성 월**을 기준으로, 해당 **월**이 속하는 **계절**에 따라 분류됩니다.
  - **기본값**으로 필터가 적용되며, **현재 월*** 기준으로 자동 적용됩니다. (ex)6,7,8월 → 여름)

 
- **온도별 필터 기능**
  - **세분화된 온도 범위** 제공 이를 통해 **해당 계절에 맞는 다양한 온도대의 코디 정보**를 구체적으로 확인 할 수 있습니다.
  - **계절의 상태**에 따라 기준 온도가 다르게 설정 됨
    - 봄 / 가을: 전체, 5–9, 10–14, 15–19
    - 여름: 전체, 20–24, 25–29, 30~
    - 겨울: 전체, 0–4, -5 ~ -1, ~(-6)
    - 기타(기본값): 전체

- **최신순 기능**
  - **모든 필터**가 **최신순 정렬**로 설정되어 있어, 가장 **최근**에 업로드된 **게시글**부터 확인할 수 있습니다

- **인기순 기능**
  - **사용자들**이 누른 **‘좋아요 수’** 를 기준으로 정렬
  - **좋아요 수**가 같은 **게시글**끼리는 **최신순**을 기준으로 다시 **정렬**되어 **가장 최근에 업로드된 게시글**부터 확인 할 수 있습습니다.
 
<br>

### [상세 페이지]
- **메인 페이지**와 **OOTD 페이지**에서 게시글이나 이미지를 클릭하면 해당 게시글의 **상세 페이지**로 이동합니다.
- 상세 페이지에서는 **작성자 이름과 프로필, 첨부 이미지, 좋아요 수, 댓글 수, 본문 내용, 댓글 및 대댓글**을 확인할 수 있습니다.
- **댓글 작성자 ID**와 **현재 사용자 ID**가 일치할 경우, 해당 댓글을 삭제할 수 있도록 구현하였습니다.


<br>



### [글 작성 기능]
- **우측 하단 플로팅 버튼** 클릭 시 **글 작성 페이지**로 이동합니다.
- **사용자 입력 항목**: 이미지(필수), 내용
- **자동 저장 항목**: 체감온도, 사용자 ID, 생성일

<br>

---

## 설치 및 실행

### 저장소 클론
```
git clone https://github.com/FRONT-END-BOOTCAMP-PLUS-5/ONNS.git
cd ONNS
```

### 의존성 설치
```
yarn install  # 또는 npm install
```

### 환경 변수 설정
> 루트에 .env.local 파일을 생성하고, 아래 값을 입력하세요.
```
NEXT_PUBLIC_SUPABASE_URL=your_supabase_url
NEXT_PUBLIC_SUPABASE_ANON_KEY=your_supabase_anon_key
WEATHER_API_KEY=your_openweather_api_key
```

### 개발 서버 실행
```
yarn dev  # 또는 npm run dev
```

###빌드 및 프로덕션 서버
```
yarn build && yarn start  # 또는 npm run build && npm start
```

## 환경 변수
| 변수 이름                     | 설명                                   |
| ----------------------------- | -------------------------------------- |
| NEXT_PUBLIC_SUPABASE_URL      | Supabase 프로젝트 URL                  |
| NEXT_PUBLIC_SUPABASE_ANON_KEY | Supabase 익명 키                       |
| WEATHER_API_KEY               | 외부 날씨 API (OpenWeather 등) 키      |


## API 문서
- Postman: ./OOTD-Permissions-Test.postman_collection.json
- 주요 엔드포인트:
    - GET /api/posts
    - POST /api/posts
    - PATCH /api/posts/:id
    - DELETE /api/posts/:id
    - POST /api/posts/:id/like
    - POST /api/posts/:id/comments
