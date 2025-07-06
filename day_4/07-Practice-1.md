<img src="./header.png" />

# 7. 실습 1: CSS로 Auto Layout 구현하기

## 7.1 Figma의 [Auto Layout](/day_2/07-Auto-Layout.md) 개념 복습

- Auto Layout은 Figma에서 오브젝트의 **간격, 정렬, 크기 자동 조절**을 설정하여 반응형 UI를 빠르게 구성할 수 있도록 돕는 기능입니다.
- 예시: 버튼 안의 텍스트가 길어지면 버튼이 자동으로 늘어남, 여러 개의 카드 요소가 일정한 간격으로 정렬됨

## 7.2 CSS로 Auto Layout 기능 구현하기

Auto Layout의 핵심은 **Flexbox** 또는 **Grid**입니다. 이번 실습에서는 **Flexbox**로 구현합니다.

### 🎯 목표 디자인 구조

```plaintext
[Logo]         [Menu1] [Menu2] [Menu3]         [CTA Button]
```

> 좌측 정렬된 로고, 가운데 정렬된 메뉴들, 우측의 버튼
> 모든 요소는 반응형으로 중앙 정렬 + 간격 유지

## 7.3 기본 HTML 작성

```html
<body>
  <header class="navbar">
    <div class="logo">MyLogo</div>
    <nav class="menu">
      <a href="#">Menu1</a>
      <a href="#">Menu2</a>
      <a href="#">Menu3</a>
    </nav>
    <button class="cta">Sign Up</button>
  </header>
</body>
```

## 7.4 CSS Auto Layout 구현 (Flexbox)

```css
body {
  margin: 0;
  font-family: sans-serif;
}

.navbar {
  display: flex; /* Auto Layout 핵심 */
  justify-content: space-between; /* 요소 간 간격 자동 분배 */
  align-items: center; /* 수직 정렬 */
  padding: 16px 32px;
  background-color: #f8f8f8;
}

.menu {
  display: flex;
  gap: 24px; /* 메뉴 간 간격 설정 */
}

.menu a {
  text-decoration: none;
  color: #333;
}

.cta {
  background-color: #007aff;
  color: white;
  border: none;
  padding: 10px 20px;
  border-radius: 8px;
  cursor: pointer;
}
```

## 7.5 주요 포인트 정리

| Figma Auto Layout 기능       | HTML/CSS 구현 방식                      |
| ---------------------------- | --------------------------------------- |
| 가로 방향 정렬 (Row)         | `display: flex` + `flex-direction: row` |
| 세로 정렬                    | `flex-direction: column`                |
| 정렬 방식 설정 (좌/중/우)    | `justify-content` + `align-items`       |
| 간격 설정                    | `gap` 속성 사용                         |
| 안쪽 여백 (Padding)          | `padding` 속성                          |
| 컨텐츠에 맞게 자동 크기 조정 | `width: fit-content` or 기본            |

## 7.6 연습

가로 형식이 아닌 세로 형식의 Nav 바를 만들어보세요

- Flex로 상하 배치
