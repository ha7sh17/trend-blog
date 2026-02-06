# Trend Blog

자동화된 트렌드 블로그 - Google Trends 기반 일일 포스팅

## 📍 URLs

- **Live Site:** https://trend-blog-313.pages.dev/
- **GitHub:** https://github.com/stegolab/trend-blog
- **Cloudflare Pages:** stegolab 계정

## 🛠 기술 스택

- **Static Site Generator:** Hugo (PaperMod 테마)
- **Hosting:** Cloudflare Pages (GitHub 연동, 자동 배포)
- **Automation:** Clawdbot Cron Jobs
- **Trend Source:** Google Trends RSS

## 📁 프로젝트 구조

```
~/Programming/trend-blog/
├── content/
│   ├── posts/           # 블로그 포스트 (MD 파일)
│   ├── archives.md      # 아카이브 페이지
│   ├── about.md         # About 페이지
│   └── privacy.md       # Privacy Policy
├── layouts/
│   └── index.html       # 커스텀 홈페이지 (달력 포함)
├── themes/
│   └── PaperMod/        # 테마 (git submodule)
├── hugo.toml            # Hugo 설정
└── scripts/
    └── post-template.md # 포스트 작성 가이드라인
```

## 🔄 자동화 플로우

### Cron Job 설정
- **Job ID:** `da75ccd3-3e8b-4ff2-8fb8-3174024722d5`
- **이름:** `trend-blog-daily`
- **실행 시간:** 매일 0시, 3시, 6시, 9시, 12시, 15시, 18시, 21시 (KST)
- **총 8회/일**

### 동작 순서
1. Google Trends RSS 피드 fetch (`https://trends.google.com/trending/rss?geo=US`)
2. 가장 흥미로운 키워드 선택 (스포츠, 엔터 우선)
3. 관련 뉴스 기사 2-3개 fetch
4. 800-1200 단어 포스트 작성
5. `content/posts/YYYY-MM-DD-keyword-slug.md` 저장
6. `draft: false`로 즉시 발행
7. Git commit & push
8. Cloudflare 자동 빌드/배포

## 📝 포스트 형식 (SEO 최적화)

```markdown
---
title: "키워드를 앞에 배치한 제목 (60자 이내)"
date: YYYY-MM-DD
draft: false
tags: ["keyword1", "keyword2", ...] # 5-7개
description: "키워드 포함, 150-160자, 핵심 요약"
---

본문 (1000-1500 단어)
```

### SEO 체크리스트
- [ ] **제목**: 키워드 앞쪽 배치, 60자 이내
- [ ] **Description**: 키워드 포함, 150-160자
- [ ] **첫 문단**: 키워드 자연스럽게 포함
- [ ] **H2 소제목**: 키워드 변형 포함 (3-5개)
- [ ] **본문**: 키워드 2-3% 밀도로 분산
- [ ] **FAQ 섹션**: "People Also Ask" 노출용 Q&A 2-3개
- [ ] **결론**: 키워드 다시 언급

### 포스트 구조
1. **Hook** - 왜 지금 트렌딩인지 (키워드 포함)
2. **Background** - 배경/맥락
3. **Current Situation** - 현재 상황 상세
4. **Analysis** - 분석/인사이트
5. **FAQ** - `## Frequently Asked Questions`
6. **Conclusion** - 요약 및 전망

## 🗓 홈페이지 레이아웃

- 상단: 미니 달력 (280px, 중앙 정렬)
  - 포스트 있는 날짜는 주황색 표시
  - 클릭하면 해당 날짜 포스트 목록 표시
- 하단: 포스트 목록 (제목 → 날짜/태그 → 요약)

## 🚀 수동 배포 방법

```bash
cd ~/Programming/trend-blog

# 새 포스트 작성 후
git add -A
git commit -m "Add post: [제목]"
git push

# Cloudflare가 자동으로 빌드/배포 (1-2분 소요)
```

## ⚙️ Cron Job 수정

```bash
# 목록 확인
clawdbot cron list

# 시간 변경 예시
clawdbot cron edit da75ccd3-3e8b-4ff2-8fb8-3174024722d5 --cron "0 9 * * *" --tz "Asia/Seoul"
```

또는 Clawdbot에게 직접 요청.

## 📊 AdSense 준비 상태

- [x] 콘텐츠 20개+ (하루 8개씩 누적 중)
- [x] About 페이지 (`/about/`)
- [x] Privacy Policy (`/privacy/`)
- [ ] 1-2주 운영 후 신청 예정

## 🔧 Hugo 명령어

```bash
# 로컬 서버 (미리보기)
hugo server -D

# 빌드
hugo

# 새 포스트 생성
hugo new posts/my-post.md
```

## ⚠️ 주의사항

1. **타임존:** 포스트 날짜는 UTC 기준. Cloudflare 빌드 시 미래 날짜는 빌드 안 됨.
2. **테마:** PaperMod는 git submodule로 관리됨.
3. **Cloudflare:** GitHub push 감지 → 자동 빌드. 실패 시 대시보드에서 Retry.

## 📞 문의

- **Discord:** ha7sh17.
- **Owner:** 신 (한신)

---

*Created: 2026-02-07*
*Last Updated: 2026-02-07*
