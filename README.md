# TeamO2 Backend Developer Onboarding Helper

> 환영인사 및 소개

## 목차


## Tech Stack

## Git
### Git Flow

저희는 보다 보기편한 git history 관리 및 무슨이유로 gitflow 를 사용하고 있습니다. 

Merge Commit은 원활한 rebase를 방해하고, 관리하는 데 어려움이 있어요. 또, Merge Commit을 할 때, merge하려고 하는 브랜치가 최신이 아닌 경우, remote branch를 기준으로 merge 하는 등, 이래서 안좋다.

"그리고 항상 local repository를 remote repository와 맞춰 두어야 한다"라는 얘기 적기...

#### Git Flow 란 ?

Backend 의 막내, Steve 가 작성한 Repository 그 어떤 아티클보다 명료하게 정리가 잘 돼 있어요.  
[이리오세요](https://github.com/stevejkang/git-guideline#2-git-flow--branch)

- [ ] Gitflow 의 안좋은예, 좋은예 
- [ ] Gitflow 링크 말고 설명으로 적어보기

### Git Hooks

🙋‍♀️🙋‍♂️ : Git 에 규칙이 있다는건 알겠어..! 근데 습관이 안들여져서 자꾸 실수할까 두렵고 무서워요ㅠㅠ  
그런거에 신경쓰지마세요, 여러분이 잘 못 쓰면, 커밋이 안되도록, production/staging/develop 브랜치에 커밋 못 하도록 등등을 Git Hooks 에 세팅 해두었답니다.  
_예제는 아래에 쨔란~_

![커밋형태오류](https://user-images.githubusercontent.com/74130738/173327920-cd5f2d80-620a-4c24-8d19-529f8c688ba1.png)

- [ ] init_repo.sh 쓰는 방법 적어두기.


#### Commit Convention

그러면 우리가 추구하는 Commit Convention 에 대해서 알아봅시다 !
Commit 에서 저희가 제일 중요하게 생각하는 것들은 아래와 같아요.

- **어떤 작업을 했는가**
- **어떤 이슈인가 ?**
- **그래서 무엇을 했는가 ?**

그래서, Commit Convention 도 그 중요도를 반영하기 위한 형태로 유지하고 있어요!

```
{$COMMIT_TYPE}: ($ISSUE_NUMBER | NONE) ${TITLE}

${OPTIONAL_BODY}

${OPTIONAL_REFERENCE}
```

* COMMIT_TYPE: 어떤 커밋인가를 보여줘요
    * FEAT: 작업, 가장 기본적이고 가장 많이 쓰여요.
    * FIX: 버그 수정
    * HOTFIX: production 에서 긴급하게 된 버그 수정
    * DOCS: 문서수정



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
- 코드 지향 점
    - 주석 없는 코드
- 코드리뷰
- 정적분석



목적
- 리소스를 줄이고 싶다.
- Legacy가 순수악이 아니라는 것.


----

어떤 걸 하고 있어 -> 왜 하고 있어 -> 이건 이런거야. 필요하다면 예시
