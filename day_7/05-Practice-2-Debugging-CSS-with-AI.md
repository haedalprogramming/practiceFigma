<img src="./header.png" />

# 5. 실습 2: CSS 버그를 AI와 함께 해결해보기

> [!NOTE]
> 이 실습에서는 개발 중에 흔히 마주치는 CSS 버그 상황을 가정하고, AI에게 문제 해결을 요청하는 디버깅 과정을 경험해 봅니다. 문제 상황을 정확히 설명하고, 관련 코드를 제공하며, AI의 제안을 비판적으로 검토하여 문제를 해결하는 능력을 기르는 것이 목표입니다.

## 5.1. 문제 상황 (시나리오)

Flexbox를 사용하여 헤더를 만들고 있습니다. 왼쪽에는 로고, 오른쪽에는 네비게이션 메뉴를 배치하여 양쪽 끝으로 정렬하고 싶습니다. 그런데 의도와 달리, 네비게이션 메뉴 아이템들이 세로로 쌓여버리는 문제가 발생했습니다.

**[현재 코드]**

```html
<!-- index.html -->
<header class="site-header">
  <div class="logo">MyLogo</div>
  <nav class="main-nav">
    <a href="#">Home</a>
    <a href="#">About</a>
    <a href="#">Login</a>
  </nav>
</header>
```

```css
/* style.css */
.site-header {
  display: flex;
  justify-content: space-between; /* 양쪽 끝으로 정렬 */
  align-items: center; /* 세로 중앙 정렬 */
  padding: 1rem 2rem;
  background-color: #f8f8f8;
  border-bottom: 1px solid #ddd;
}

.main-nav a {
  margin-left: 1.5rem;
  text-decoration: none;
  color: #333;
}
```

**[버그 현상]**

-   `justify-content: space-between`이 제대로 작동하지 않는 것처럼 보입니다.
-   네비게이션 메뉴의 링크(`<a>`)들이 가로로 배치되지 않고 세로로 나열됩니다.

## 5.2. AI에게 디버깅 요청하기

문제 상황과 현재 코드를 명확하게 설명하여 AI에게 도움을 요청하는 프롬프트를 작성합니다.

**[프롬프트]**

> "너는 CSS, 특히 Flexbox 전문가야. 내가 작성한 헤더 코드에 버그가 있어. 도와줘.
> 
> **[내가 원하는 것]**
> -   헤더(`.site-header`) 안에서 로고(`.logo`)는 왼쪽에, 네비게이션 메뉴(`.main-nav`)는 오른쪽에 위치하도록 양쪽 끝으로 정렬하고 싶어.
> -   네비게이션 메뉴 안에 있는 링크(`<a>`)들은 가로로 나란히 배열되어야 해.
> 
> **[문제점]**
> -   현재 코드에서는 네비게이션 링크들이 가로가 아니라 세로로 쌓여서 표시돼.
> 
> **[전체 코드]**
> ```html
> <!-- HTML -->
> <header class="site-header">
>   <div class="logo">MyLogo</div>
>   <nav class="main-nav">
>     <a href="#">Home</a>
>     <a href="#">About</a>
>     <a href="#">Login</a>
>   </nav>
> </header>
> ```
> ```css
> /* CSS */
> .site-header {
>   display: flex;
>   justify-content: space-between;
>   align-items: center;
>   padding: 1rem 2rem;
>   background-color: #f8f8f8;
> }
> 
> .main-nav a {
>   margin-left: 1.5rem;
> }
> ```
> 
> **[요청]**
> -   이 버그의 원인이 무엇인지 설명해줘.
> -   문제를 해결하기 위한 수정된 CSS 코드를 보여줘."

## 5.3. AI의 답변 및 해결 과정 (예상)

AI는 제공된 코드를 분석하고 Flexbox의 동작 원리에 따라 다음과 같이 답변할 가능성이 높습니다.

> **[AI의 답변 예시]**
> 
> "안녕하세요! 제공해주신 코드를 분석했습니다. 버그의 원인과 해결 방법을 알려드릴게요.
> 
> **[버그 원인]**
> 
> 현재 `.site-header`에 `display: flex`가 적용되어 있습니다. 이로 인해 직계 자식인 `.logo`와 `.main-nav`는 Flex 아이템이 되어 가로로 배치됩니다. `justify-content: space-between`도 이 두 아이템을 양쪽 끝으로 밀어내는 역할을 잘 수행하고 있습니다.
> 
> 하지만, **문제는 `.main-nav` 자체**에 있습니다. `.main-nav`는 Flex 컨테이너가 아니기 때문에, 그 자식 요소인 `<a>` 태그들은 기본 블록(block) 또는 인라인(inline) 레벨 요소의 규칙에 따라 배치됩니다. `<a>` 태그는 인라인 요소이므로 가로로 배치될 것처럼 보이지만, Flex 아이템(`nav`) 안에서는 동작이 다를 수 있으며, 명시적으로 가로 배치를 지정해주는 것이 가장 확실합니다.
> 
> **[해결 방법]**
> 
> `.main-nav` 또한 Flex 컨테이너로 만들어, 그 자식인 `<a>` 태그들을 Flex 아이템으로 만들어주면 됩니다.
> 
> **[수정된 CSS 코드]**
> 
> ```css
> /* 기존 .site-header 스타일은 그대로 둡니다 */
> .site-header {
>   display: flex;
>   justify-content: space-between;
>   align-items: center;
>   padding: 1rem 2rem;
>   background-color: #f8f8f8;
> }
> 
> /* .main-nav에 display: flex 추가 */
> .main-nav {
>   display: flex; /* 자식 요소인 a 태그들을 flex 아이템으로 만듦 */
>   align-items: center; /* 세로 중앙 정렬 (선택 사항) */
> }
> 
> .main-nav a {
>   margin-left: 1.5rem;
>   text-decoration: none;
>   color: #333;
> }
> ```
> 
> **[수정 설명]**
> 
> `.main-nav`에 `display: flex`를 추가함으로써, `.main-nav`는 이제 그 자체로 Flex 컨테이너가 됩니다. 따라서 그 자식인 `<a>` 태그들이 가로 방향으로 나란히 정렬되게 됩니다. 이렇게 하면 원하셨던 레이아웃이 완성됩니다."

## 5.4. 결과 확인 및 적용

AI가 제안한 수정 코드를 적용하여 브라우저에서 확인합니다. 문제가 해결되었는지, 그리고 다른 부작용은 없는지 검토합니다. 이 과정을 통해 단순히 답을 얻는 것을 넘어, 왜 문제가 발생했는지(Flexbox의 중첩 구조)에 대한 근본적인 이해를 높일 수 있습니다.
