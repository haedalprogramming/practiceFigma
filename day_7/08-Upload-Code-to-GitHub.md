<img src="./header.png" />

# 08. GitHub에 내 코드 올리기

> [!NOTE]
> 이 문서는 로컬 컴퓨터에 있는 프로젝트 코드를 GitHub 원격 저장소에 올리는 구체적인 방법을 설명합니다. [Git과 GitHub](./07-Git-and-GitHub.md)에서 배운 기본 개념을 바탕으로 합니다.

## 8.1. GitHub 저장소 생성

1.  **GitHub 접속**: 웹 브라우저를 열고 [GitHub](https://github.com/)에 접속하여 로그인합니다.
2.  **새 저장소 생성**: GitHub 메인 페이지에서 `New` 버튼 (또는 `+` 아이콘)을 클릭하여 `New repository`를 선택합니다.
3.  **저장소 설정**: 다음 정보를 입력하고 `Create repository` 버튼을 클릭합니다.
    - **Repository name**: 프로젝트 이름 (예: `my-first-web-project`)
    - **Description (optional)**: 저장소에 대한 간단한 설명
    - **Public/Private**: 공개 여부 선택 (일반적으로 `Public`으로 시작)
    - **Add a README file**: `README.md` 파일을 자동으로 생성할지 여부 (선택 사항, 나중에 추가할 수도 있습니다.)
    - **Add .gitignore**: 프로젝트에 맞는 `.gitignore` 템플릿 선택 (예: `Node`, `Python` 등)
    - **Choose a license**: 라이선스 선택 (선택 사항)

## 8.2. 로컬 프로젝트 Git 초기화 및 연결

이제 로컬 컴퓨터에 있는 프로젝트 폴더를 GitHub 저장소와 연결할 차례입니다.

1.  **터미널/명령 프롬프트 열기**: 프로젝트 폴더로 이동하여 터미널 또는 명령 프롬프트를 엽니다.
2.  **Git 초기화**: 프로젝트 폴더를 Git 저장소로 초기화합니다.
    ```bash
    git init
    ```
3.  **원격 저장소 연결**: GitHub에서 생성한 저장소의 URL을 복사하여 로컬 저장소에 연결합니다.
    ```bash
    git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPOSITORY_NAME.git
    # YOUR_USERNAME과 YOUR_REPOSITORY_NAME을 실제 값으로 변경하세요.
    ```
4.  **파일 추가 및 커밋**: 프로젝트의 모든 파일을 Git에 추가하고 첫 번째 커밋을 생성합니다.
    ```bash
    git add .
    git commit -m "Initial commit"
    ```

## 8.3. GitHub에 코드 푸시

로컬 저장소의 코드를 GitHub 원격 저장소에 업로드합니다.

1.  **브랜치 이름 확인**: 기본 브랜치 이름이 `main`인지 `master`인지 확인합니다. (GitHub는 최근 `main`을 기본으로 사용합니다.)
    ```bash
    git branch -M main # 만약 기본 브랜치가 master라면 이 명령어를 사용하지 않아도 됩니다.
    ```
2.  **코드 푸시**: 로컬 저장소의 코드를 GitHub에 푸시합니다.
    ```bash
    git push -u origin main
    # 또는 git push -u origin master (기본 브랜치 이름에 따라)
    ```
    - `-u` 옵션은 `origin` 원격 저장소의 `main` 브랜치를 추적하도록 설정하여, 다음부터는 `git push`만 입력해도 됩니다.

## 8.4. 변경 사항 업데이트

프로젝트를 계속 개발하면서 변경 사항이 생기면 다음 단계를 반복합니다.

1.  **파일 변경**: 코드를 수정하거나 새로운 파일을 추가합니다.
2.  **변경 사항 확인**: `git status` 명령어로 변경된 파일을 확인합니다.
3.  **파일 추가**: `git add .` 또는 `git add <파일 이름>`으로 변경된 파일을 스테이징 영역에 추가합니다.
4.  **커밋**: `git commit -m "변경 내용 요약"`으로 변경 사항을 커밋합니다.
5.  **푸시**: `git push` 명령어로 GitHub에 변경 사항을 업로드합니다.

> [!TIP]
> GitHub에 코드를 올리는 것은 협업과 버전 관리를 위한 첫걸음입니다. 꾸준히 커밋하고 푸시하는 습관을 들이세요.

> [!NOTE]
> 다음 내용인 [실습 1: 랜딩 페이지 만들기](./09-Practice-1-Landing-Page.md)에서는 지금까지 배운 Figma 디자인과 AI 도구, 그리고 Git/GitHub를 활용하여 간단한 랜딩 페이지를 만드는 실습을 진행합니다.
