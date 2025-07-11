<img src="./header.png" />

# 1. CSS 전역 변수 (Custom Properties)

> [!NOTE]
> 이 페이지에서는 CSS의 강력한 기능인 **전역 변수(Custom Properties)**의 개념을 깊이 이해하고, 실제 프로젝트에서 어떻게 활용하여 유지보수성과 재사용성을 높일 수 있는지 학습합니다.

## 1.1. CSS 변수란?

CSS 변수는 CSS 속성 값을 저장하고 재사용할 수 있도록 만든 사용자 정의 속성입니다. `--`로 시작하는 이름을 가지며, `var()` 함수를 통해 값을 참조합니다. 이를 통해 반복되는 값을 한 곳에서 관리하여 코드의 일관성을 유지하고 수정을 용이하게 만듭니다.

### 기본 문법

변수는 보통 `:root` 의사 클래스(pseudo-class) 내에 선언하여 문서 전체에서 사용할 수 있는 **전역 변수**로 만듭니다.

```css
/* :root는 HTML 문서의 최상위 요소(<html>)를 가리킵니다. */
:root {
  --main-bg-color: #f0f2f5;
  --main-text-color: #333333;
  --primary-color: #4b7eff;
  --secondary-color: #6c757d;
  --default-font-size: 16px;
  --base-spacing-unit: 8px;
}
```

선언된 변수는 `var()` 함수를 사용하여 값으로 불러올 수 있습니다.

```css
body {
  background-color: var(--main-bg-color);
  color: var(--main-text-color);
  font-size: var(--default-font-size);
}

.button-primary {
  background-color: var(--primary-color);
  color: white;
  padding: calc(var(--base-spacing-unit) * 1.5) calc(var(--base-spacing-unit) * 3); /* 12px 24px */
}

.container {
  margin-bottom: calc(var(--base-spacing-unit) * 2); /* 16px */
}
```

## 1.2. 전역 변수 vs 지역 변수

변수는 특정 요소 안에서만 사용 가능한 **지역 변수**로도 선언할 수 있습니다. 해당 요소와 그 자식 요소들에서만 유효합니다.

### 예시 코드

```html
<div class="light-theme">
  <p>이 텍스트는 라이트 테마의 기본 텍스트 색상을 사용합니다.</p>
  <button>기본 버튼</button>
</div>

<div class="dark-theme">
  <p>이 텍스트는 다크 테마의 텍스트 색상을 사용합니다.</p>
  <button>테마 버튼</button>
</div>
```

```css
/* 전역 변수 선언 */
:root {
  --default-text-color: #222;
  --default-bg-color: #fff;
}

/* 기본 스타일 */
p {
  color: var(--text-color, var(--default-text-color)); /* Fallback 값 설정 */
  background-color: var(--bg-color, var(--default-bg-color));
  padding: 10px;
}

/* .dark-theme 클래스에 지역 변수 선언 */
.dark-theme {
  --text-color: #eee; /* 지역 변수 재정의 */
  --bg-color: #222;
}
```

- `.light-theme` 내의 `p` 태그는 `:root`에 선언된 전역 변수 값을 사용합니다.
- `.dark-theme` 내의 `p` 태그는 자신에게 더 가까운 `.dark-theme`에 선언된 지역 변수 값을 우선적으로 사용합니다.

## 1.3. `var()` 함수의 Fallback 값

`var()` 함수는 두 번째 인자로 **Fallback 값**을 지정할 수 있습니다. 이는 첫 번째 인자로 전달된 변수가 정의되지 않았을 경우 사용될 대체 값입니다.

```css
.element {
  /* --undefined-color가 정의되지 않았으므로, Fallback 값인 black이 사용됩니다. */
  color: var(--undefined-color, black);

  /* 다른 변수를 Fallback 값으로 사용할 수도 있습니다. */
  background-color: var(--primary-bg, var(--main-bg-color));
}
```

## 1.4. CSS 변수의 장점

1.  **코드 가독성 및 유지보수성 향상**:
    `#4b7eff`와 같은 의미 없는 값 대신 `--primary-color`와 같이 의미 있는 이름을 사용할 수 있어 코드를 이해하기 쉽습니다. 색상이나 폰트 크기 변경이 필요할 때, 변수 선언부 한 곳만 수정하면 사이트 전체에 일관되게 반영됩니다.

2.  **코드 중복 감소**:
    반복적으로 사용되는 값을 변수로 대체하여 CSS 파일의 전체적인 크기를 줄일 수 있습니다.

3.  **동적 테마 구현**:
    JavaScript를 사용하여 `:root` 또는 특정 요소의 변수 값을 동적으로 변경함으로써, 다크/라이트 모드나 사용자 맞춤 테마 기능을 쉽게 구현할 수 있습니다.

    ```javascript
    // 다크 모드 활성화
    function enableDarkMode() {
      document.documentElement.style.setProperty('--main-bg-color', '#1a1a1a');
      document.documentElement.style.setProperty('--main-text-color', '#ffffff');
    }

    // 라이트 모드 활성화
    function enableLightMode() {
      document.documentElement.style.setProperty('--main-bg-color', '#f0f2f5');
      document.documentElement.style.setProperty('--main-text-color', '#333333');
    }
    ```

4.  **계산의 용이성**:
    `calc()` 함수와 함께 사용하면 간격, 폰트 크기 등을 동적으로 계산하여 유연한 레이아웃을 만들 수 있습니다.

    ```css
    :root {
      --base-font-size: 1rem;
    }

    h1 {
      font-size: calc(var(--base-font-size) * 2.5); /* 2.5rem */
    }
    h2 {
      font-size: calc(var(--base-font-size) * 2);   /* 2.0rem */
    }
    ```
