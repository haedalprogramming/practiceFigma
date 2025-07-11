<img src="./header.png" />

# 6. 실습 2: 다크/라이트 테마 토글 만들기 (자바스크립트 X)

> [!NOTE]
> 이 실습에서는 JavaScript를 전혀 사용하지 않고, 순수 HTML과 CSS만으로 다크/라이트 테마를 전환하는 토글 기능을 구현해 봅니다. HTML의 **`<input type="checkbox">`** 요소와 CSS의 **`:checked`** 가상 클래스, 그리고 **일반 형제 결합자(`~`)**를 활용하는 창의적인 CSS 기법을 학습합니다.

## 6.1. 실습 목표

- 체크박스를 클릭하여 페이지의 테마(배경색, 글자색 등)를 라이트 모드와 다크 모드 간에 전환합니다.
- CSS 변수를 사용하여 테마 색상을 효율적으로 관리합니다.
- 부드러운 전환 효과를 위해 `transition` 속성을 적용합니다.

## 6.2. 핵심 원리

1.  **`<input type="checkbox">`**: 사용자가 클릭하여 'on'/'off' 상태를 만들 수 있는 보이지 않는 스위치 역할을 합니다.
2.  **`<label>`**: 체크박스와 연결되어 사용자가 시각적으로 클릭할 수 있는 UI를 제공합니다. `for` 속성을 사용하여 `input`의 `id`와 연결합니다.
3.  **`:checked` 가상 클래스**: 체크박스가 'on'(체크된) 상태일 때를 선택합니다.
4.  **일반 형제 결합자 (`~`)**: 같은 부모를 공유하는 형제 요소들 중에서, 특정 요소(`input:checked`) 뒤에 오는 모든 형제 요소(`~ .theme-container`)를 선택합니다.

## 6.3. HTML 구조

체크박스, 레이블, 그리고 테마가 적용될 전체 컨테이너를 포함하는 HTML 구조를 작성합니다.

```html
<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>CSS-only Theme Toggle</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>

  <!-- 테마 토글 스위치 -->
  <input type="checkbox" id="theme-toggle" class="toggle-checkbox">
  <label for="theme-toggle" class="toggle-label"></label>

  <!-- 테마가 적용될 콘텐츠 영역 -->
  <div class="theme-container">
    <header>
      <h1>CSS-only 다크 모드 토글</h1>
      <p>오직 HTML과 CSS만으로 구현되었습니다.</p>
    </header>
    <main>
      <article>
        <h2>콘텐츠 제목</h2>
        <p>이 영역의 배경색과 글자색은 토글 스위치에 따라 변경됩니다. 체크박스의 상태가 CSS 변수 값을 바꾸는 원리입니다.</p>
        <a href="#">이 링크 색상도 바뀌는지 확인해보세요.</a>
      </article>
    </main>
  </div>

</body>
</html>
```

## 6.4. CSS 스타일링 (style.css)

### 1. 기본 변수 및 스타일

먼저 라이트 모드를 기본으로 하는 CSS 변수와 전체적인 스타일을 정의합니다.

```css
body {
  font-family: sans-serif;
}

/* 테마 색상 변수 선언 */
:root {
  --bg-color: #f0f2f5;
  --text-color: #333;
  --header-color: #111;
  --link-color: #007bff;
  --border-color: #ddd;
  --toggle-bg: #bebebe;
  --toggle-fg: #ffffff;
}

/* 보이지 않는 실제 체크박스 */
.toggle-checkbox {
  display: none;
}

/* 시각적인 토글 스위치 스타일 */
.toggle-label {
  display: block;
  width: 60px;
  height: 30px;
  background-color: var(--toggle-bg);
  border-radius: 15px;
  position: fixed; /* 화면 상단에 고정 */
  top: 20px;
  right: 20px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

/* 토글 스위치의 원형 핸들 */
.toggle-label::after {
  content: '';
  display: block;
  width: 24px;
  height: 24px;
  background-color: var(--toggle-fg);
  border-radius: 50%;
  position: absolute;
  top: 3px;
  left: 3px;
  transition: transform 0.3s ease;
}

/* 테마가 적용될 컨테이너 */
.theme-container {
  background-color: var(--bg-color);
  color: var(--text-color);
  min-height: 100vh;
  padding: 20px;
  transition: background-color 0.3s, color 0.3s;
}

.theme-container h1 {
  color: var(--header-color);
}

.theme-container a {
  color: var(--link-color);
}
```

### 2. `:checked`를 이용한 테마 변경

이제 핵심 부분입니다. 체크박스가 `:checked` 상태일 때, 일반 형제 결합자(`~`)를 사용하여 `.theme-container` 내부에서 사용될 CSS 변수 값을 다크 모드용으로 재정의합니다. 토글 스위치의 시각적 변화도 함께 정의합니다.

```css
/* 체크박스가 체크되었을 때 */
.toggle-checkbox:checked + .toggle-label {
  background-color: #4b7eff; /* 활성화된 토글 배경색 */
}

.toggle-checkbox:checked + .toggle-label::after {
  transform: translateX(30px); /* 핸들을 오른쪽으로 이동 */
}

/* 체크박스가 체크되었을 때, 그 뒤에 오는 .theme-container의 변수 재정의 */
.toggle-checkbox:checked ~ .theme-container {
  --bg-color: #1e1e1e;
  --text-color: #ccc;
  --header-color: #fff;
  --link-color: #82a5ff;
  --border-color: #444;
}
```

## 6.5. 결과 확인

브라우저에서 오른쪽 상단의 토글 스위치를 클릭해보세요. JavaScript 없이도 페이지의 전체적인 테마가 부드럽게 전환되는 것을 확인할 수 있습니다. 이 기술은 간단한 상호작용을 구현할 때 매우 유용합니다.
