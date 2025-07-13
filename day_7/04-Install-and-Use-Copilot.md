<img src="./header.png" />

# 04. Copilot 설치 및 사용하기

> [!NOTE]
> 이 문서는 AI 기반 코드 생성 도구인 GitHub Copilot을 설치하고 사용하는 방법을 설명합니다. 이는 Figma에서 디자인된 MCP를 실제 코드로 구현하는 데 도움을 줄 수 있습니다.

## 4.1. GitHub Copilot이란?

GitHub Copilot은 OpenAI의 Codex 모델을 기반으로 하는 AI 페어 프로그래머입니다. 주석이나 코드의 맥락을 분석하여 실시간으로 코드 제안을 제공하며, 다양한 프로그래밍 언어와 프레임워크를 지원합니다.

- **코드 자동 완성**: 작성 중인 코드에 대한 다음 줄 또는 전체 함수를 제안합니다.
- **주석을 코드로 변환**: 자연어 주석을 기반으로 코드를 생성합니다.
- **다양한 언어 지원**: Python, JavaScript, TypeScript, Go, Ruby 등 여러 언어에서 작동합니다.
- **학습 및 개선**: 사용자의 코딩 스타일과 패턴을 학습하여 시간이 지남에 따라 더 정확한 제안을 제공합니다.

## 4.2. Copilot 설치 및 활성화

GitHub Copilot은 주로 Visual Studio Code(VS Code) 확장 프로그램으로 제공됩니다. [Day 4: Visual Studio Code](./../day_4/04-Visual-Studio-Code.md)에서 VS Code 설치 방법을 학습했습니다.

1.  **GitHub Copilot 구독**: GitHub Copilot은 유료 서비스이며, GitHub Copilot 웹사이트에서 구독을 활성화해야 합니다. (학생 및 교직원은 무료로 이용 가능합니다.)
2.  **VS Code 열기**: Visual Studio Code를 실행합니다.
3.  **확장 프로그램 설치**: VS Code 좌측 사이드바에서 `Extensions` 아이콘 (네모 4개)을 클릭합니다.
4.  **Copilot 검색 및 설치**: 검색창에 `GitHub Copilot`을 입력하고 검색 결과에서 `GitHub Copilot` 확장을 찾아 `Install` 버튼을 클릭합니다.
5.  **GitHub 계정 연동**: 설치가 완료되면 VS Code 하단 상태 바에 Copilot 아이콘이 나타납니다. 아이콘을 클릭하여 GitHub 계정에 로그인하고 Copilot을 활성화합니다.

## 4.3. Copilot 사용 방법

Copilot은 코드를 작성하는 동안 자동으로 제안을 제공합니다. 제안된 코드를 수락하거나 무시할 수 있습니다.

- **자동 완성**: 코드를 입력하기 시작하면 Copilot이 회색 텍스트로 코드 제안을 표시합니다. `Tab` 키를 눌러 제안을 수락할 수 있습니다.
- **여러 제안 보기**: 여러 가지 제안이 있는 경우, `Alt + [` 또는 `Alt + ]` (Windows/Linux) / `Option + [` 또는 `Option + ]` (macOS)를 눌러 다른 제안을 탐색할 수 있습니다.
- **주석을 코드로**: 원하는 기능에 대한 설명을 주석으로 작성하면 Copilot이 해당 주석을 기반으로 코드를 제안합니다.

    ```python
    # Function to calculate the factorial of a number
    def factorial(n):
        # Copilot이 여기에 코드를 제안할 수 있습니다.
    ```

- **Figma 디자인을 코드로**: Figma에서 디자인된 UI 컴포넌트의 구조나 스타일을 주석으로 설명하면, Copilot이 해당 설명을 기반으로 HTML, CSS, JavaScript 코드를 제안할 수 있습니다. 이는 [Figma MCP](./03-Figma-MCP.md)를 실제 코드로 전환하는 데 유용합니다.

> [!TIP]
> Copilot은 강력한 도구이지만, 생성된 코드를 항상 검토하고 이해하는 것이 중요합니다. AI가 생성한 코드가 항상 완벽하거나 최적의 솔루션은 아닐 수 있습니다.

> [!NOTE]
> 다음 내용인 [Figma MCP 설치 및 사용하기](./05-Install-and-Use-Figma-MCP.md)에서는 Figma 디자인을 코드로 변환하는 데 특화된 Figma MCP 플러그인을 설치하고 사용하는 방법을 학습합니다.
