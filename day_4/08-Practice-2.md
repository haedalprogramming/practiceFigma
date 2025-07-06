<img src="./header.png" />

# 7. 실습 2: CSS 상대 위치, 절대 위치

## 7.1 위치 지정의 기본 개념

HTML에서 요소의 위치를 자유롭게 조정하기 위해 CSS에서는 `position` 속성을 사용합니다. 대표적인 두 가지 방식:

| 속성       | 설명                                                                                  |
| ---------- | ------------------------------------------------------------------------------------- |
| `relative` | 현재 위치를 기준으로 이동. 원래 공간은 유지됨.                                        |
| `absolute` | 가장 가까운 `position`이 지정된 조상 기준으로 정확한 위치에 배치. 공간 차지하지 않음. |

## 7.2 기본 예시: 배지 뱃지 만들기

> 버튼에 숫자 뱃지를 절대 위치로 올려보는 실습입니다.

### HTML 구조

```html
<div class="badge-container">
  <button class="btn">알림</button>
  <div class="badge">3</div>
</div>
```

### CSS 스타일

```css
.badge-container {
  position: relative; /* 기준이 되는 부모 요소 */
  display: inline-block;
}

.btn {
  padding: 12px 24px;
  font-size: 16px;
}

.badge {
  position: absolute; /* 부모인 .badge-container 기준으로 배치됨 */
  top: -8px;
  right: -8px;
  background-color: red;
  color: white;
  font-size: 12px;
  padding: 4px 8px;
  border-radius: 50%;
}
```

## 7.3 시각적 이해

> 강사의 화면으로 직접 보여줍니다

- `relative`는 기준을 제공함
- `absolute`는 부모의 `relative` 위치를 기준으로 좌표 이동

## 7.4 실습 예제 2: 절대 위치로 요소 배치

### HTML

```html
<div class="box">
  <div class="inner-box">Hi!</div>
</div>
```

### CSS

```css
.box {
  width: 300px;
  height: 200px;
  background-color: lightblue;
  position: relative;
}

.inner-box {
  width: 100px;
  height: 50px;
  background-color: coral;
  position: absolute;
  bottom: 0;
  right: 0;
}
```

📌 `inner-box`는 `box`의 오른쪽 아래에 정확히 고정됩니다.

## 7.5 참고 표: position 속성 요약

| 속성     | 설명                                         |
| -------- | -------------------------------------------- |
| static   | 기본값. 위치 조정 불가                       |
| relative | 원래 위치 기준으로 이동. 공간 차지 유지      |
| absolute | 부모 기준 위치 고정. 공간 차지하지 않음      |
| fixed    | 화면(Viewport) 기준 위치 고정                |
| sticky   | 스크롤 시 특정 위치에 고정됨 (스크롤 반응형) |

## 실습 과제 제안

아래 구조를 CSS로 구현해보세요.

```plaintext
[ 카드 ]
┌──────────────────────────────┐
│ 제목                         ⓘ  <- 절대 위치 아이콘
│ 내용 내용 내용                 │
└──────────────────────────────┘
```

- 카드 내부 오른쪽 상단에 `ⓘ` 아이콘 배치
- `position: absolute` 사용하여 위치 고정
- 카드 내용은 자유롭게 변경되더라도 아이콘은 항상 고정된 위치에 있어야 함
