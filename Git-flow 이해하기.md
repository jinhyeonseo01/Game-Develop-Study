# Git-flow 이해하기

Git-flow는 Git 브랜치 관리 모델 중 하나이다. 하나의 프로젝트에서 팀원들이 원활하게 협업을 할 수 있다록 브랜치를 활용하느데, 이 Git 브랜치의 관리를 쉽게할 수 있도록 패턴을 적용한 것이 Git-flow 모델이다.

![Untitled](Git-flow%20%E1%84%8B%E1%85%B5%E1%84%92%E1%85%A2%E1%84%92%E1%85%A1%E1%84%80%E1%85%B5%201339439b972649dd97130d1a25e25f60/Untitled.png)

위는 Git-flow를 사용하는 프로젝트의 히스토리를 이미지로 나타낸 것이다. 해당 이미지에서 Master, Develop, Feature, Hotfix 라는 브랜치를 확인 할 수 있다.

<aside>
⚠️ 모든 프로젝트에서 위와 같은 브랜치가 사용되는 것은 아니다. 회사나 프로젝트마다 브랜치가 다를 수 있다.

</aside>

**핵심 브랜치**

- Master, Develop

**인스턴스 브랜치**

- Feature, Release, Hotfix

Git-flow에서 브랜치는 계속 업데이트하여 유지되는지에 따라 위와 같이 두 가지로 나눌 수 있다. **Master**, **Develop** 브랜치는 계속 업데이트되어 뻗어 나가지만 **Feature, Release, Hotfix** 브랜치는 핵심 브랜치에서 분기되었다가 합쳐지고 사라진다.

---

## Git-flow branch

각 브랜치의 목적은 아래와 같다.

### Master

- 실제 서비스에 배포되는 브랜치이다.

### Develop

- 새 버전에 대한 개발을 진행하는 브랜치이다.

### Feature

- 개발의 기본 단위인 기능을 추가하기 위한 브랜치이다.
- Develop에서 분기되어 Develop에 합쳐진다.

### Release

- Develop에서 새 버전에 대한 개발이 마무리 되어 출시하기 위한 브랜치다.
- Develop에서 분기되어 Master와 Develop으로 합쳐진다.

### Hotfix

- Master에서 생긴 버그를 급하게 해결하기 위한 브랜치이다.
- Master에서 분기되어 Master와 Develop으로 합쳐진다.

**Master, Develop** 브랜치는 실제로 배포하거나 개발자들이 공유하기 위해 보존되어야 하는 브랜치이다. 하지만 **Feature, Release, Hotfix** 브랜치는 Develop 또는 Master 브랜치를 업데이트하기 위한 수단이라는 걸 알 수 있다.****

---

## 시나리오

Git-flow를 사용해서 협업을 하는 몇 가지 시나리오를 준비했다.

1. 로그인 기능 제작 (Feature)
2. 1.0.0 버전 배포 (Release)
3. 배포된 서비스에서 발견된 버그 수정 (Hotfix)

### Feature : 로그인 기능 제작

Git-flow를 시작했다면 Develop 브랜치가 기본으로 세팅이 되어있다. Develop 브랜치에서 분기된 Feature 브랜치를 생성한다. 

Feature 브랜치 생성시 **Feature/** 라는 접두사를 붙여서 해당 브랜치의 목적을 분명하게 하는 것이 좋다.

이후 기능 개발이 완료되면 해당 Feature 브랜치를 다시 Develop 브랜치에 머지한다.

<aside>
⚠️ 이때 해당 머지의 변경점을 확인하여 자신이 작업한 내용만 올라가는지 확인하는 것이 좋다.

</aside>

### Release : 1.0.0 버전 배포

모든 기능을 완성하여 기능을 배포한다고 하자, Git flow를 통해 Release를 시작하고 Release 버전을 변경한다. 버전 관리는 회사나 팀 나름이지만, 해당 프로젝트에서는 **major.minor.hotfix** 형식을 사용할 것이다.

일반적으로 Release는 Develop 브랜치를 Master 브랜치에 반영하기 위한 브랜치이다. 하지만 Release를 열고 검토하는 도중에 문서를 추가하거나 에러를 고치는 등의 작업이 발생할 수도 있기때문에 이후에 Develop에도 다시 반영할 필요가 있다. 

### Hotfix : 배포된 서비스에서 발견된 버그 수정

v1.0.0이 배포된 이후 다음 버전 개발 도중 배포된 서비스 (Master 브랜치)에서 발견된 버그를 해결해야할 때를 가정해보자. Develop에서 버그를 수정하고 Release 한다면 다음에 배포하려했던 기능이 같이 배포될 것이다. 이때 Hotfix 브랜치를 이용할 수 있다.

Master 브랜치에서 Hotfix 브랜치를 생성하고 에러를 수정 후 마무리한다. 이후 Hotfix 브랜치는 Master와 Develop 브랜치에 각각 머지된다. 이러면 Develop 과는 별개로 Hotfix를 Master 브랜치에 반영할 수 있으며, 이 내용을 Develop에도 동기화 할 수 있다.