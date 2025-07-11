<img src="./header.png" />

# 4. @media를 활용한 테마 설정 (prefers-color-scheme)

> [!NOTE]
> 이 페이지에서는 사용자의 시스템 설정(라이트 모드 또는 다크 모드)에 자동으로 반응하는 웹사이트를 만들기 위해 **`prefers-color-scheme`** 미디어 기능을 사용하는 방법을 학습합니다. 이를 통해 별도의 토글 버튼 없이도 사용자에게 최적화된 테마를 제공할 수 있습니다.

## 4.1. `prefers-color-scheme` 이란?

`prefers-color-scheme`은 사용자가 자신의 운영체제(OS)나 브라우저에서 선호하는 색상 테마가 무엇인지 감지하는 미디어 기능입니다. 이 기능을 사용하면 CSS를 통해 사용자의 선택에 맞는 스타일을 제공할 수 있습니다.

### 사용 가능한 값

- **`light`**: 사용자가 시스템에서 라이트 테마를 선택했음을 나타냅니다.
- **`dark`**: 사용자가 시스템에서 다크 테마를 선택했음을 나타냅니다.
- **`no-preference`**: 사용자가 시스템에 특정 테마를 설정하지 않았음을 나타냅니다.

### 기본 문법

```css
/* 기본 스타일 (라이트 모드 또는 미설정 시) */
body {
  background-color: #ffffff;
  color: #222222;
}

/* 사용자가 다크 모드를 선호할 경우 적용될 스타일 */
@media (prefers-color-scheme: dark) {
  body {
    background-color: #222222;
    color: #ffffff;
  }
}
```

## 4.2. CSS 변수와 함께 사용하기

`prefers-color-scheme`은 CSS 변수(Custom Properties)와 함께 사용할 때 가장 강력한 시너지를 발휘합니다. 테마에 따라 변경될 색상들을 변수로 정의하고, 미디어 쿼리 내에서 이 변수들의 값만 재정의하면 훨씬 효율적으로 테마를 관리할 수 있습니다.

### 예시 코드

```html
<body>
  <header>
    <h1>웹사이트 제목</h1>
    <p>사용자 설정에 따라 테마가 변경됩니다.</p>
  </header>
  <main>
    <article>
      <h2>첫 번째 글</h2>
      <p>이것은 본문 내용입니다. <a href="#">링크 스타일</a>도 확인해보세요.</p>
    </article>
  </main>
</body>
```

```css
/* 1. :root에 기본 (라이트 모드) 색상 변수 선언 */
:root {
  --bg-color: #ffffff;
  --text-color: #333333;
  --heading-color: #111111;
  --link-color: #4b7eff;
  --border-color: #dddddd;
}

/* 2. 다크 모드일 때 변수 값 재정의 */
@media (prefers-color-scheme: dark) {
  :root {
    --bg-color: #1e1e1e;
    --text-color: #cccccc;
    --heading-color: #ffffff;
    --link-color: #82a5ff;
    --border-color: #444444;
  }
}

/* 3. 변수를 사용하여 스타일 적용 */
body {
  background-color: var(--bg-color);
  color: var(--text-color);
  font-family: sans-serif;
  line-height: 1.6;
}

h1, h2 {
  color: var(--heading-color);
}

a {
  color: var(--link-color);
}

article {
  border: 1px solid var(--border-color);
  padding: 20px;
  margin-top: 20px;
}
```

**작동 방식:**

1.  브라우저는 먼저 `:root`에 선언된 라이트 모드용 변수를 기본값으로 인식합니다.
2.  만약 사용자의 시스템 설정이 다크 모드이면, `@media (prefers-color-scheme: dark)` 블록 안의 CSS가 활성화됩니다.
3.  활성화된 미디어 쿼리 내에서 `:root`의 색상 변수들이 다크 모드용 값으로 **재정의(override)**됩니다.
4.  `body`, `h1`, `a` 등의 요소들은 `var()`를 통해 현재 활성화된 변수 값을 참조하므로, 시스템 설정에 따라 자동으로 테마가 변경됩니다.

## 4.3. 이미지 테마 대응

`<picture>` 태그와 함께 사용하면, 다크 모드일 때 더 어두운 이미지를 보여주는 등 이미지 리소스도 테마에 맞게 변경할 수 있습니다.

```html
<picture>
  <source srcset="logo-dark.png" media="(prefers-color-scheme: dark)">
  <img src="logo-light.png" alt="로고">
</picture>
```

위 코드는 사용자가 다크 모드를 선호하면 `logo-dark.png`를, 그렇지 않으면 기본적으로 `logo-light.png`를 표시합니다.
