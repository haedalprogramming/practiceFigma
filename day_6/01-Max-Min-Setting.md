<img src="./header.png" />

# 01. Max/Min 설정

> [!NOTE]
> 이 문서는 Figma에서 Auto Layout 프레임의 크기를 조절할 때 `Max width/height` 및 `Min width/height` 속성을 활용하는 방법을 설명합니다. 이는 반응형 디자인을 더욱 정교하게 제어하는 데 필수적입니다.

## 1.1. Max/Min 속성의 이해

Figma의 Auto Layout 프레임은 기본적으로 `Hug contents` 또는 `Fill container`와 같은 크기 조절(Resizing) 속성을 가집니다. 여기에 `Max width/height` (최대 너비/높이)와 `Min width/height` (최소 너비/높이) 속성을 추가하여 프레임의 크기가 특정 범위 내에서만 조절되도록 제한할 수 있습니다.

- **`Max width/height`**: 프레임이 최대로 커질 수 있는 크기를 지정합니다. 이 값을 초과하여 커지지 않습니다.
- **`Min width/height`**: 프레임이 최소로 작아질 수 있는 크기를 지정합니다. 이 값 미만으로 작아지지 않습니다.

## 1.2. Max/Min 설정의 필요성

반응형 디자인에서 요소들이 무한정 커지거나 작아지는 것을 방지하고, 가독성 및 사용성을 유지하기 위해 Max/Min 설정이 중요합니다.

- **가독성 유지**: 텍스트 블록이 너무 넓어지거나 좁아지는 것을 방지하여 읽기 편한 너비를 유지합니다.
- **레이아웃 안정성**: 특정 요소가 너무 커져서 다른 요소들을 밀어내거나, 너무 작아져서 내용이 잘리는 것을 방지합니다.
- **디자인 일관성**: 컴포넌트의 크기 범위를 제한하여 디자인 시스템 내에서 일관된 사용성을 보장합니다.

## 1.3. Max/Min 설정 방법

1.  **Auto Layout 프레임 선택**: 크기를 제한하고 싶은 Auto Layout 프레임을 선택합니다.
2.  **Resizing 속성 변경**: 오른쪽 사이드바의 `Design` 패널에서 `Width` 또는 `Height` 속성을 `Fixed`가 아닌 `Hug contents` 또는 `Fill container`로 설정합니다.
3.  **Max/Min 값 입력**: `Width` 또는 `Height` 드롭다운 메뉴를 다시 클릭하면 `Min width`, `Max width`, `Min height`, `Max height` 입력 필드가 나타납니다. 원하는 값을 픽셀(px) 단위로 입력합니다.

## 1.4. 활용 예시

- **텍스트 블록**: 텍스트 프레임에 `Max width`를 설정하여 텍스트가 너무 길어져 가독성이 떨어지는 것을 방지합니다.
- **카드 컴포넌트**: 카드 컴포넌트에 `Min width`를 설정하여 내용이 줄어들더라도 카드가 너무 작아져서 디자인이 깨지는 것을 방지합니다.
- **반응형 컨테이너**: `Fill container`와 함께 `Max width`를 사용하여 컨테이너가 화면 크기에 따라 유연하게 늘어나되, 특정 크기 이상으로는 커지지 않도록 합니다.

> [!TIP]
> Max/Min 설정은 Auto Layout의 `Fill container` 속성과 함께 사용할 때 가장 강력한 시너지를 발휘합니다. 이를 통해 유연하면서도 제어 가능한 반응형 디자인을 구현할 수 있습니다.

> [!NOTE]
> 다음 내용인 [복습 1: Smart Animate로 부드러운 애니메이션 만들기](./02-Review-1-Smart-Animate.md)에서는 Figma의 Smart Animate 기능을 복습하고, 이를 활용하여 부드러운 UI 애니메이션을 만드는 방법을 학습합니다.
