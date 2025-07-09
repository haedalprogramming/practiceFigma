<img src="./header.png" />

# 3. @media를 활용한 해상도 대응

> [!NOTE]
> 이 페이지에서는 반응형 웹의 핵심 기술인 **미디어 쿼리(`@media`)**를 사용하여 다양한 화면 해상도에 대응하는 구체적인 방법을 학습합니다. Breakpoint를 설정하고, 이를 기준으로 CSS 스타일을 어떻게 다르게 적용하는지 예제와 함께 살펴봅니다.

## 3.1. 미디어 쿼리(@media)란?

미디어 쿼리는 웹페이지가 표시되는 미디어의 유형(예: `screen`, `print`)이나 특정 조건 또는 특징(예: 뷰포트 너비, 화면 방향)을 감지하여, 해당 조건이 참(true)일 경우에만 특정 CSS 규칙을 적용하는 기능입니다.

### 기본 문법

미디어 쿼리는 `@media` 키워드로 시작하며, 그 뒤에 미디어 유형과 괄호로 묶인 조건을 명시합니다.

```css
@media [미디어 유형] and (조건) {
  /* 조건이 참일 때 적용될 CSS 규칙 */
}
```

- **미디어 유형 (선택 사항)**: `all`, `print`, `screen`, `speech` 등이 있습니다. 보통 웹에서는 `screen`을 대상으로 하므로 생략하는 경우가 많습니다 (기본값은 `all`).
- **조건 (Media Features)**: `max-width`, `min-width`, `orientation` 등 다양한 조건을 사용할 수 있습니다.

## 3.2. Breakpoint와 해상도 대응

**Breakpoint(분기점)**는 웹사이트의 레이아웃이 변경되는 특정 뷰포트 너비 지점을 의미합니다. 디자이너와 개발자는 주요 디바이스 크기를 고려하여 Breakpoint를 설정하고, 각 Breakpoint에 맞춰 최적의 레이아웃을 제공합니다.

### 일반적인 Breakpoint 예시

- **모바일**: 320px ~ 767px
- **태블릿**: 768px ~ 1023px
- **데스크톱**: 1024px 이상

> [!TIP]
> 프로젝트나 디자인 시스템에 따라 Breakpoint 기준은 달라질 수 있습니다. 중요한 것은 특정 디바이스에 맞추기보다, 콘텐츠가 어색해 보이기 시작하는 지점을 기준으로 Breakpoint를 설정하는 것입니다.

### `min-width` vs `max-width`

미디어 쿼리 작성 시, `min-width`와 `max-width`는 가장 흔하게 사용되는 조건입니다.

- **`min-width` (Mobile First 접근 방식)**:
  뷰포트 너비가 **지정된 값 이상일 때** 스타일을 적용합니다. 작은 화면(모바일)을 기본으로 디자인하고, 화면이 커짐에 따라 스타일을 추가해 나가는 방식입니다. 현대 웹 개발에서 권장되는 접근법입니다.

- **`max-width` (Desktop First 접근 방식)**:
  뷰포트 너비가 **지정된 값 이하일 때** 스타일을 적용합니다. 큰 화면(데스크톱)을 기본으로 디자인하고, 화면이 작아짐에 따라 스타일을 변경하는 방식입니다.

### 예시 코드: Mobile First 접근법

```html
<div class="container">
  <div class="box">Box 1</div>
  <div class="box">Box 2</div>
  <div class="box">Box 3</div>
</div>
```

```css
/* 기본 스타일 (모바일) */
.container {
  display: flex;
  flex-direction: column; /* 기본적으로 세로로 쌓임 */
}

.box {
  background-color: #4b7eff;
  color: white;
  padding: 20px;
  margin: 10px;
  text-align: center;
}

/* 태블릿 (768px 이상) */
@media (min-width: 768px) {
  .container {
    flex-direction: row; /* 가로로 배치 */
    flex-wrap: wrap;
  }
  .box {
    width: calc(50% - 20px); /* 2개의 컬럼, margin 값을 고려하여 계산 */
  }
}

/* 데스크톱 (1024px 이상) */
@media (min-width: 1024px) {
  .box {
    width: calc(33.333% - 20px); /* 3개의 컬럼 */
  }
}
```

## 3.3. 복합적인 미디어 쿼리

`and`, `not`, `,`(or) 등의 논리 연산자를 사용하여 여러 조건을 조합할 수 있습니다.

### `and` 연산자

여러 조건을 모두 만족할 때 스타일을 적용합니다.

```css
/* 화면 너비가 768px 이상이고 1023px 이하일 때 (태블릿 가로 모드 등) */
@media (min-width: 768px) and (max-width: 1023px) {
  body {
    background-color: lightblue;
  }
}
```

### `,` (or) 연산자

여러 조건 중 하나라도 만족할 때 스타일을 적용합니다.

```css
/* 화면이 가로 방향이거나, 인쇄용일 때 */
@media (orientation: landscape), print {
  .header {
    display: none; /* 헤더 숨기기 */
  }
}
```

### `not` 연산자

특정 조건을 제외할 때 사용합니다.

```css
/* 흑백이 아닌 컬러 스크린에만 적용 */
@media not screen and (color) {
  /* 스타일 규칙 */
}
```
