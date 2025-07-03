<img src="./header.png" />

# 1일차: 웹 디자인 기초 및 Figma 시작하기

## 5교시: Git/GitHub 초기 설정 및 결과물 업로드

### 1. Git 기본 개념 소개 (로컬 저장소, 원격 저장소)

웹 디자인 결과물을 효과적으로 관리하고 공유하기 위해 버전 관리 시스템인 Git이 필수적입니다.

- **Git (깃) 이란?**
  - **버전 관리 시스템 (Version Control System, VCS):** 파일의 변경 이력을 추적하고 관리하는 도구입니다. 모든 변경 사항을 자동으로 기록하고 필요 시 특정 시점으로 되돌릴 수 있습니다.
  - **협업의 필수 도구:** 여러 개발자나 디자이너가 같은 프로젝트를 동시에 작업할 때, 변경 사항의 충돌을 방지하고 효율적인 병합을 지원합니다.
- **로컬 저장소 (Local Repository):**
  - **정의:** Git이 관리하는 프로젝트 파일들이 저장된 사용자 컴퓨터 내의 공간입니다. 모든 변경 이력(버전)이 이곳에 저장됩니다.
  - **Git Bash/Terminal:** 로컬 저장소에서 Git 명령어를 사용하여 버전을 생성하고 관리할 수 있습니다.
- **원격 저장소 (Remote Repository):**
  - **정의:** 로컬 저장소의 내용을 인터넷 상에 저장해두는 공간입니다. 여러 사람이 공유하고 접근할 수 있어 협업과 백업에 활용됩니다.
  - **GitHub (깃허브):** 가장 대표적인 원격 저장소 호스팅 서비스입니다. Git 저장소를 생성하고 관리하며, 다른 사람들과 코드를 공유하고 협업할 수 있는 웹 기반 플랫폼입니다.
- **Git과 GitHub의 관계 (클라이언트-서버 비유):**
  - **Git:** 사용자 컴퓨터에 설치되어 파일의 변경 이력을 관리하는 '도구'인 버전 관리 프로그램입니다.
  - **GitHub:** Git으로 작업한 결과물을 업로드하고 다른 사람들과 공유할 수 있는 '플랫폼'인 웹 서비스입니다.

### 2. GitHub 계정 생성 및 첫 번째 레포지토리 생성

금일 생성한 Figma 결과물 업로드를 위해 GitHub 계정을 생성하고 원격 저장소를 생성합니다.

- **GitHub 계정 생성:**
  - `github.com` 접속.
  - `Sign up` 버튼 클릭하여 회원가입 시작.
  - 이메일 주소, 비밀번호, 사용자 이름 입력 (사용자 이름은 GitHub 주소에 포함되므로 신중하게 선택).
  - 이메일 인증 및 필요한 경우 로봇이 아님을 증명하는 퍼즐 해결.
  - 설문 완료 후 계정 생성 마무리.
  - (참고: 학생들에게 미리 계정 생성을 권장했으나, 미생성 학생을 위해 여유 시간 제공)
- **첫 번째 레포지토리 (Repository) 생성:**
  - **레포지토리 정의:** 프로젝트의 모든 파일과 변경 이력이 저장되는 공간.
  - 로그인 후 대시보드에서 `New` 버튼 클릭.
  - **레포지토리 이름 설정:**
    - `Repository name`: `figma-1day-results` (예시) 또는 `web-design-bootcamp-day1` (알아보기 쉬운 영어 소문자, 하이픈 권장).
    - **설명 (Optional):** "1일차 웹 디자인 기초 및 Figma 실습 결과물"과 같이 간단히 설명 추가.
  - **Public/Private 선택:**
    - **Public:** 누구나 저장소 내용 열람 가능 (과제 제출 시 권장).
    - **Private:** 계정 소유자 및 초대된 사용자만 열람 가능.
  - `Add a README file` 선택 (저장소 설명 파일 자동 생성).
  - `Add .gitignore`, `Choose a license`는 현재 단계에서는 `None`으로 설정.
  - `Create repository` 클릭하여 레포지토리 생성 완료.

### 3. Git Clone 및 로컬 환경 설정 (VS Code 연결)

GitHub에 생성된 원격 저장소를 사용자 컴퓨터로 복제(Clone)하고 VS Code와 연결합니다.

- **Git 설치 확인:**
  - 터미널(Windows: Git Bash 또는 PowerShell, macOS: Terminal)을 열고 `git --version` 입력하여 Git 설치 여부 확인. 미설치 시 Git 공식 웹사이트에서 다운로드 및 설치 필요.
  - (팁: 대부분의 컴퓨터에 Git이 설치되어 있음을 안내하고, 미설치 시 대기 시간 제공)
