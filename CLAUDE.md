# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is an Astro-based blog site for Korean food content. Built using the Astro Blog starter template with static site generation, content collections, and SEO features.

## Development Commands

```bash
npm run dev        # Start dev server at localhost:4321
npm run build      # Build production site to ./dist/
npm run preview    # Preview production build locally
npm run astro ...  # Run Astro CLI commands (e.g., astro add, astro check)
```

## Architecture

### Content Collections System

The project uses Astro's Content Collections API for type-safe blog content management:

- **Collection Definition**: `src/content.config.ts` defines the `blog` collection with a Zod schema
- **Content Location**: All blog posts live in `src/content/blog/` as `.md` or `.mdx` files
- **Schema**: Posts require `title`, `description`, `pubDate`, and optional `updatedDate` and `heroImage`
- **Retrieval**: Use `getCollection('blog')` to fetch posts, `render()` to get content

### Routing & Pages

- **File-based routing**: Files in `src/pages/` become routes (e.g., `about.astro` → `/about`)
- **Dynamic routes**: `src/pages/blog/[...slug].astro` handles all blog post pages using `getStaticPaths()`
- **RSS feed**: `src/pages/rss.xml.js` generates RSS using `@astrojs/rss`

### Global Configuration

- **Site constants**: `src/consts.ts` exports `SITE_TITLE` and `SITE_DESCRIPTION` - update these for site-wide changes
- **Astro config**: `astro.config.mjs` configures MDX and sitemap integrations, and sets `site` URL

### Component Structure

- **Layouts**: `src/layouts/BlogPost.astro` wraps individual blog posts
- **Components**: `src/components/` contains reusable UI components (Header, Footer, BaseHead, etc.)

### Static Assets

Place images and other static files in `public/` - they're served at the root path.

## Adding New Blog Posts

Create a new `.md` or `.mdx` file in `src/content/blog/` with required frontmatter:

```markdown
---
title: 'Post Title'
description: 'Post description'
pubDate: 2026-02-25
heroImage: '/image.jpg' # optional
---

Post content here...
```

The post will automatically appear on the blog index and generate a route at `/blog/filename/`.

## Integrations

- **@astrojs/mdx**: Enables MDX support for interactive content
- **@astrojs/sitemap**: Auto-generates sitemap.xml
- **@astrojs/rss**: Powers the RSS feed at `/rss.xml`
- **sharp**: Image optimization (required by Astro)

---

## 한식 블로그 자동 작성 규칙

이 블로그는 수익화를 목적으로 하는 한식(Korean Food) 전문 블로그입니다.

### 블로그 글 작성 규칙

사용자가 **"새 글 작성"** 이라고 말하면, 다음 규칙에 따라 자동으로 새로운 블로그 포스트를 작성합니다:

#### 1. 파일 형식
- `src/content/blog/` 디렉토리에 `.md` (마크다운) 형식으로 작성
- 파일명: 주제를 나타내는 영문 slug (예: `kimchi-jjigae-recipe.md`, `bibimbap-guide.md`)

#### 2. 콘텐츠 요구사항
- **최소 길이**: 5,000자 이상
- **주제**: 매번 새로운 한식 관련 주제 (중복 금지)
- **말투**: 자연스럽고 사람이 쓴 것 같은 문체 (AI 느낌 최소화)
- **SEO 최적화**:
  - 제목에 핵심 키워드 포함
  - 메타 설명(description)은 150-160자로 작성
  - 소제목(## h2, ### h3) 적극 활용
  - 자연스러운 키워드 배치
  - 내부 링크 및 외부 링크 포함

#### 3. 이미지 요구사항
- **최소 1개 이상** 한식 관련 이미지 삽입
- 이미지 소스: Unsplash (https://unsplash.com)
- 이미지 검색 키워드: 해당 글의 한식 주제 관련
- 마크다운 이미지 문법 사용: `![설명](이미지URL)`
- 각 이미지에 적절한 alt 텍스트 작성 (SEO)

#### 4. Frontmatter 작성
```markdown
---
title: 'SEO 최적화된 제목 (한글)'
description: '150-160자 분량의 매력적인 설명'
pubDate: YYYY-MM-DD (작성 당일 날짜)
heroImage: 'Unsplash 이미지 URL'
---
```

#### 5. 글 구조 예시
```markdown
# 제목 (H1은 자동 생성되므로 본문에서는 H2부터 시작)

서론 - 독자의 관심을 끄는 도입부

## 첫 번째 소제목
내용...

![한식 이미지](unsplash-url)

## 두 번째 소제목
내용...

## 세 번째 소제목
내용...

## 결론
마무리 및 독자 액션 유도
```

#### 6. 추천 주제 예시
- 한식 레시피 (김치찌개, 불고기, 떡볶이 등)
- 한식 재료 소개 (고추장, 된장, 김치 등)
- 한식 문화 (밥상 차림, 식사 예절 등)
- 한식당 추천
- 한식의 건강 효능
- 계절별 한식 추천
- 지역별 향토 음식

### 작업 흐름

1. 사용자가 "새 글 작성" 명령
2. 아직 다루지 않은 새로운 한식 주제 선정
3. Unsplash에서 적절한 이미지 검색
4. 5,000자 이상의 자연스러운 글 작성
5. SEO 최적화된 frontmatter 작성
6. `src/content/blog/주제-slug.md` 파일 생성
7. 작성 완료 알림

### 주의사항
- 기존에 작성한 주제와 중복되지 않도록 체크
- 자연스러운 한국어 문체 유지 (과도한 경어 지양, 친근한 톤)
- 문단을 적절히 나눠서 가독성 확보
- 전문 용어는 쉽게 풀어서 설명
- 실용적이고 유용한 정보 제공
