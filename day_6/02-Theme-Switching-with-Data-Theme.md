<img src="./header.png" />

# 2. `data-theme`을 활용한 테마 전환

> [!NOTE]
> 이 페이지에서는 `data-theme`이라는 사용자 정의 데이터 속성을 활용하여 웹사이트의 테마(예: 라이트/다크 모드, 블루/레드 테마 등)를 동적으로 전환하는 세련되고 효율적인 방법을 학습합니다. CSS 변수와 JavaScript를 함께 사용하여 어떻게 강력한 테마 시스템을 구축하는지 알아봅니다.

## 2.1. `data-theme` 방식의 핵심 원리

이 방식은 HTML 최상위 요소(보통 `<html>` 또는 `<body>`)에 `data-theme` 속성을 두고, 이 속성 값에 따라 다른 스타일을 적용하는 것입니다. JavaScript로 이 속성 값만 변경해주면, CSS가 알아서 해당 테마에 맞는 스타일을 렌더링합니다.

**왜 이 방식이 좋은가?**

- **중앙 집중 관리**: 테마와 관련된 모든 스타일이 CSS에 집중되어 있어 관리가 편합니다.
- **유연성**: 라이트/다크 모드뿐만 아니라, `data-theme="blue"`, `data-theme="high-contrast"` 등 다양한 테마를 쉽게 추가할 수 있습니다.
- **관심사 분리**: JavaScript는 "어떤 테마를 적용할지"만 결정하고, "어떻게 보일지"는 전적으로 CSS가 담당하여 코드 구조가 깔끔해집니다.

## 2.2. CSS 구현: 테마별 스타일 정의

먼저 CSS에서 `data-theme` 속성 값에 따라 다른 색상 변수를 정의합니다. 속성 선택자(`[]`)를 사용합니다.

```css
/* 기본 테마 (라이트 모드) */
[data-theme='light'] {
  --bg-color: #ffffff;
  --text-color: #222222;
  --primary-color: #007bff;
  --card-bg-color: #f8f9fa;
  --border-color: #dee2e6;
}

/* 다크 모드 테마 */
[data-theme='dark'] {
  --bg-color: #121212;
  --text-color: #e0e0e0;
  --primary-color: #bb86fc;
  --card-bg-color: #1e1e1e;
  --border-color: #333333;
}

/* 블루 테마 (추가 예시) */
[data-theme='blue'] {
  --bg-color: #e7f1ff;
  --text-color: #0b3d7a;
  --primary-color: #0056b3;
  --card-bg-color: #ffffff;
  --border-color: #b3d4ff;
}

/* --- 이제 이 변수들을 사용하여 실제 스타일을 적용 --- */

body {
  background-color: var(--bg-color);
  color: var(--text-color);
  font-family: sans-serif;
  transition: background-color 0.3s, color 0.3s; /* 부드러운 전환 효과 */
}

.card {
  background-color: var(--card-bg-color);
  border: 1px solid var(--border-color);
  padding: 20px;
  margin: 20px 0;
}

.button-primary {
  background-color: var(--primary-color);
  color: var(--bg-color); /* 배경색과 대비되는 색상 사용 */
  padding: 10px 15px;
  border: none;
  cursor: pointer;
}
```

## 2.3. HTML 구조: 기본 설정

HTML의 `<html>` 태그에 기본 테마를 설정해줍니다. 사용자가 테마를 변경하기 전까지 이 테마가 적용됩니다.

```html
<!DOCTYPE html>
<!-- 기본 테마를 'light'로 설정 -->
<html lang="ko" data-theme="light">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>data-theme 테마 전환</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>

  <h1>테마 전환 예제</h1>
  <div class="card">
    <p>이 카드의 스타일은 현재 테마에 따라 변경됩니다.</p>
  </div>
  <button class="button-primary">주요 버튼</button>

  <div class="theme-switcher">
    <button data-set-theme="light">Light</button>
    <button data-set-theme="dark">Dark</button>
    <button data-set-theme="blue">Blue</button>
  </div>

  <script src="script.js"></script>
</body>
</html>
```

## 2.4. JavaScript 구현: 테마 변경 로직

JavaScript는 버튼 클릭을 감지하여 `<html>` 요소의 `data-theme` 속성 값을 변경하는 역할만 수행합니다.

```javascript
// script.js

document.addEventListener('DOMContentLoaded', () => {
  const themeSwitcher = document.querySelector('.theme-switcher');

  themeSwitcher.addEventListener('click', (event) => {
    // 클릭된 요소가 테마 설정 버튼인지 확인
    const theme = event.target.dataset.setTheme;
    if (theme) {
      setTheme(theme);
    }
  });

  function setTheme(theme) {
    // html 요소의 data-theme 속성 값을 변경
    document.documentElement.setAttribute('data-theme', theme);
    
    // 사용자의 테마 선택을 localStorage에 저장 (선택 사항)
    localStorage.setItem('theme', theme);
  }

  // 페이지 로드 시 localStorage에 저장된 테마가 있으면 적용 (선택 사항)
  const savedTheme = localStorage.getItem('theme');
  if (savedTheme) {
    setTheme(savedTheme);
  }
});
```

### localStorage를 이용한 테마 유지 (선택 사항)

위 JavaScript 코드에는 사용자가 선택한 테마를 브라우저의 `localStorage`에 저장하는 기능이 포함되어 있습니다. 이렇게 하면 사용자가 페이지를 새로고침하거나 나중에 다시 방문했을 때 이전에 선택했던 테마가 그대로 유지되어 더 나은 사용자 경험을 제공할 수 있습니다.
