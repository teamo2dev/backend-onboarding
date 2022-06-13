# class TeamO2BackendDeveloperOnboardingHelper

**Welcome to the TeamO2 Backend World !**  

> "레거시 코드는 어제 짠 코드다"  

하루 하루 성장해 나갈 수 있는, 성장해 나가고 있는 팀오투의 백엔드를 맡고 있는 곳에 오신 것을 환영합니다. 신입이라면 멱살 잡고 성장을, 경력자라면 본인의 장기를 마음껏 뿜뿜할 수 있는 곳을 지향하고 있습니다.  

> 🤝 잘 지내봅시다 🤝


## 목차
- [class TeamO2BackendDeveloperOnboardingHelper](#class-teamo2backenddeveloperonboardinghelper)
  - [목차](#목차)
  - [1. Tech Stack](#1-tech-stack)
  - [2. Git](#2-git)
    - [Git Flow](#git-flow)
    - [Git Commit & Branch](#git-commit--branch)
    - [Git Rebase & Merge](#git-rebase--merge)
    - [Git Hooks](#git-hooks)
      - [세팅하는 법](#세팅하는-법)
    - [Commit Convention](#commit-convention)
  - [3. Our Coding GOAL](#3-our-coding-goal)
    - [주석 없는 코드](#주석-없는-코드)
    - [정석을 따르지 않을 용기](#정석을-따르지-않을-용기)
    - [Micro Service Architecture](#micro-service-architecture)
  - [4. Code Review](#4-code-review)
  - [5. DDD](#5-ddd)
  - [6. TDD](#6-tdd)

## 1. Tech Stack

첫 번째로, 간략하게 TeamO2에서 개발 중인 서비스들을 나열하면서, 어떤 Stack 들을 가지고 있는지 알려드리도록 하죠 💁

> 서비스를 누르면, StackShare 링크로 이동해요.

- 렌트카 가격비교 1등 앱, [**카모아**](https://stackshare.io/teamo2/carmore)
- 팀오투 서비스의 숨은 1등 공신, [**카모아 파트너스**]
- 구성원들의 업무 집중도를 최대로, [**운영툴**]
- 분산화의 시발점이 된, [**카모아 내부API**]
- OTA의 Role, [**카모아 외부API**](https://stackshare.io/teamo2/carmore-external-api)

## 2. Git
### Git Flow

Git Flow는 버전 관리 시스템(Version Control System, VCS)의 한 종류인 git을 통해 효율적으로 프로젝트를 관리하고 배포하기 위한 전략이자 브랜칭 관리 전략(Branch Management Strategy)이에요. 저희는 코드의 지속적인 관리와 히스토리 확인, 그리고 협업을 위해 Git을 사용하고 있고, 그 전략으로 GitFlow를 사용하고 있습니다.

![](https://i.imgur.com/aGMUnV9.png)
~~이쁜 커밋라인 & 메시지들~~

### Git Commit & Branch
GitFlow에 해당하는 브랜치들과, 나누는 기준에 대해서는 [여기](https://github.com/stevejkang/git-guideline#2-git-flow--branch)에서 설명해요. 이 다음에 나올 내용들을 이해하기 위해서 반드시 확인해주세요.

브랜치는 기본적으로 1-branch 1-commit을 지켜주세요. 예를 들어, 브랜치에 작업이 완료되고, 해당 브랜치 PR을 올린 후 PR 피드백이 생겨, 이를 반영하고자 할때는 git commit의 amend option을 이용하면 커밋을 하나로 합칠 수 있어요.

또, 커밋은 우리가 생각하는 "어떠한 모듈을 만들었다" 혹은 "A UseCase를 위한 Dto 추가"와 같이 개발의 단위보다는 기능 단위의 커밋을 지향하고 있어요.

이렇게 하는 가장 큰 이유는, 해당 브랜치가 dev(develop)이나 master/main으로 머지되었을 때에는 이 기능을 위해서 작업했던 일련의 작은 과정들은 우리의 관심사가 아닐 뿐더러, 깃 히스토리 파악에도 방해가 돼요.

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
<br>

🙋‍♀️🙋‍♂️ : 왜요 ?  
💁 : 우리가 작업하는 모든 feature들은 dev에 merge된 이후에는(= 서비스에 반영된 이후에는) _"어느 시점에 branch가 생성됐는 지"_, _"이 branch는 무슨역할을 하는지"_ 는 관심사가 아니에요.

이런 점들을 신경쓸 필요가 없기 때문에 dev/master 브랜치는 가지(branch) 모양이 일직선으로 이루어져 있게끔 하고 있어요. ~~그리고 이쁨~~

또, 주기적으로 작업 중인 branch를 후에 merge할 branch(target branch) _(주로 dev나 feature root 브랜치)_ 에 rebase를 해주어야만 큰 프로젝트 단위에서 merge 시 conflict 해결에 드는 리소스도 최소화 할 수 있어요!

![rebase](https://user-images.githubusercontent.com/47936709/173546249-dbea4556-a6ac-4fd4-b1bd-45ea355d811d.png)


> **왜 Merge Commit을 남기지 않나요?**
> 
> Merge Commit은 원활한 interactive rebase를 방해하고, 관리하는 데 어려움이 있어요. 위에서 말했듯 merge commit으로 브랜치가 병합된 시점은 우리의 관심사가 아니고, merge할 때 부주의로 local repository가 최신이 아니라면 임의로 remote repository의 branch와 merge되는 경우도 있어요.
> 
> 그래서 만약, 프로젝트를 진행하다가 아래와 같은 commit이 생겼다면 무언가 잘못되었다는 뜻이에요.
> ```
> (1) Merge pull request #2 from ${user}/${branch}
> (2) Merge branch '${branch}' of https://github.com/${user}/${repo} into ${branch}
> (3) Merge branch '${branch}' into ${branch}
> ```
> 이때는 merge를 되돌리고 rebase merge를 진행해주세요.

rebase를 잘 하려면, merge하는 브랜치(head branch)와 base branch의 local repository 상태는 remote repository와 일치해야 해요.

만약 일치하지 않고, `git pull origin <branch>` 명령어가 conflict를 발생시킨다면, 주저하지 말고 `git reset --hard origin/${branch}`로 head branch를 최신화 시켜주세요.

일치가 보장되면, base branch에서 아래 커맨드로 merge를 진행해요.
```bash
$ git merge --ff-only <branch>
```

그래서 보통 아래와 같은 순서로 작업이 이루어져요.

```bash
$ git checkout backend/dev # develop 브랜치에서 시작
$ git checkout -b backend/feature/naver-pay # feature root branch 생성
$ git commit # feature root branch 변경사항 커밋
$ git push origin backend/feature/naver-pay # feature root branch 변경사항 푸시
$ git checkout -b backend/feature/naver-pay-DEV-12121 # feature branch 생성
$ git commit # feature 변경사항 커밋
$ git push origin backend/feature/naver-pay-DEV-12121 # feature 변경사항 푸시
# 다른 누군가의 PR이 feature/naver-pay feature root branch에 병합됨.
$ git checkout backend/feature/naver-pay
$ git fetch origin
$ git pull
# 병합된 내용이 기존 backend/feature/naver-pay의 커밋에 force-push 되었고, 이 때문에 마지막 commit의 변경사항이 내 local과 remote가 같지 않아 git pull에서 conflict 발생
$ git reset --hard origin/backend/feature/naver-pay
$ git checkout backend/feature/naver-pay-DEV-12121
$ git rebase backend/feature/naver-pay
$ git push origin backend/feature/naver-pay-DEV-12121 -f
```

### Git Hooks

🙋‍♀️🙋‍♂️ : Git 에 규칙이 있다는건 알겠슴다..! 근데 습관이 안들여져서 자꾸 실수할까 두렵고 무서워요ㅠㅠ  
💁 : Don't care ! 여러분이 잘 못 쓰면, 커밋이 안되도록, production/staging/develop 브랜치에 커밋 못 하도록 등등을 Git Hooks 에 세팅 해두었답니다.  
_예제는 아래에 쨔란~_

![커밋형태오류](https://user-images.githubusercontent.com/74130738/173327920-cd5f2d80-620a-4c24-8d19-529f8c688ba1.png)

#### 세팅하는 법

저장소를 pull 받으면 root directory 에 `init_repo.sh` 를 볼 수 있습니다.  
해당 shell 을 실행해주면 _The end_

### Commit Convention

그러면 우리가 추구하는 Commit Convention 에 대해서 알아봅시다!
Commit 에서 저희가 제일 중요하게 생각하는 것들은 아래와 같아요.

- **어떤 작업을 했는가**
- **어떤 이슈인가**
- **그래서 무엇을 했는가**

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
Clean Code에서 설명하는 좋은 주석과 나쁜 주석을 구분할 수 있다고 가정할게요. 그리고 당연히 나쁜 주석은 사용하지 않아야 하고요.

하지만, **주석으로 설명이 필요한 코드 = 설명이 필요할 만큼 가독성이 갖춰지지 않은 코드**라고 생각해요. 그런 의미에서 내가 주석을 적었다면, 조금 더 읽기 쉽게 개선할 수 있는 방법은 없는 지 PR 올리기 전에 고민해보면 좋을 것 같아요.

하지만 간혹, 우리가 논의했던 내용이나 정책적인 이유로 이를 코드안에 남겨두어야 빠르게 파악 가능한 경우도 있어요. 예를 들면 아래와 같은 경우에요.

```typescript
{
    ...parms
    // NOTE: 규격에 관한 논의 쓰레드 https://teamo2.slack.com/archives/CSK9AG58Q/p165...
    대여종료일: dayjs(reservation.fullRentEndDatetime).format('YYYY년 MM월 DD일 HH시 mm분'), 
    // NOTE: 논의 쓰레드, https://teamo2.slack.com/archives/CSK9AG58Q/p16...
    이용개월: termCount, 
    회차주소: reservation.returnAddress,
    차종: reservation.model,
}
```

이런 경우에는 
1. 해당 부분에 `// NOTE: FooBar 때문에 수정` 와 같이 Note Comment를 남기거나
2. Commit Message의 Body에 상세하게 적을 수 있어요.

> 가끔은 이 코드가 왜 생겨났는 지 히스토리가 궁금한 경우가 많아요.
> 히스토리 파악과 관련된 내용은 Commit Message에 포함시켜주면, 나중에 Git Blame과 같은 Tool을 이용하여 특정 파일 내 변경 히스토리를 볼 때 편하게 확인할 수 있어요.

### 정석을 따르지 않을 용기

Clean Code, Clean Architecture 등등, 유명한 책들은 많은 개발자들이 참고하고, 실무를 하는 데 있어 좋은 참고서에요. 하지만, 아무리 좋은 방법이더라도, 실제 우리가 처한 현실과 맞지 않다면 정석적인 방법을 따르지 않을 용기가 필요해요. 우리가 지향하는 방향은 가장 정석적인 방법이면서, 가장 유연한 방법이에요.

**그때, 그 상황에 가장 맞는 선택이 정석적인 방법을 따르지 않는다고 두려워하지 마세요.**

### Micro Service Architecture

이 문서가 작성되는 시점 (22. 06) 에 저희는 Micro 하지 않아요. 그러나, 느리지만 꾸준히 Monolithic에서 하나 씩 떼어가고 있고, 무조건 MSA를 해낼 것이예요.

**하지만, Monolithic이 반드시 악이라는 것이 아니에요.**

팀오투, 카모아가 만들어지기 시작한 초창기에는 맞았던 아키텍쳐이지만, 개인의 역량이 성장하듯 사업의 성장세도 가파르기에, 사업의 변화/확장에 발맞춰 **우리도 변화할 뿐**입니다. 그 작업이 고되고, 오래걸리더라도 더 관리하기 용이하게, 서비스 확장이 더 용이하게 하기 위함입니다. 

저희는 새로운 프로젝트들부터 기존의 인프라 에서 벗어나, 프로젝트에 맞는 새로운 DB, 서버 등을 세팅해가면서 micro해지기 위해 노력중입니다.  
아직 만능 서버/만능 클래스를 없애지 못했지만, 우리가 할 수 있는 노력들을 하고 있으니 함께 해보시죠 !

## 4. Code Review
모든 코드는 적절하고 효율적으로 구현됐는지, 잘 읽히는지 등을 모두가 코드리뷰를 통해 검토한 뒤에 배포가 이루어져요.

코드리뷰를 하는 목적은 작업물에 대한 책임을 작업자가 오롯이 떠안지 않고 리더급에게 위임하는 것도 있지만, 기능을 구성원 모두가 알 수 있게 되고, 궁극적으로는 모두의 성장을 이끌어 낼 수 있어요.

리뷰어가 리뷰를 남겼다고 해서 무조건 수용하는 것이 아닌 비판적 수용을 해야하고, 모든 관련 구성원의 의견이 일치해야 해요. 그래서, 저희가 생각하는 코드리뷰는 **"이해" > "납득" > "공감"** 의 순서를 거쳐야만 해요.

**이해**: 어떤 리뷰를 남겼는지 이해가 된다.  
**납득**: 왜 이렇게 작성/변경 해야 하는지 납득이 된다.  
**공감**: 다른 상황에서 비슷한 케이스라면 남긴 리뷰처럼 코딩을 할 것 이다.  

> 한 줄의 코드라 할지라도, 의견을 남겨주세요 !  
> 그리고 본인의 생각을 말하고 피력해주세요 !


## 5. DDD

저희의 개발 방식은 도메인이 주가 되는 Domain Driven Development 를 지향하고 있습니다.  
DDD 란, 간단하게 말하면 서비스, 즉 코드 내 모든 것들은 Domain 화 되어서 커플링을 최소화하고, 독립된 테스트가 가능해지게 하는 방법론입니다.  

제가 느끼는 DDD 에 정답은 없습니다.  
어느 곳은 이렇게, 어떤 곳은 저렇게...  
그래서 저희가 맞다 생각하는 것을, 정답이라 믿고 굳건하게 진행해나가고 있어요.  

이는 MSA 를 하기 위한 초석이 되는 작업이기도 하여 굉장히 중요하게 여기고 있습니다.  
관련 지식들은 아래 책을 통해 Deep하게 배울 수 있습니다.  

- [도서: 도메인 주도 설계란 무엇인가 ?](https://www.aladin.co.kr/shop/wproduct.aspx?ItemId=12620317)
- [아티클: DDD 핵심만 빠르게 이해하기](https://happycloud-lee.tistory.com/94)

## 6. TDD 

**Test-Driven Development**  
단어에서 보여지는 것과 같이 **테스트 주도 개발**이예요.  
저희는 TestCase를 먼저 구현하고 나서, 그 테스트를 통과하기 위한 개발을 진행하고 있습니다.  

🙋‍♀️🙋‍♂️ : TDD 는 왜 하나요 ?  
💁 : 우리의 코드는 항상 불안정해요, 항상 버그를 지니고 있는 잠재적 버그유발코드이죠. 그러기 위해서는 테스트코드가 필요로 됩니다.
그러나 테스트코드를 코드 작성 이후에 만들게 되면, 테스트코드의 범위가 너무 좁아지고, 생각의 폭이 좁아집니다. 그리고, 이미 작성된 코드안에서만 테스트코드가 만들어져요. 그렇게 되면 의미가 없습니다.
테스트코드를 먼저 만들게 되면, 만드려면, 해야할 작업에 대한 이해가 필수적으로 선행되게 됩니다. 
이해된 내용을 작업하는 것은, 이해되지 않은 내용을 작업하는 것보다 수월하고 더 많은 경우를 고려할 수 있다는 것은 두말하면 잔소리겠죠.  
그리고 먼저 만들어진 테스트코드를 통과시키기 위한 코딩을 하게 되면, Code Coverage 는 자연스레 100%가 되게 됩니다. 통과하는 코드만 작성하니까 !

🙋‍♀️🙋‍♂️ : WoW !! 그러면 TDD를 통해 작성된 코드는 완벽하겠네요 !?  
💁 : 아니요, TDD 는 만능이 아니예요, 위에 내용을 가만히 살펴보면, 결국 사람/개발자의 머리에서 나온 거기 때문에 완벽하지 않아요. 다만, 이런 개발을 많이 하다보면 자연스레 Defensive-Thinking이 가능해지기 때문에 개발자의 생각의 폭을 넓힐 수 있고, 발생될 오류를 사전에 검증이 가능해집니다 !

TDD를 조금더 원활하게 하기 위해서는 여러 방법론 및 구현법들이 있어요.  
아래에 참고할 수 있을 만한 아티클을 공유드릴게요!  

- [Given When Then](https://brunch.co.kr/@springboot/292)
- [Red Green Blue](https://www.oreilly.com/library/view/modern-c-programming/9781941222423/f_0054.html)
- [어떤 것들을 테스트 해야 하나요?](https://jojoldu.tistory.com/674)
- [테스트 내 코드들 작성은 어떻게 하나요?](https://jojoldu.tistory.com/615)
