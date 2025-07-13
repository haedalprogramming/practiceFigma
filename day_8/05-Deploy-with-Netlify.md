<img src="./header.png" />

# 05. Netlify로 자신의 프로젝트 배포하기

> [!NOTE]
> 이 문서는 GitHub에 업로드된 웹 프로젝트를 Netlify를 사용하여 온라인에 배포하는 방법을 설명합니다. [완성된 디자인을 AI로 구현하고 GitHub에 올리기](./04-AI-Implementation-and-GitHub.md)에서 GitHub에 올린 코드를 실제 웹사이트로 만드는 단계입니다.

## 5.1. 웹 호스팅 및 배포란?

웹 호스팅은 웹사이트의 파일(HTML, CSS, JavaScript, 이미지 등)을 서버에 저장하여 인터넷을 통해 사용자들이 접근할 수 있도록 하는 서비스입니다. 배포(Deployment)는 개발된 웹 프로젝트를 웹 호스팅 서버에 업로드하여 실제 서비스로 만드는 과정을 의미합니다.

Netlify는 정적 웹사이트(Static Website)를 빠르고 쉽게 배포할 수 있도록 돕는 플랫폼입니다. GitHub, GitLab, Bitbucket과 같은 Git 저장소와 연동하여 코드가 업데이트될 때마다 자동으로 웹사이트를 재배포하는 CI/CD(Continuous Integration/Continuous Deployment) 기능을 제공합니다.

## 5.2. Netlify를 이용한 배포 단계

### 5.2.1. Netlify 계정 생성 및 로그인

1.  **Netlify 웹사이트 접속**: [Netlify](https://www.netlify.com/)에 접속합니다.
2.  **회원가입/로그인**: `Sign up` 또는 `Log in` 버튼을 클릭하여 계정을 생성하거나 로그인합니다. GitHub 계정으로 로그인하는 것이 가장 편리합니다.

### 5.2.2. GitHub 저장소 연결

1.  **새 사이트 생성**: Netlify 대시보드에서 `Add new site` 버튼을 클릭하고 `Import an existing project`를 선택합니다.
2.  **Git 공급자 선택**: `GitHub`를 선택합니다. (또는 프로젝트가 있는 다른 Git 서비스)
3.  **저장소 선택**: Netlify가 GitHub 저장소에 접근할 수 있도록 권한을 부여한 후, 배포하고 싶은 프로젝트 저장소([GitHub에 내 코드 올리기](./04-AI-Implementation-and-GitHub.md)에서 올린 저장소)를 선택합니다.

### 5.2.3. 배포 설정

선택한 저장소에 대한 배포 설정 화면이 나타납니다.

1.  **Branch to deploy**: 배포할 브랜치를 선택합니다. 일반적으로 `main` 또는 `master` 브랜치를 선택합니다.
2.  **Build command**: 프로젝트를 빌드하는 명령어를 입력합니다. HTML, CSS, JavaScript로만 구성된 정적 웹사이트의 경우 빌드 명령어가 필요 없을 수 있습니다. (비워둡니다.)
3.  **Publish directory**: 빌드된 파일이 위치하는 디렉토리를 지정합니다. 일반적으로 프로젝트 루트 디렉토리(`./`) 또는 `dist`, `build`, `public` 등입니다. (프로젝트 구조에 따라 다름)
4.  **Deploy site**: 모든 설정을 확인한 후 `Deploy site` 버튼을 클릭합니다.

### 5.2.4. 배포 확인 및 사이트 접속

- Netlify가 프로젝트를 빌드하고 배포하는 과정이 진행됩니다. 몇 분 정도 소요될 수 있습니다.
- 배포가 완료되면, Netlify가 자동으로 생성해준 URL을 통해 자신의 웹사이트에 접속할 수 있습니다. (예: `https://your-random-name.netlify.app`)
- `Site settings`에서 `Domain management`를 통해 원하는 도메인으로 변경할 수도 있습니다.

## 5.3. 지속적인 배포 (Continuous Deployment)

Netlify는 Git 저장소와 연동되어 있어, GitHub에 코드를 푸시할 때마다 자동으로 웹사이트를 재배포합니다. 이는 개발자가 수동으로 배포할 필요 없이, 코드 변경 사항이 즉시 웹사이트에 반영되도록 합니다.

1.  **코드 변경 및 푸시**: 로컬에서 프로젝트 코드를 수정하고 GitHub에 푸시합니다. ([GitHub에 내 코드 올리기](./04-AI-Implementation-and-GitHub.md) 참고)
2.  **Netlify 자동 배포**: GitHub에 푸시된 변경 사항을 Netlify가 감지하여 자동으로 새로운 버전의 웹사이트를 빌드하고 배포합니다.
3.  **변경 사항 확인**: 배포가 완료되면 웹사이트에 접속하여 변경 사항이 반영되었는지 확인합니다.

> [!TIP]
> Netlify는 정적 웹사이트 배포에 매우 강력하고 편리한 도구입니다. 무료 플랜으로도 충분히 많은 기능을 활용할 수 있으니, 적극적으로 사용해보세요.

> [!NOTE]
> 다음 내용인 [발표 및 GitHub Issue를 활용한 동료 피드백](./06-Presentation-and-Feedback.md)에서는 완성된 프로젝트를 동료들에게 발표하고, GitHub Issue를 활용하여 건설적인 피드백을 주고받는 방법을 학습합니다.
