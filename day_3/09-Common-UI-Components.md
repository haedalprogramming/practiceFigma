<img src="./header.png" />

# 9. 자주 쓰는 UI 컴포넌트

> [!NOTE]  
> 이 문서에서는 [재사용 가능한 디자인](./07-Reusable-Design.md)과 연계하여 자주 쓰이는 UI 컴포넌트를 소개합니다.  
> 자주 쓰이는 요소는 Figma에서 컴포넌트로 제작하여 효율적이고 일관된 디자인 시스템을 구축할 수 있습니다.

## 9.1. UI 컴포넌트란?

- **정의:** 사용자 인터페이스를 구성하는 기본 요소를 말합니다.
- **목적:** 일관된 UI 구성 및 사용자 경험 향상, 유지보수와 협업의 효율 증가.
- **컴포넌트화:** 자주 쓰이는 요소를 컴포넌트로 만들면 수정이 전체에 반영되어 효율적인 관리 가능.

## 9.2. 자주 쓰이는 컴포넌트 예시

### 1) **버튼 (Button)**

- 클릭 가능한 가장 기본적인 UI 요소.
- **상태별 구성:** 기본(Default), 호버(Hover), 비활성(Disabled), 로딩(Loading).
- **크기/색상 분류:** Primary, Secondary, Danger, Small, Large 등.

### 2) **입력창 (Input Field)**

- 사용자의 텍스트 입력을 위한 필드.
- **구성 요소:** Placeholder, Label, Error Message, 아이콘 등.
- **상태:** Focus, Disabled, Error, Valid.

### 3) **체크박스 / 라디오 버튼 (Checkbox / Radio Button)**

- 다중 선택 또는 단일 선택을 위한 요소.
- 선택 여부에 따른 시각적 피드백 필수.

### 4) **토글 스위치 (Toggle Switch)**

- On/Off 상태를 직관적으로 표현하는 컴포넌트.
- 설정 화면이나 기능 제어에 많이 사용됨.

### 5) **탭 (Tabs)**

- 콘텐츠를 구분하여 보여주는 UI.
- 선택된 탭은 강조되고, 관련 콘텐츠만 보여짐.

### 6) **드롭다운 (Dropdown)**

- 여러 항목 중 하나를 선택할 수 있는 컴포넌트.
- 펼침/접힘 상태를 디자인으로 명확히 표현해야 함.

### 7) **모달 (Modal)**

- 화면 위에 나타나는 팝업 형태의 UI.
- 경고, 확인, 정보 입력 등 특정 작업에 집중할 수 있도록 함.

### 8) **툴팁 (Tooltip)**

- 사용자가 마우스를 올렸을 때 추가 정보를 제공하는 작은 UI.
- 복잡한 설명 없이도 직관적인 사용자 가이드 가능.

## 9.3. 컴포넌트 디자인 시 고려사항

- **접근성:** 색 대비, 키보드 접근성, 시각적 명확성.
- **반응성:** 다양한 디바이스에서도 잘 작동하도록 Auto Layout, Constraints 설정.
- **상태 디자인:** 모든 가능한 상태(기본, hover, active, disabled 등)를 미리 디자인.

> [!NOTE]  
> 상태 디자인은 [Component Set](./11-Component-Set.md)에서 상세히 기술합니다.

## 9.4. Figma에서의 컴포넌트 활용

- 컴포넌트로 설정한 후 `Instance`를 활용하여 여러 곳에서 재사용 가능.
- 하나의 컴포넌트를 수정하면 전체 인스턴스에 자동 반영됨.
- `Variants` 기능을 활용하여 한 컴포넌트에 여러 상태를 통합 가능 (예: 버튼 상태별 통합).

> [!TIP]  
> 자주 쓰는 컴포넌트를 프로젝트 초기에 잘 정의하면, 디자인 시스템을 더욱 견고하게 만들 수 있습니다.
