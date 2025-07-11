<img src="./header.png" />

# 3. 다크/라이트 테마 커스터마이징 (CSS 변수 기반)

> [!NOTE]
> 이 페이지에서는 CSS 변수(Custom Properties)를 기반으로 다크 모드와 라이트 모드를 체계적으로 디자인하고 커스터마이징하는 구체적인 전략을 학습합니다. 단순히 색상을 반전시키는 것을 넘어, 각 테마에 맞는 최적의 가독성과 시각적 계층을 만드는 방법을 알아봅니다.

## 3.1. 왜 그냥 색상 반전만으로는 부족한가?

단순히 배경을 어둡게, 글자를 밝게 바꾸는 것만으로는 좋은 다크 모드를 만들 수 없습니다. 그 이유는 다음과 같습니다.

- **눈의 피로**: 순수한 검은색 배경(` #000000`)에 순수한 흰색 텍스트(` #ffffff`)는 대비가 너무 강해 장시간 사용 시 눈에 피로를 줄 수 있습니다.
- **시각적 계층 붕괴**: 라이트 모드에서 그림자(shadow)로 표현했던 깊이감이 다크 모드에서는 어색하거나 보이지 않게 됩니다.
- **채도 문제**: 라이트 모드에서 사용된 채도 높은 색상이 다크 모드 배경에서는 너무 튀어 보일 수 있습니다.

## 3.2. 체계적인 테마 커스터마이징 전략

효과적인 테마 시스템을 구축하기 위해 색상을 역할에 따라 변수로 정의하는 것이 중요합니다.

### 1. 시맨틱(Semantic) 색상 변수 정의

`--blue`, `--gray-100`과 같은 직접적인 색상 이름 대신, **역할에 기반한 이름**을 사용합니다. 이는 테마가 바뀌어도 역할은 그대로 유지되기 때문입니다.

```css
/* 테마에 따라 값이 변경될 시맨틱 변수들 */
:root {
  /* 기본 (라이트) 테마 */
  --color-background: #ffffff; /* 페이지 전체 배경 */
  --color-surface: #f8f9fa;    /* 카드, 모달 등 표면 배경 */
  --color-primary: #007bff;      /* 주요 상호작용 색상 (버튼, 링크) */
  --color-secondary: #6c757d;    /* 부가적인 색상 */
  --color-text-primary: #212529; /* 가장 중요한 텍스트 */
  --color-text-secondary: #495057;/* 부가적인 텍스트 */
  --color-border: #dee2e6;       /* 경계선 색상 */
  --shadow-elevation-low: 0 1px 2px 0 rgba(0, 0, 0, 0.05);
}

/* 다크 테마 재정의 */
[data-theme='dark'] {
  --color-background: #121212; /* 순수한 검정 대신 약간 밝은 회색 */
  --color-surface: #1e1e1e;    /* 배경보다 한 단계 밝은 표면 */
  --color-primary: #bb86fc;      /* 채도를 약간 낮춘 보라색 계열 */
  --color-secondary: #8a8a8a;
  --color-text-primary: #e0e0e0; /* 순수한 흰색 대신 연한 회색 */
  --color-text-secondary: #a0a0a0;
  --color-border: #3a3a3a;
  /* 다크모드에서는 그림자 대신 밝은 테두리로 깊이감을 표현하기도 함 */
  --shadow-elevation-low: 0 0 0 1px rgba(255, 255, 255, 0.1);
}
```

### 2. 컴포넌트에 시맨틱 변수 적용

이제 각 컴포넌트는 역할 기반의 변수를 사용하여 스타일을 지정합니다. 이렇게 하면 테마가 변경될 때 컴포넌트의 코드를 수정할 필요가 없습니다.

```html
<div class="card">
  <h3 class="card-title">카드 제목</h3>
  <p class="card-body">이것은 카드 본문 내용입니다.</p>
  <button class="button">더보기</button>
</div>
```

```css
.card {
  background-color: var(--color-surface);
  border: 1px solid var(--color-border);
  box-shadow: var(--shadow-elevation-low);
  padding: 1.5rem;
  border-radius: 8px;
}

.card-title {
  color: var(--color-text-primary);
  margin: 0 0 0.5rem;
}

.card-body {
  color: var(--color-text-secondary);
  margin: 0 0 1rem;
}

.button {
  background-color: var(--color-primary);
  color: var(--color-background); /* 버튼 텍스트는 배경색과 대비되도록 */
  border: none;
  padding: 0.75rem 1.5rem;
  border-radius: 4px;
  cursor: pointer;
}
```

## 3.3. 다크 모드 디자인 팁

- **배경색**: `#000000` 대신 다크 그레이 계열(예: `#121212`, `#1e1e1e`)을 사용하여 눈의 피로를 줄입니다.
- **텍스트 색상**: `#ffffff` 대신 약간의 투명도를 주거나(예: `rgba(255, 255, 255, 0.87)`) 연한 회색을 사용합니다. 중요한 텍스트와 부가적인 텍스트의 명도 차이를 두어 계층을 만듭니다.
- **강조 색상(Primary Color)**: 라이트 모드에서 사용하던 고채도의 색상은 다크 모드에서 너무 튀어 보일 수 있습니다. 채도를 약간 낮추거나 명도를 높인 색상(Pastel 계열)을 사용하는 것이 좋습니다.
- **그림자(Shadow)**: 어두운 배경에서는 그림자가 잘 보이지 않습니다. 대신, 표면(surface)의 배경색을 기본 배경색보다 약간 밝게 하거나, 옅은 테두리(`border`)를 사용하여 깊이감을 표현할 수 있습니다.

이러한 전략을 통해 단순히 색상만 바꾼 것이 아니라, 각 테마의 환경에 맞게 세심하게 조정된 고품질의 사용자 경험을 제공할 수 있습니다.
