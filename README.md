# class TeamO2BackendDeveloperOnboardingHelper

**Welcome to the Teamo2 Backend World !**  

> "레거시 코드는 어제 짠 코드다"  

하루 하루 성장해 나갈 수 있는, 성장해 나가고 있는 팀오투의 백엔드를 맡고 있는 곳에 오신 것을 환영합니다.  
신입이라면 멱살 잡고 성장을, 경력자라면 본인의 장기를 마음 껏 뿜뿜할 수 있는 곳을 지향하고 있습니다.  
🤝 잘 지내봅시다 🤝


## 목차
- [class TeamO2BackendDeveloperOnboardingHelper](#class-teamo2backenddeveloperonboardinghelper)
  - [목차](#목차)
  - [1. Tech Stack](#1-tech-stack)
  - [2. Git](#2-git)
    - [Git Flow](#git-flow)
      - [Git Flow 란 ?](#git-flow-란-)
    - [Git Branching 전략](#git-branching-전략)
    - [Git Rebase & Merge](#git-rebase--merge)
    - [Git Hooks](#git-hooks)
      - [세팅하는 법](#세팅하는-법)
      - [Commit Convention](#commit-convention)
  - [3. Our Coding GOAL](#3-our-coding-goal)
    - [주석 없는 코드](#주석-없는-코드)
    - [인간은 반복된 실수를 하는 동물](#인간은-반복된-실수를-하는-동물)
    - [Micro Service Architecture](#micro-service-architecture)
  - [4. Code Review](#4-code-review)
  - [5. DDD](#5-ddd)
  - [6. TDD](#6-tdd)

## 1. Tech Stack

첫 번째로, 간략하게 TeamO2 에서 개발 중인 서비스들을 나열하면서, 어떤 Stack 들을 가지고 있는지 알려드리도록 합죠 💁

> 서비스를 누르면, StackShare 링크로 이동해요.

렌트카 가격비교 1등 앱, [**카모아**](https://stackshare.io/teamo2/carmore)
팀오투 서비스의 숨은 1등 공신, [**파트너스**]()
구성원들의 업무 집중도를 최대로, [**운영툴**]()
분산화의 시발점이 된, [**내부API**]()
OTA의 Role, [**외부API**]()
업체들의 또다른 매출 성장동력, [**티켓**]()
제주 업체들의 고객 경험 향상, [**카모아TV**]()
[미오픈] 렌트카도 선물이 된다, 상품권


## 2. Git
### Git Flow

저희는 보다 보기편한 git history 관리 및 무슨이유로 gitflow 를 사용하고 있습니다. 



#### Git Flow 란 ?

Backend 의 막내, Steve 가 작성한 Repository 그 어떤 아티클보다 명료하게 정리가 잘 돼 있어요.  
[이리오세요](https://github.com/stevejkang/git-guideline#2-git-flow--branch)

- [ ] Gitflow 의 안좋은예, 좋은예 
- [ ] Gitflow 링크 말고 설명으로 적어보기


### Git Branching 전략
// 우리가 실제로 사용하고 있는 방법 위주로 설명하기

### Git Rebase & Merge

저희는 merge 방법 중 `--ff-only`를 사용하는 **rebase & fast-forward merge**를 사용하고 있어요.

<details>
  <summary>다른 merge 방법도 알려주세요!</summary>
    Merge의 종류에는 크게 아래와 같이 3가지 방법이 있어요.

    `--ff`
    `--no-ff`
    `--ff-only`

    각각은 아래와 같은 특징을 가지고 있어요.

    `--ff` 옵션은 현 브랜치와 병합할 브랜치가 fast-forward 관계라면 merge commit 없이 merge가 진행되고, 현 브랜치와 병합할 브랜치가 fast-forward 관계가 아니라면 merge commit을 남겨요.
    `--no-ff` 옵션은 fast-forward merge가 가능한 상황에서도 항상 merge commit을 남겨요.
    `--ff-only` 옵션은 fast-forward merge가 가능한 상황에만 merge를 진행하고, 그렇지 않을 경우 non-zero status로 종료돼요.

    만약, 특정 브랜치에서 선형적인 히스토리가 필요한 경우, squash 또는 rebase를 한 뒤에 merge를 진행해야 해요.
</details>

🙋‍♀️🙋‍♂️ : 왜요 ?
💁 : 우리가 작업하는 모든 feature들은 dev에 merge된 이후에는(= 서비스에 반영된 이후에는) _"어느 시점에 branch가 생성됐는 지"_, _"이 branch는 무슨역할을 하는지"_ 는 관심사가 아니에요.

이런 점들을 신경쓸 필요가 없기 때문에 dev/master 브랜치는 가지(branch) 모양이 일직선으로 이루어져 있게끔 하고 있어요. ~~그리고 이쁨~~

또, 주기적으로 작업 중인 브랜치를 후에 merge할 브랜치 _(주로 dev나 feature root 브랜치가 되겠죠)_ 에 rebase를 해주어야만 큰 프로젝트 단위에서 merge 시 conflict 해결에 드는 리소스도 최소화 할 수 있어요!

![rebase](https://user-images.githubusercontent.com/47936709/173546249-dbea4556-a6ac-4fd4-b1bd-45ea355d811d.png)


> **왜 Merge Commit을 남기지 않나요?**
> 
> Merge Commit은 원활한 rebase를 방해하고, 관리하는 데 어려움이 있어요. 또, merge할 때, merge하려고 하는 브랜치가 최신이 아닌 경우, remote branch를 기준으로 merge 하는 등, 이래서 안좋다.
> 
> 그래서 만약, 프로젝트를 진행하다가 아래와 같은 commit이 생겼다면 무언가 잘못되었다는 뜻이에요.
> ```
> (1) Merge pull request #2 from ${user}/${branch}
> (2) Merge branch '${branch}' of https://github.com/${user}/${repo} into ${branch}
> (3) Merge branch '${branch}' into ${branch}
> ```
>
> 1번의 경우 Pull Request를 머지할 때 rebase merge가 아니라 merge 


rebase를 잘 하려면, merge하는 브랜치(head branch)와 base branch의 local repository 상태는 remote repository와 일치해야 해요.

// reset --hard 옵션 설명

일치가 보장되면, base branch에서 아래 커맨드로 merge를 진행해요.
```bash
$ git merge --ff-only <branch>
```

그래서 보통 아래와 같은 순서로 작업이 이루어져요.

// 작업 flow command로 정리하기

### Git Hooks

🙋‍♀️🙋‍♂️ : Git 에 규칙이 있다는건 알겠슴다..! 근데 습관이 안들여져서 자꾸 실수할까 두렵고 무서워요ㅠㅠ  
💁 : Don't care ! 여러분이 잘 못 쓰면, 커밋이 안되도록, production/staging/develop 브랜치에 커밋 못 하도록 등등을 Git Hooks 에 세팅 해두었답니다.  
_예제는 아래에 쨔란~_

![커밋형태오류](https://user-images.githubusercontent.com/74130738/173327920-cd5f2d80-620a-4c24-8d19-529f8c688ba1.png)

#### 세팅하는 법

저장소를 pull 받으면 root directory 에 `init_repo.sh` 를 볼 수 있습니다.  
해당 shell 을 실행해주면 _The end_ 


#### Commit Convention

그러면 우리가 추구하는 Commit Convention 에 대해서 알아봅시다 !
Commit 에서 저희가 제일 중요하게 생각하는 것들은 아래와 같아요.

- **어떤 작업을 했는가**
- **어떤 이슈인가 ?**
- **그래서 무엇을 했는가 ?**

그래서, Commit Convention 도 그 중요도를 반영하기 위한 형태로 유지하고 있어요!

```
${COMMIT_TYPE}: (${${ISSUE_NUMBER} | NONE}) ${TITLE}

${OPTIONAL_BODY}

${OPTIONAL_REFERENCE}
```

For Example,
```
FIX: (DEV-1221) iOS에서 네이버페이 결제 오류 수정

아이폰에서 네이버페이로 결제 시도 시 네이버페이로 연결 안되는 현상 수정

ref: https://slack.com/adiekd/ds...
```

* COMMIT_TYPE: 어떤 커밋인가를 보여줘요
    * `FEAT`: 작업, 가장 기본적이고 가장 많이 쓰여요.
    * `FIX`: 버그 수정
    * `HOTFIX`: production 에서 긴급하게 발생한 버그 수정
    * `DOCS`: 문서를 만들거나 수정

## 3. Our Coding GOAL

### 주석 없는 코드

### 인간은 반복된 실수를 하는 동물
    
### Micro Service Architecture

해당 문서가 작성되는 시점 (22. 06) 에 저희는 Micro 하지 않아요.  
그러나, 느리지만 꾸준히 Monolithic 에서 하나 씩 떼어가고 있고, 무조건 MSA 를 해낼 것이예요  

**Monolithic 이 악이라는 소리를 하고 있는 것이 아닙니다.**  
팀오투, 카모아가 만들어지기 시작한 초창기에는 맞았던 아키텍쳐이지만, 개인의 역량이 성장하듯 사업의 성장세도 가파르기에, 사업의 변화/확장에 발맞춰 **우리도 변화할 뿐**입니다.  
그 작업이 고되고, 오래걸리더라도 더 관리하기 용이하게, 서비스 확장이 더 용이하게 하기 위함입니다. 

--

우리가 지향하는 바를 이루기 위해 아래의 행동들을 하고 있어. 거의 다 왔으니 좀만 힘내
블라블라


## 4. Code Review
모든 코드는 적절하고 효율적으로 구현됐는지, 잘 읽히는지 등을 모두가 코드리뷰를 통해 검토한 뒤에 배포가 이루어져요.

코드리뷰를 하는 목적은 작업물에 대한 책임을 작업자가 오롯이 떠안지 않고 리더급에게 위임하는 것도 있지만, 기능을 구성원 모두가 알 수 있게 되고, 궁극적으로는 모두의 성장을 이끌어 낼 수 있어요.

리뷰어가 리뷰를 남겼다고 해서 무조건 수용하는 것이 아닌 비판적 수용을 해야하며, 모든 관련 구성원의 의견이 일치해야 합니다. 그래서, 저희가 생각하는 코드리뷰는 **"이해" > "납득" > "공감"** 의 순서를 거쳐야만 합니다. 

**이해**: 어떤 리뷰를 남겼는지 이해가 된다.  
**납득**: 왜 이렇게 작성/변경 해야 하는지 납득이 된다.  
**공감**: 다른 상황에서 비슷한 케이스라면 남긴 리뷰처럼 코딩을 할 것 이다.  

> 한 줄의 코드라 할지라도, 의견을 남겨주세요 !  
> 그리고 본인의 생각을 말하고 피력해주세요 !


## 5. DDD

// 책 추천해주기.

## 6. TDD 


----

- git hooks
- git commit
- git flow


- DDD
    - DDD in NestJS
    - 네이밍 규칙 (내부 컨벤션)

- TDD
- 커뮤니케이션
- 지향 점
- [ ] 코드 지향 점
    - 주석 없는 코드
- [x] 코드리뷰 
- [ ] 정적분석
- [ ] IDE 포맷팅 (save in action)
    - e.g. 예를 들어, 탭 <-> 스페이스 같은 경우 사람마다 다르다



목적
- 리소스를 줄이고 싶다.
- Legacy가 순수악이 아니라는 것.


----

어떤 걸 하고 있어 -> 왜 하고 있어 -> 이건 이런거야. 필요하다면 예시

다 작성하고 할 것
- [ ] 맞춤법 검사
- [ ] 톤 맞추기 (~~ 해요?)
- [ ] 같은 단어에 대해 다르게 쓰지는 않았는지
