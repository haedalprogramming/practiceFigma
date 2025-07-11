<img src="./header.png" />

# 6. 실습 2: 전체 사이트에 테마 적용하기

> [!NOTE]
> 이 실습에서는 지금까지 `day_6`에서 배운 모든 개념(CSS 변수, `data-theme`, JavaScript 로직, `transition`)을 총동원하여, 조금 더 복잡한 구조를 가진 전체 웹사이트에 일관된 테마 시스템을 적용해 봅니다. 시맨틱 변수 설계를 통해 어떻게 유지보수하기 좋은 테마 시스템을 구축하는지 경험합니다.

## 6.1. 실습 목표

- 헤더, 메인 콘텐츠, 카드, 버튼, 폼 요소 등 다양한 컴포넌트로 구성된 웹사이트에 라이트/다크 테마를 적용합니다.
- 역할 기반의 시맨틱 CSS 변수를 체계적으로 설계하고 적용합니다.
- JavaScript를 사용하여 테마를 전환하고, 사용자의 선택을 유지합니다.
- 모든 색상 변경에 부드러운 `transition` 효과를 적용합니다.

## 6.2. HTML 구조

다양한 컴포넌트를 포함하는 예제 사이트의 HTML 구조입니다.

```html
<!DOCTYPE html>
<html lang="ko" data-theme="light">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>전체 사이트 테마 적용</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>

  <header class="site-header">
    <div class="logo">MySite</div>
    <nav>
      <a href="#">Home</a>
      <a href="#">About</a>
      <a href="#">Contact</a>
    </nav>
    <button id="theme-toggle">Toggle Theme</button>
  </header>

  <main class="site-content">
    <section class="hero">
      <h1>웹사이트에 오신 것을 환영합니다</h1>
      <p>이 사이트는 전체 테마 적용 실습을 위한 페이지입니다.</p>
    </section>

    <section class="card-section">
      <div class="card">
        <h3>카드 1</h3>
        <p>카드 콘텐츠...</p>
      </div>
      <div class="card">
        <h3>카드 2</h3>
        <p>카드 콘텐츠...</p>
      </div>
    </section>

    <section class="form-section">
      <form>
        <input type="text" placeholder="이름을 입력하세요">
        <button type="submit" class="button-primary">제출</button>
      </form>
    </section>
  </main>

  <script src="script.js"></script>
</body>
</html>
```

## 6.3. CSS 스타일링 (style.css)

### 1. 시맨틱 변수 및 테마 정의

역할에 따라 변수를 정의하고, 각 테마에 맞게 값을 설정합니다.

```css
/* 테마 변수 정의 */
[data-theme='light'] {
  --bg-page: #f8f9fa;
  --bg-content: #ffffff;
  --text-primary: #212529;
  --text-secondary: #6c757d;
  --color-accent: #007bff;
  --color-accent-contrast: #ffffff;
  --border-color: #dee2e6;
}

[data-theme='dark'] {
  --bg-page: #121212;
  --bg-content: #1e1e1e;
  --text-primary: #e0e0e0;
  --text-secondary: #adb5bd;
  --color-accent: #bb86fc;
  --color-accent-contrast: #000000;
  --border-color: #343a40;
}

/* 기본 스타일 및 전환 효과 */
body {
  background-color: var(--bg-page);
  color: var(--text-primary);
  font-family: sans-serif;
  transition: background-color 0.3s, color 0.3s;
}
```

### 2. 컴포넌트별 스타일 적용

정의된 변수를 사용하여 각 컴포넌트의 스타일을 지정합니다.

```css
/* 헤더 */
.site-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1rem 2rem;
  background-color: var(--bg-content);
  border-bottom: 1px solid var(--border-color);
  transition: background-color 0.3s, border-color 0.3s;
}

.logo { font-weight: bold; }
nav a { color: var(--text-secondary); text-decoration: none; margin-left: 1rem; transition: color 0.3s; }
nav a:hover { color: var(--text-primary); }

/* 메인 콘텐츠 */
.site-content { padding: 2rem; }
.hero h1 { color: var(--text-primary); }
.hero p { color: var(--text-secondary); }

/* 카드 */
.card-section { display: flex; gap: 1rem; margin: 2rem 0; }
.card {
  flex: 1;
  background-color: var(--bg-content);
  border: 1px solid var(--border-color);
  padding: 1.5rem;
  border-radius: 8px;
  transition: background-color 0.3s, border-color 0.3s;
}

/* 폼 */
input[type="text"] {
  padding: 0.5rem;
  border: 1px solid var(--border-color);
  background-color: var(--bg-page);
  color: var(--text-primary);
  border-radius: 4px;
  transition: background-color 0.3s, border-color 0.3s, color 0.3s;
}

.button-primary {
  padding: 0.5rem 1rem;
  border: none;
  border-radius: 4px;
  background-color: var(--color-accent);
  color: var(--color-accent-contrast);
  cursor: pointer;
  transition: background-color 0.3s;
}
```

## 6.4. JavaScript 로직 (script.js)

이전 실습에서 사용한 JavaScript 로직과 동일합니다. 버튼의 ID만 맞게 수정해주면 됩니다.

```javascript
document.addEventListener('DOMContentLoaded', () => {
  const themeToggleButton = document.getElementById('theme-toggle');
  const htmlElement = document.documentElement;

  const savedTheme = localStorage.getItem('theme') || 'light';
  htmlElement.setAttribute('data-theme', savedTheme);

  themeToggleButton.addEventListener('click', () => {
    const currentTheme = htmlElement.getAttribute('data-theme');
    const newTheme = currentTheme === 'dark' ? 'light' : 'dark';
    htmlElement.setAttribute('data-theme', newTheme);
    localStorage.setItem('theme', newTheme);
  });
});
```

## 6.5. 결과 및 고찰

이제 웹사이트의 모든 요소가 테마 전환에 일관되게 반응합니다. 이 실습을 통해 얻을 수 있는 핵심은 다음과 같습니다.

- **추상화의 힘**: 색상 값을 역할 기반의 변수로 추상화함으로써, HTML과 CSS의 나머지 부분을 건드리지 않고도 테마를 쉽게 추가하거나 수정할 수 있습니다.
- **일관성**: 모든 컴포넌트가 동일한 변수 시스템을 공유하므로, 사이트 전체에 걸쳐 디자인의 일관성을 유지하기가 매우 용이합니다.
- **유지보수성**: 나중에 디자인 변경이 필요할 때, CSS 변수가 선언된 부분만 수정하면 되므로 유지보수가 매우 간편해집니다.