- **원격 저장소 Clone (복제):**
  - GitHub 레포지토리 페이지에서 `Code` 버튼 클릭.
  - `HTTPS` 탭 선택 후 URL 주소 복사.
  - 로컬 폴더 생성: 레포지토리 저장용 폴더(`Documents/web-design-bootcamp` 등) 생성 및 이동.
  - 터미널 열기: 해당 폴더 안에서 마우스 오른쪽 버튼 클릭 > `Git Bash Here` (Windows) 또는 터미널 열어 해당 폴더로 이동.
  - **Clone 명령어 실행:** 터미널에 다음 명령어 입력 후 `Enter`.
    ```bash
    git clone [복사한 HTTPS 주소]
    # 예시: git clone https://github.com/your-username/figma-1day-results.git
    ```
  - 확인: 명령어가 성공적으로 실행되면, 해당 폴더 안에 GitHub 레포지토리와 동일한 이름의 새 폴더가 생성됨을 확인.
- **VS Code로 폴더 열기:**
  - Visual Studio Code 실행.
  - `File` > `Open Folder...` 클릭 후, 방금 Git Clone으로 생성된 레포지토리 폴더(`figma-1day-results` 등) 선택하여 열기.
  - Git 연동 확인: VS Code 좌측 하단에 현재 Git 브랜치 이름(main 또는 master)이 표시되는지 확인. 좌측 'Source Control' (세 갈래 화살표) 아이콘 클릭하여 Git 패널 확인.

### 4. 학생별 브랜치 생성 및 Figma 결과물 업로드

각자 Figma 결과물을 업로드할 개별 공간(브랜치)을 생성하고 파일을 업로드합니다.

- **브랜치 (Branch) 생성:**
  - **브랜치 정의:** 독립적인 작업 공간을 생성하는 기능. 메인 코드에 영향을 주지 않고 새로운 기능 개발 또는 디자인 수정 시 사용.
  - **생성 방법:**
    - VS Code 터미널 또는 Git Bash에서 해당 레포지토리 폴더로 이동.
    - 다음 명령어를 입력하여 새 브랜치 생성 및 이동.
    <!-- end list -->
    ```bash
    git branch [본인이름-day1]
    # 예시: git branch gildonghong-day1
    git checkout [본인이름-day1]
    # 예시: git checkout gildonghong-day1
    # 또는 한 번에: git checkout -b [본인이름-day1]
    ```
    - VS Code 좌측 하단의 브랜치 이름이 변경된 것을 확인.
- **Figma 결과물 내보내기 (Export):**
  - Figma에서 공유할 프레임이나 디자인 요소 선택 (예: 4교시에서 만든 와이어프레임 프레임 전체).
  - `Export` 설정: 우측 속성 패널의 `Export` 섹션에서 `+` 버튼 클릭.
  - **형식 선택:**
    - **PNG (권장):** 투명 배경 불필요 및 고화질 이미지 원할 때.
    - **JPG:** 배경 투명도 불필요 및 파일 크기 감소 원할 때.
    - **Figma File (.fig):** Figma 원본 파일 공유 시.
  - `Export` 클릭: 저장할 폴더 지정 (Git Clone한 레포지토리 폴더 안에 `day1_results`와 같은 새 폴더 생성하여 저장 권장).
- **Git으로 결과물 업로드 (Add, Commit, Push):**
  - **파일 추가 (Add):** 변경된 파일(Export한 이미지 파일)을 Git이 추적하도록 준비.
    ```bash
    git add .
    # 또는 특정 파일만: git add day1_results/my-wireframe.png
    ```
  - **버전 기록 (Commit):** 변경 사항을 하나의 의미 있는 단위로 기록.
    ```bash
    git commit -m "feat: 1일차 Figma 와이어프레임 결과물 추가"
    # -m 다음의 메시지는 해당 커밋이 어떤 변경을 담고 있는지 설명합니다.
    ```
  - **원격 저장소로 전송 (Push):** 로컬 저장소에 기록된 변경 사항을 GitHub 원격 저장소로 전송.
    ```bash
    git push origin [본인이름-day1]
    # 예시: git push origin gildonghong-day1
    ```
    - (첫 `push` 시 GitHub 사용자 이름과 비밀번호 또는 Personal Access Token을 요구할 수 있습니다.)
- **GitHub에서 결과물 확인:**
  - GitHub 웹사이트의 본인 레포지토리 페이지로 이동하여, 방금 `push`한 브랜치로 전환 시 업로드된 파일 확인 가능.
  - **Pull Request 생성 (선택 사항):** 이후 `main` 브랜치에 본인의 작업을 병합하고 싶을 때 `Pull Request` 생성.
