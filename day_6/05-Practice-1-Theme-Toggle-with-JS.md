<img src="./header.png" />

# 5. 실습 1: 토글 버튼으로 테마 바꾸기 (JS 포함)

> [!NOTE]
> 이 실습에서는 JavaScript를 사용하여 사용자가 버튼을 클릭할 때마다 웹사이트의 테마를 동적으로 변경하는 완전한 기능을 구현합니다. `data-theme` 속성을 제어하고, 사용자의 선택을 `localStorage`에 저장하여 다음 방문 시에도 테마를 유지하는 방법을 학습합니다.

## 5.1. 실습 목표

- 버튼 클릭 시 `<html>` 요소의 `data-theme` 속성 값을 `light`와 `dark` 간에 전환합니다.
- 현재 적용된 테마가 무엇인지 감지하여 다음 테마로 변경하는 로직을 구현합니다.
- 사용자가 선택한 테마를 브라우저의 `localStorage`에 저장하고, 페이지 로드 시 이를 다시 불러와 적용합니다.

## 5.2. HTML 구조

테마를 변경할 버튼과 테마가 적용될 콘텐츠를 포함하는 기본 HTML 구조를 작성합니다.

```html
<!DOCTYPE html>
<html lang="ko" data-theme="light"> <!-- 기본 테마 설정 -->
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>JS 테마 토글 실습</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>

  <header>
    <h1>JavaScript 테마 토글</h1>
    <button id="theme-toggle-button">테마 변경</button>
  </header>

  <main>
    <p>이 페이지의 테마는 버튼 클릭으로 변경됩니다.</p>
  </main>

  <script src="script.js"></script>
</body>
</html>
```

## 5.3. CSS 스타일

`data-theme` 속성 값에 따라 변경될 스타일과 부드러운 전환 효과를 정의합니다.

```css
/* style.css */
[data-theme='light'] {
  --bg-color: #f0f2f5;
  --text-color: #222;
}

[data-theme='dark'] {
  --bg-color: #121212;
  --text-color: #e0e0e0;
}

body {
  background-color: var(--bg-color);
  color: var(--text-color);
  transition: background-color 0.3s, color 0.3s;
}

header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1rem 2rem;
}

button {
  padding: 0.5rem 1rem;
  cursor: pointer;
}
```

## 5.4. JavaScript 로직 (script.js)

이제 테마 변경의 핵심 로직을 JavaScript로 작성합니다.

```javascript
// DOM이 완전히 로드된 후 스크립트 실행
document.addEventListener('DOMContentLoaded', () => {

  // 1. 필요한 요소 가져오기
  const themeToggleButton = document.getElementById('theme-toggle-button');
  const htmlElement = document.documentElement; // <html> 요소

  // 2. localStorage에서 저장된 테마 불러오기
  // 저장된 값이 없으면 'light'를 기본값으로 사용
  const savedTheme = localStorage.getItem('theme') || 'light';
  htmlElement.setAttribute('data-theme', savedTheme);

  // 3. 버튼 클릭 이벤트 리스너 추가
  themeToggleButton.addEventListener('click', () => {
    // 현재 테마 가져오기
    const currentTheme = htmlElement.getAttribute('data-theme');

    // 테마 전환: 현재 테마가 'dark'이면 'light'로, 아니면 'dark'로 변경
    const newTheme = currentTheme === 'dark' ? 'light' : 'dark';

    // <html> 요소의 data-theme 속성 변경
    htmlElement.setAttribute('data-theme', newTheme);

    // 변경된 테마를 localStorage에 저장
    localStorage.setItem('theme', newTheme);
  });

});
```

### 코드 해설

1.  **`DOMContentLoaded`**: HTML 문서가 완전히 파싱되고 DOM 트리가 완성된 후에 JavaScript 코드가 실행되도록 하여, `getElementById`가 요소를 찾지 못하는 오류를 방지합니다.

2.  **요소 선택**: `getElementById`로 버튼을, `document.documentElement`로 `<html>` 요소를 선택하여 변수에 저장합니다.

3.  **테마 불러오기**: `localStorage.getItem('theme')`을 사용하여 브라우저에 저장된 테마 값을 가져옵니다. 만약 저장된 값이 없으면(`null`), 논리 OR 연산자(`||`)를 통해 `'light'`를 기본값으로 사용합니다. 가져온 테마를 페이지 로드 시 바로 적용합니다.

4.  **클릭 이벤트**: 버튼에 `addEventListener`를 추가하여 클릭 이벤트를 감지합니다.

5.  **테마 전환 로직**: 클릭이 발생하면, 먼저 현재 `data-theme` 속성 값을 읽어옵니다. 그 후, 삼항 연산자(`? :`)를 사용하여 현재 값이 `'dark'`이면 `'light'`로, 그 외의 경우(즉, `'light'`)는 `'dark'`로 `newTheme` 변수를 설정합니다.

6.  **테마 적용 및 저장**: `setAttribute`를 사용하여 `<html>` 요소의 `data-theme` 속성을 `newTheme`으로 변경합니다. 이 순간 CSS에 정의된 스타일에 따라 화면의 테마가 변경됩니다. 마지막으로, `localStorage.setItem('theme', newTheme)`을 통해 사용자의 새로운 테마 선택을 브라우저에 저장하여 다음 방문 시에도 유지되도록 합니다.

## 5.5. 결과 확인

브라우저에서 '테마 변경' 버튼을 클릭하여 테마가 잘 전환되는지 확인합니다. 페이지를 새로고침해도 마지막에 선택한 테마가 유지되는지 확인해보세요. 개발자 도구(F12)의 'Application' 탭 > 'Local Storage'에서 값이 어떻게 저장되고 변경되는지 관찰하면 이해에 더 도움이 됩니다.
