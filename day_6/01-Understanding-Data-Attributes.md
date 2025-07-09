<img src="./header.png" />

# 1. HTML의 `data-*` 속성 이해하기

> [!NOTE]
> 이 페이지에서는 표준 HTML 속성 외에, 개발자가 요소에 추가적인 정보를 저장할 수 있도록 해주는 **사용자 정의 데이터 속성(`data-*`)**에 대해 깊이 알아봅니다. 이 속성을 CSS와 JavaScript에서 어떻게 활용하여 더 동적이고 의미 있는 웹 페이지를 만들 수 있는지 학습합니다.

## 1.1. `data-*` 속성이란?

`data-*` 속성은 HTML 요소에 **사용자 정의 데이터**를 저장하기 위한 목적으로 사용되는 특별한 종류의 속성입니다. 이 속성들은 일반적으로 브라우저의 렌더링에 직접적인 영향을 주지 않지만, CSS나 JavaScript에서 해당 데이터를 참조하여 특정 동작이나 스타일을 적용하는 데 사용됩니다.

### 기본 문법

- 속성 이름은 반드시 `data-`로 시작해야 합니다.
- `data-` 다음에는 최소 하나 이상의 문자가 와야 합니다.
- 속성 이름에는 대문자를 사용해서는 안 되며, 여러 단어로 구성될 경우 하이픈(`-`)으로 연결하는 것이 일반적입니다 (예: `data-user-id`).

```html
<!-- 간단한 데이터 저장 -->
<div data-animal="dog">강아지</div>

<!-- 여러 단어로 구성된 데이터 속성 -->
<div data-user-id="12345" data-user-role="admin">관리자 정보</div>

<!-- JSON 형식의 복잡한 데이터 저장 -->
<div data-options='{"name": "Alice", "age": 30}'>사용자 옵션</div>
```

## 1.2. CSS에서 `data-*` 속성 활용하기

CSS에서는 **속성 선택자(`[]`)**를 사용하여 `data-*` 속성 값에 따라 다른 스타일을 적용할 수 있습니다. 이는 요소의 상태에 따라 시각적 피드백을 주는 데 매우 유용합니다.

### 예시 코드: 툴팁(Tooltip) 표시

`data-tooltip` 속성에 저장된 텍스트를 마우스 호버 시 보여주는 툴팁을 만들어 보겠습니다.

```html
<p>여기에 마우스를 올려보세요: <span data-tooltip="이것은 툴팁 메시지입니다!">도움말</span></p>
```

```css
[data-tooltip] {
  position: relative; /* 툴팁의 기준점이 됨 */
  cursor: help;
  text-decoration: underline dotted;
}

/* ::before 가상 요소를 사용하여 툴팁 생성 */
[data-tooltip]::before {
  content: attr(data-tooltip); /* data-tooltip 속성 값을 content로 가져옴 */
  position: absolute;
  bottom: 100%; /* 텍스트 위쪽에 위치 */
  left: 50%;
  transform: translateX(-50%);
  
  background-color: #333;
  color: #fff;
  padding: 8px 12px;
  border-radius: 5px;
  white-space: nowrap; /* 줄바꿈 방지 */
  
  opacity: 0; /* 기본적으로 숨김 */
  visibility: hidden;
  transition: opacity 0.2s, visibility 0.2s;
}

/* 호버 시 툴팁 표시 */
[data-tooltip]:hover::before {
  opacity: 1;
  visibility: visible;
}
```

## 1.3. JavaScript에서 `data-*` 속성 활용하기

JavaScript에서는 `HTMLElement.dataset` 속성을 통해 `data-*` 속성에 쉽게 접근하고 조작할 수 있습니다. `data-` 뒤에 오는 이름이 `dataset` 객체의 속성 키가 됩니다. 이때 하이픈(`-`)으로 연결된 이름은 카멜 케이스(camelCase)로 변환됩니다.

- `data-user-id` → `dataset.userId`
- `data-animal` → `dataset.animal`

### 예시 코드: 이미지 갤러리

버튼을 클릭하면 `data-image-src`에 저장된 이미지 주소를 가져와 메인 이미지를 변경하는 간단한 갤러리를 만들어 보겠습니다.

```html
<div id="gallery">
  <img id="main-image" src="https://via.placeholder.com/400x250/4b7eff/ffffff" alt="메인 이미지">
  
  <div class="thumbnails">
    <button data-image-src="https://via.placeholder.com/400x250/4b7eff/ffffff">이미지 1</button>
    <button data-image-src="https://via.placeholder.com/400x250/28a745/ffffff">이미지 2</button>
    <button data-image-src="https://via.placeholder.com/400x250/ffc107/000000">이미지 3</button>
  </div>
</div>
```

```javascript
// 갤러리 컨테이너에서 이벤트 위임 사용
document.getElementById('gallery').addEventListener('click', function(event) {
  // 클릭된 요소가 버튼이고, data-image-src 속성을 가지고 있는지 확인
  if (event.target.tagName === 'BUTTON' && event.target.dataset.imageSrc) {
    const mainImage = document.getElementById('main-image');
    const newImageSrc = event.target.dataset.imageSrc;
    
    // 메인 이미지의 src 속성을 변경
    mainImage.src = newImageSrc;
    
    console.log(`이미지가 ${newImageSrc}로 변경되었습니다.`);
    console.log('선택된 버튼의 dataset:', event.target.dataset); // { imageSrc: "..." }
  }
});
```

> [!TIP]
> `data-*` 속성은 클래스나 ID와 달리, 스타일링이나 스크립팅을 위한 **상태 정보**나 **메타데이터**를 저장하는 데 사용하는 것이 좋습니다. 요소의 역할을 나타낼 때는 시맨틱 태그나 클래스를 사용하는 것이 더 적절합니다.
