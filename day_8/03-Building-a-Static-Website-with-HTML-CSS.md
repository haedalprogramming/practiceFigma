<img src="./header.png" />

# 3. HTML/CSS 기반의 정적 웹사이트 구축

> [!NOTE]
> 이 페이지에서는 Figma로 디자인한 시안을 바탕으로, **HTML과 CSS**만을 사용하여 **정적 웹사이트(Static Website)**를 실제로 구축하는 방법을 학습합니다. `Day 4`에서 HTML과 CSS의 기본적인 문법과 사용법을 익혔다면, 여기서는 웹 표준을 준수하고, 효율적인 코드 작성 습관을 기르며, 실제 웹사이트를 완성하는 데 필요한 실용적인 지식에 중점을 둡니다.

## 3.1. 정적 웹사이트란?

정적 웹사이트는 서버에 미리 저장된 HTML, CSS, JavaScript 파일들을 사용자의 요청이 있을 때 **그대로 전달**하는 방식의 웹사이트입니다. 데이터베이스 연동이나 서버 측 로직 없이, 모든 콘텐츠가 미리 준비되어 있습니다.

### 정적 웹사이트의 특징

-   **빠른 로딩 속도**: 서버에서 별도의 처리 없이 파일을 바로 전달하므로 로딩 속도가 빠릅니다.
-   **높은 보안성**: 서버 측 코드가 없으므로 서버 해킹 등의 보안 위협이 적습니다.
-   **저렴한 호스팅 비용**: 복잡한 서버 환경이 필요 없어 호스팅 비용이 저렴하거나 무료인 경우가 많습니다.
-   **간단한 배포**: 파일을 서버에 업로드하는 것만으로 배포가 가능합니다.
-   **제한된 기능**: 사용자 상호작용이나 동적인 데이터 처리가 필요한 복잡한 웹 애플리케이션에는 적합하지 않습니다.

### 적합한 용도

-   개인 포트폴리오, 블로그, 회사 소개 페이지, 이벤트 페이지, 랜딩 페이지 등 콘텐츠 변경이 잦지 않은 웹사이트.

## 3.2. 개발 프로세스

Figma 시안을 실제 코드로 옮기는 과정은 다음과 같습니다.

### 1. HTML 구조화 (Semantic HTML)

시안의 레이아웃과 콘텐츠를 바탕으로 웹 표준에 맞는 HTML 구조를 작성합니다. 이때 **시맨틱(Semantic) 태그**를 사용하여 각 요소의 의미를 명확히 하는 것이 중요합니다.

-   `<header>`, `<nav>`, `<main>`, `<section>`, `<article>`, `<footer>` 등
-   `<div>`와 `<span>`은 의미 없는 컨테이너로 사용하고, 가능한 한 시맨틱 태그를 활용합니다.

**예시:**

```html
<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>나의 포트폴리오</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>

  <header class="main-header">
    <nav class="main-nav">
      <!-- 네비게이션 링크 -->
    </nav>
  </header>

  <main class="main-content">
    <section class="hero-section">
      <!-- 히어로 섹션 내용 -->
    </section>

    <section class="portfolio-section">
      <h2>나의 작업물</h2>
      <div class="portfolio-grid">
        <!-- 포트폴리오 아이템 -->
      </div>
    </section>
  </main>

  <footer class="main-footer">
    <!-- 푸터 내용 -->
  </footer>

</body>
</html>
```

### 2. CSS 스타일링 (Layout & Design)

작성된 HTML 구조에 Figma 시안의 디자인을 입힙니다. 레이아웃, 색상, 폰트, 간격, 반응형 디자인 등을 구현합니다.

-   **레이아웃**: Flexbox 또는 CSS Grid를 사용하여 유연하고 반응형인 레이아웃을 만듭니다.
-   **색상/폰트**: Figma에서 정의한 색상 팔레트와 폰트 스타일을 CSS 변수로 관리하여 적용합니다.
-   **간격**: `margin`과 `padding`을 사용하여 요소 간의 적절한 간격을 유지합니다.
-   **반응형 디자인**: 미디어 쿼리(`@media`)를 사용하여 다양한 화면 크기에 대응합니다.

**예시:**

```css
/* CSS 변수 정의 */
:root {
  --primary-color: #007bff;
  --text-color: #333;
  --bg-color: #f4f4f4;
}

body {
  font-family: 'Noto Sans KR', sans-serif;
  color: var(--text-color);
  background-color: var(--bg-color);
}

.main-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1rem 2rem;
  background-color: #fff;
}

.portfolio-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); /* 반응형 그리드 */
  gap: 20px;
  padding: 20px;
}

/* 모바일 반응형 */
@media (max-width: 768px) {
  .main-header {
    flex-direction: column;
  }
}
```

### 3. 이미지 및 미디어 최적화

웹사이트의 성능에 큰 영향을 미치는 이미지와 비디오 같은 미디어 파일들을 최적화합니다.

-   **압축**: 이미지 압축 도구를 사용하여 파일 크기를 줄입니다.
-   **포맷**: WebP와 같은 최신 이미지 포맷을 고려합니다.
-   **반응형 이미지**: `srcset` 속성이나 `<picture>` 태그를 사용하여 다양한 해상도에 맞는 이미지를 제공합니다.

### 4. 웹 호스팅을 통한 배포

완성된 정적 웹사이트는 Netlify, Vercel, GitHub Pages 등 다양한 정적 웹사이트 호스팅 서비스를 통해 쉽게 배포할 수 있습니다.

-   **Netlify/Vercel**: Git 저장소와 연동하여 코드를 푸시할 때마다 자동으로 배포되는 CI/CD(Continuous Integration/Continuous Deployment) 기능을 제공합니다.
-   **GitHub Pages**: GitHub 저장소의 특정 브랜치(예: `main` 또는 `gh-pages`)에 HTML, CSS, JS 파일을 올리는 것만으로 웹사이트를 호스팅할 수 있습니다.

이러한 과정을 통해 Figma에서 구상했던 디자인을 실제 웹사이트로 구현하고, 전 세계 어디서든 접근할 수 있도록 배포할 수 있습니다.