<img src="./header.png" />

# 5. 실습 1: 반응형 카드 UI 만들기

> [!NOTE]
> 이 실습에서는 지금까지 배운 **유동형 그리드**와 **미디어 쿼리**를 활용하여 화면 크기에 따라 레이아웃이 유연하게 변경되는 반응형 카드 UI를 직접 만들어 봅니다. 모바일, 태블릿, 데스크톱 환경에 최적화된 UI를 구현하는 과정을 경험합니다.

## 5.1. 실습 목표

- **모바일 (기본)**: 카드가 세로로 한 줄에 하나씩 표시됩니다 (1열).
- **태블릿 (768px 이상)**: 카드가 한 줄에 두 개씩 표시됩니다 (2열).
- **데스크톱 (1024px 이상)**: 카드가 한 줄에 세 개씩 표시됩니다 (3열).

## 5.2. HTML 구조

먼저 카드들을 감싸는 컨테이너와 개별 카드 아이템을 포함하는 기본 HTML 구조를 작성합니다.

```html
<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>반응형 카드 UI 실습</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>

  <div class="card-container">
    <div class="card">
      <img src="https://via.placeholder.com/400x250/4b7eff/ffffff?text=Card+Image" alt="카드 이미지">
      <div class="card-content">
        <h3>카드 제목 1</h3>
        <p>이곳은 카드에 대한 설명이 들어가는 부분입니다. 화면 크기에 따라 레이아웃이 변경됩니다.</p>
        <a href="#" class="button">더 알아보기</a>
      </div>
    </div>

    <div class="card">
      <img src="https://via.placeholder.com/400x250/28a745/ffffff?text=Card+Image" alt="카드 이미지">
      <div class="card-content">
        <h3>카드 제목 2</h3>
        <p>이곳은 카드에 대한 설명이 들어가는 부분입니다. 화면 크기에 따라 레이아웃이 변경됩니다.</p>
        <a href="#" class="button">더 알아보기</a>
      </div>
    </div>

    <div class="card">
      <img src="https://via.placeholder.com/400x250/ffc107/000000?text=Card+Image" alt="카드 이미지">
      <div class="card-content">
        <h3>카드 제목 3</h3>
        <p>이곳은 카드에 대한 설명이 들어가는 부분입니다. 화면 크기에 따라 레이아웃이 변경됩니다.</p>
        <a href="#" class="button">더 알아보기</a>
      </div>
    </div>
  </div>

</body>
</html>
```

## 5.3. CSS 스타일링 (style.css)

**Mobile First** 접근법에 따라 모바일 스타일을 기본으로 작성하고, 미디어 쿼리를 사용하여 더 큰 화면에 대한 스타일을 추가합니다.

### 1. 기본 및 모바일 스타일

```css
/* 기본 스타일 초기화 및 폰트 설정 */
body {
  margin: 0;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  background-color: #f4f4f4;
}

img {
  max-width: 100%;
  height: auto;
  display: block; /* 이미지 하단 여백 제거 */
}

/* 카드 컨테이너 */
.card-container {
  display: flex;
  flex-direction: column; /* 모바일에서는 세로로 쌓음 */
  padding: 20px;
  gap: 20px; /* 카드 사이의 간격 */
}

/* 개별 카드 */
.card {
  background-color: #ffffff;
  border-radius: 8px;
  box-shadow: 0 4px 8px rgba(0,0,0,0.1);
  overflow: hidden; /* 이미지가 모서리를 벗어나지 않도록 */
  transition: transform 0.2s ease-in-out;
}

.card:hover {
  transform: translateY(-5px);
}

.card-content {
  padding: 20px;
}

.card-content h3 {
  margin-top: 0;
  color: #333;
}

.card-content p {
  color: #666;
  line-height: 1.5;
}

.button {
  display: inline-block;
  background-color: #4b7eff;
  color: white;
  padding: 10px 20px;
  text-decoration: none;
  border-radius: 5px;
  margin-top: 15px;
  transition: background-color 0.2s;
}

.button:hover {
  background-color: #3a6ae6;
}
```

### 2. 태블릿 스타일 (768px 이상)

화면 너비가 768px 이상일 때, 카드를 2열로 배치합니다. `flex-direction`을 `row`로 바꾸고 `flex-wrap`을 사용하여 줄바꿈을 허용합니다. 각 카드의 너비는 `gap`을 고려하여 계산합니다.

```css
/* 태블릿 스타일 */
@media (min-width: 768px) {
  .card-container {
    flex-direction: row; /* 가로로 배치 */
    flex-wrap: wrap; /* 줄바꿈 허용 */
    justify-content: space-between;
  }

  .card {
    width: calc(50% - 10px); /* 2열, gap(20px)의 절반을 뺌 */
  }
}
```

### 3. 데스크톱 스타일 (1024px 이상)

화면 너비가 1024px 이상일 때, 카드를 3열로 배치합니다. 카드의 너비를 다시 계산해줍니다.

```css
/* 데스크톱 스타일 */
@media (min-width: 1024px) {
  .card {
    width: calc(33.333% - 14px); /* 3열, (gap*2)/3 만큼 뺌 */
  }
}
```

> [!TIP]
> `calc()` 함수 내의 계산이 복잡해 보일 수 있습니다. `(전체 너비 / 컬럼 수) - (전체 gap / 컬럼 수)` 와 유사한 원리로 계산됩니다. `justify-content: space-between`을 사용하면 양쪽 끝에 카드를 붙여주므로 계산이 더 간단해질 수 있습니다.

## 5.4. 결과 확인

브라우저 창의 크기를 조절하면서 카드의 레이아웃이 1열, 2열, 3열로 부드럽게 변경되는지 확인해보세요. 이를 통해 반응형 웹의 기본 원리를 실제로 경험할 수 있습니다.
