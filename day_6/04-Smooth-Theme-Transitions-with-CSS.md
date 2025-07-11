<img src="./header.png" />

# 4. CSS 전환 애니메이션으로 부드러운 테마 전환

> [!NOTE]
> 이 페이지에서는 CSS의 **`transition`** 속성을 사용하여 테마가 변경될 때 시각적 요소들이 딱딱하게 변하는 것이 아니라, 부드럽고 자연스럽게 전환되는 애니메이션을 구현하는 방법을 학습합니다. 좋은 전환 효과는 사용자 경험을 한층 더 고급스럽게 만들어 줍니다.

## 4.1. `transition` 속성이란?

`transition` 속성은 CSS 속성 값이 변경될 때, 그 변화가 일정 시간(duration)에 걸쳐 점진적으로 일어나도록 만들어주는 단축 속성입니다. 이를 통해 요소의 색상, 크기, 위치 등이 부드럽게 애니메이션 처리됩니다.

### 기본 문법

`transition` 속성은 여러 속성을 한 번에 지정할 수 있습니다.

`transition: [속성명] [지속시간] [타이밍함수] [지연시간];`

- **`transition-property`**: 전환 효과를 적용할 CSS 속성의 이름 (예: `background-color`, `opacity`, `all`).
- **`transition-duration`**: 전환이 일어나는 데 걸리는 시간 (예: `0.3s`, `500ms`).
- **`transition-timing-function`**: 전환의 속도 곡선을 지정 (예: `ease`, `linear`, `ease-in-out`).
- **`transition-delay`**: 전환이 시작되기 전까지의 지연 시간 (예: `0.1s`).

```css
.button {
  background-color: #007bff;
  color: white;
  /* background-color 속성이 0.3초 동안 ease-in-out 곡선으로 변하도록 설정 */
  transition: background-color 0.3s ease-in-out;
}

.button:hover {
  background-color: #0056b3;
}
```

## 4.2. 테마 전환에 `transition` 적용하기

테마 전환 시 색상이 변경되는 모든 요소에 `transition` 속성을 추가하면, `data-theme` 속성이 변경되어 CSS 변수 값이 바뀔 때 애니메이션 효과가 적용됩니다.

### 예시 코드

```html
<html lang="ko" data-theme="light">
<body>
  <div class="card">
    <h1>안녕하세요!</h1>
    <p>테마를 바꿔보세요.</p>
    <button id="theme-toggle">테마 변경</button>
  </div>
</body>
</html>
```

```css
/* 1. 테마별 변수 정의 */
[data-theme='light'] {
  --bg-color: #f0f2f5;
  --card-bg-color: #ffffff;
  --text-color: #222222;
  --heading-color: #000000;
}

[data-theme='dark'] {
  --bg-color: #121212;
  --card-bg-color: #1e1e1e;
  --text-color: #e0e0e0;
  --heading-color: #ffffff;
}

/* 2. 전환 효과를 적용할 요소에 transition 속성 추가 */
body {
  background-color: var(--bg-color);
  color: var(--text-color);
  /* 배경색과 글자색 변경에 0.3초의 전환 효과 적용 */
  transition: background-color 0.3s ease, color 0.3s ease;
}

.card {
  background-color: var(--card-bg-color);
  padding: 2rem;
  border-radius: 8px;
  /* 카드 배경색 변경에 전환 효과 적용 */
  transition: background-color 0.3s ease;
}

h1 {
  color: var(--heading-color);
  /* 제목 색상 변경에 전환 효과 적용 */
  transition: color 0.3s ease;
}
```

### 여러 속성에 한 번에 적용하기

`all` 키워드를 사용하면 해당 요소의 모든 속성 변경에 대해 전환 효과를 적용할 수 있습니다. 하지만 성능상의 이유로, 필요한 속성만 명시적으로 지정하는 것이 더 좋습니다.

```css
/* 좋은 예: 필요한 속성만 지정 */
.element {
  transition: background-color 0.3s, color 0.3s, border-color 0.3s;
}

/* 나쁜 예: 불필요한 속성까지 전환을 시도할 수 있음 */
.element {
  transition: all 0.3s;
}
```

## 4.3. 타이밍 함수(Timing Function) 비교

타이밍 함수는 전환 효과의 느낌을 크게 좌우합니다.

- **`ease`** (기본값): 천천히 시작하여 빨라졌다가 다시 천천히 끝납니다. 가장 자연스러운 느낌을 줍니다.
- **`linear`**: 시작부터 끝까지 동일한 속도로 진행됩니다. 기계적인 느낌을 줍니다.
- **`ease-in`**: 천천히 시작하여 점점 빨라집니다.
- **`ease-out`**: 빠르게 시작하여 점점 느려집니다.
- **`ease-in-out`**: `ease`와 유사하지만, 시작과 끝의 변화가 더 부드럽습니다.

다양한 타이밍 함수를 적용해보며 각 효과가 어떻게 다른지 직접 확인해보는 것이 중요합니다.

```css
.box {
  width: 100px;
  height: 100px;
  background: #007bff;
  transition: transform 1s;
}

.box.ease { transition-timing-function: ease; }
.box.linear { transition-timing-function: linear; }
.box.ease-in-out { transition-timing-function: ease-in-out; }

.container:hover .box {
  transform: translateX(200px);
}
```

이처럼 `transition`을 적절히 활용하면, 기능적인 부분을 넘어 사용자에게 훨씬 더 세련되고 만족스러운 인터랙션을 제공할 수 있습니다.
