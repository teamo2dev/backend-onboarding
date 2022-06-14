# class TeamO2BackendDeveloperOnboardingHelper

**Welcome to the Teamo2 Backend World !**  

> "레거시 코드는 어제 짠 코드다"  

하루 하루 성장해 나갈 수 있는, 성장해 나가고 있는 팀오투의 백엔드를 맡고 있는 곳에 오신 것을 환영합니다.  
신입이라면 멱살 잡고 성장을, 경력자라면 본인의 장기를 마음 껏 뿜뿜할 수 있는 곳을 지향하고 있습니다.  
🤝 잘 지내봅시다 🤝


## 목차
- [Tech Stack](#Tech-Stack)
- [Git](#Git)
    - [Git Flow](#Git-Flow)
    - [Git Rebase & Merge]
    - [Git Hooks](#Git-Hooks)
- [코드리뷰](#코드리뷰)

## Tech Stack
> 서비스를 누르면, StackShare 링크로 이동해요.

렌트카 가격비교 1등앱, [**카모아**](https://stackshare.io/teamo2/carmore)


## Git
### Git Flow

저희는 보다 보기편한 git history 관리 및 무슨이유로 gitflow 를 사용하고 있습니다. 



#### Git Flow 란 ?

Backend 의 막내, Steve 가 작성한 Repository 그 어떤 아티클보다 명료하게 정리가 잘 돼 있어요.  
[이리오세요](https://github.com/stevejkang/git-guideline#2-git-flow--branch)

- [ ] Gitflow 의 안좋은예, 좋은예 
- [ ] Gitflow 링크 말고 설명으로 적어보기

### Git Rebase & Merge
Merge의 종류에는 크게 아래와 같이 3가지 방법이 있어요.
-- ff
With --no-ff, create a merge commit in all cases, even when the merge
           could instead be resolved as a fast-forward.

           With --ff-only, resolve the merge as a fast-forward when possible.
           When not possible, refuse to merge and exit with a non-zero status
```
When merging pull requests, you can allow any combination of merge commits, squashing, or rebasing. (중략)

If you have linear history requirement enabled on any protected branch, you must enable squashing or rebasing. 
```
모든 브랜치는 merge할 때 **rebase & fast-forward merge**를 사용하고 있어요.  

그 이유는, 우리가 작업하는 모든 feature들은 dev에 merge된 이후에는(= 서비스에 반영된 이후에는) _"어느 시점에 branch가 생성됐는 지"_, _"이 branch는 무슨역할을 하는지"_ 는 관심사가 아니에요.  
이런 점들을 신경쓸 필요가 없기 때문에 dev/master 브랜치는 가지(branch) 모양이 일직선으로 이루어져 있게끔 하고 있어요. ~~그리고 이쁨~~   
또, 주기적으로 작업 중인 브랜치를 후에 merge할 브랜치 _(주로 dev나 feature root 브랜치가 되겠죠)_ 에 rebase를 해주어야만 큰 프로젝트 단위에서 merge 시 conflict 해결에 드는 리소스도 최소화 할 수 있어요!

![rebase](https://user-images.githubusercontent.com/47936709/173546249-dbea4556-a6ac-4fd4-b1bd-45ea355d811d.png)

// 아직 정리 안된 글
Merge Commit은 원활한 rebase를 방해하고, 관리하는 데 어려움이 있어요. 또, merge할 때, merge하려고 하는 브랜치가 최신이 아닌 경우, remote branch를 기준으로 merge 하는 등, 이래서 안좋다.

그래서 만약, 프로젝트를 진행하다가 아래와 같은 commit이 생겼다면 무언가 잘못되었다는 뜻이에요.
```
(1) Merge pull request #2 from <user>/<branch>
(2) Merge branch '<branch>' of https://github.com/<user>/<repo> into <branch>
(3) Merge branch '<branch>' into <branch>
```

1번의 경우 Pull Request를 머지할 때 rebase merge가 아니라 merge 



즉, merge하는 브랜치(head branch)와 base branch의 local repository 상태는 remote repository와 일치해야 해요.

일치가 보장되면, base branch에서 아래 커맨드로 merge를 진행합니다.
```bash
$ git merge --ff-only <branch>
```

### Git Hooks

🙋‍♀️🙋‍♂️ : Git 에 규칙이 있다는건 알겠어..! 근데 습관이 안들여져서 자꾸 실수할까 두렵고 무서워요ㅠㅠ  
그런거에 신경쓰지마세요, 여러분이 잘 못 쓰면, 커밋이 안되도록, production/staging/develop 브랜치에 커밋 못 하도록 등등을 Git Hooks 에 세팅 해두었답니다.  
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
{$COMMIT_TYPE}: (${${ISSUE_NUMBER} | NONE}) ${TITLE}

${OPTIONAL_BODY}

${OPTIONAL_REFERENCE}
```

For Example,
```
FIX: (NONE) 카드 결제 오류 수정

아이폰에서 네이버페이로 결제 시도 시 네이버페이로 연결 안되는 현상 수정

ref : https://slack.com/adiekd/ds...
```

* COMMIT_TYPE: 어떤 커밋인가를 보여줘요
    * FEAT: 작업, 가장 기본적이고 가장 많이 쓰여요.
    * FIX: 버그 수정
    * HOTFIX: production 에서 긴급하게 된 버그 수정
    * DOCS: 문서수정

## 코드리뷰

모든 작업은 코드 리뷰를 통해서, 기능적, 가독성 등을 다 함께 검토 후 배포가 됩니다.  
작업물에 대한 책임을 작업자가 오롯이 떠안기 보다 공동체 차원에서, 그리고 리더급에게 위임하는 역할도 있고, 작업물을 모두가 알 수 있도록 하는 행동이예요.  
저희가 생각하는 코드 리뷰는 **"이해" > "납득" > "공감"** 의 순서를 거쳐야만 합니다.  
상급자가 리뷰를 남겼다고 해서 무조건 시행하는 것이 아닌, 서로의 의견이 일치해야 합니다.  
한 줄의 코드라 할지라도, 의견을 남겨주세요 !

**이해** : 어떤 리뷰를 남겼는지 이해가 된다.  
**납득** : 왜 이렇게 작성/변경 해야 하는지 납득이 된다.  
**공감** : 다른 상황에서 비슷한 케이스라면 남긴 리뷰처럼 코딩을 할 것 이다.  

## DDD

## TDD

## Micro Service Architecture

해당 문서가 작성되는 시점 (22. 06) 에 저희는 Micro 하지 않아요.  
그러나, 느리지만 꾸준하게 Monolithic 에서 하나 씩 떼어가고 있고, 무조건 MSA 를 해낼 것이예요  

**Monolithic 이 악이라는 소리를 하고 있는 것이 아닙니다.**  
팀오투, 카모아가 만들어지기 시작한 초창기에는 맞았던 아키텍쳐이지만, 개인의 역량이 성장하듯 사업의 성장세도 가파르기에, 사업의 변화/확장에 발맞춰 **우리도 변화할 뿐**입니다.  
그 작업이 고되고, 오래걸리더라도 더 관리하기 용이하게, 서비스 확장이 더 용이하게 하기 위함입니다.  


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



목적
- 리소스를 줄이고 싶다.
- Legacy가 순수악이 아니라는 것.


----

어떤 걸 하고 있어 -> 왜 하고 있어 -> 이건 이런거야. 필요하다면 예시
