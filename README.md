# 협업을 위한 Github 컨벤션 template

**코드만 재사용되는 것이 아닙니다-!**

종종 협업을 위해서 어떤 도구를 사용할지에 대한 커뮤니케이션 비용이 발생하곤 합니다. Jira, Github issue & Projects, ... 다양한 도구들 중에서 해당 Repository는 git message, github issue, github PR을 통한 컨벤션을 탬플릿화 하려고 합니다. 추가로, PR과 브랜치를 관리하는 방법에 대해서도 적용하는 저의 방법을 소개하고자 합니다.

## 👉 진행하고자 하는 것

<aside>

1. 브랜치와 커밋이름에 이슈번호 적기
2. .gitmessage를 통해 commit message convention 만들기
3. PR과 커밋은 최대한 작은 단위로 쪼개자
4. feature 브랜치와 sub feature 브랜치로 만들어 merge하는 전략을 사용하자
5. Github 탬플릿으로 PR 내용과 ISSUE 내용 규격화
6. 라벨 활용하기
7. 코드리뷰 내용 반영할 때마다 커밋 id남기기

</aside>

## 브랜치와 커밋이름에 이슈번호 적기

Github Issue에 새 글을 등록하면 이슈번호가 생기는데요. 이 이슈번호를 이용하여 브랜치와 커밋 메시지를 표준화하고자 합니다. 이 방법을 사용했을 때의 이점은 다음과 같습니다.

1. 해당 브랜치와 커밋이 어떤 이슈를 다루고 있는지 쉽게 파악이 가능하다.
2. 브랜치명과 커밋 이름에 규칙이 생긴다.
3. Issue를 통해 문서화가 자동으로 적립된다.
4. 이후 문제가 발생했을 때, 어떤 이슈에서 발생한 것인지 파악을 빠르게 할 수 있다.

이러한 이점을 이용하기 위해 Github Issue와 이슈번호를 이용하고자 합니다.

아래의 그림에서 issue number teset #1 으로 써져있는 부분을 확인할 수 있습니다. 여기서 #1에 해당하는 부분이 이슈번호인데요. 이를 사용하는 방법은 다음과 같습니다. 브랜치를 활용하는 방법과 커밋 메시지에 대해서는 차차 이야기하도록 하겠습니다. 우선은 이슈번호를 브랜치와 커밋 메시지에 사용한다만 기억해두기 바랍니다.

```
Branch : feature/1/market
Commit : [#1] feat : market 탭 검색 기능 구현
```

![이슈 번호](https://github.com/haejunejung/Github_template/assets/99087502/f083e996-9401-41c8-bd8e-96dbfaa873fd)

## .gitmessage를 통해 commit message convention 만들기

.gitmessage를 이용하면 커밋 메시지를 모든 팀원이 동일한 방식으로 작성할 수 있습니다. 이렇게 했을 때, 커밋 내용만 보고도 이 커밋이 어떤 것을 하려고 했다는 것을 이해할 수 있습니다. 아래는 탬플릿에서 사용하는 .gitmessage 예시입니다.

```
################
# GIT MESSAGE TEMPLATE
# [커밋 타입 종류]
# feat : 새로운 기능 추가
# fix : 버그 수정
# docs : 문서 수정
# test : 테스트 코드 추가
# refact : 코드 리팩토링
# style : 코드 의미에 영향을 주지 않는 변경사항
# chore : 빌드 부분 혹은 패키지 매니저 수정사항
################

# '#' 라인은 주석입니다.
# [#Issue Number] <타입> : <제목> 의 형식으로 제목을 아래 공백줄에 작성
# 제목은 50자 이내 / 변경사항이 "무엇"인지 명확히 작성 / 끝에 마침표 금지
# 예) feat : 로그인 기능 추가
# [#Issue Number]를 커밋메세지 앞에 추가하면 이슈별로 커밋을 관리할 수 있음
# --이 라인 밑에 "[#Issue Number] <타입> : <제목>" 작성해주세요--

# 바로 아래 공백은 지우지 마세요 (제목과 본문의 분리를 위함)

################
# 본문(구체적인 내용)을 아랫줄에 작성
# 여러 줄의 메시지를 작성할 땐 "-"로 구분 (한 줄은 72자 이내)
# --이 라인 밑에 "본문" 작성해주세요--

################
# 꼬릿말(footer)을 아랫줄에 작성 (현재 커밋과 관련된 이슈 번호 추가 등)
# 예) Close #7
# --이 라인 밑에 "꼬릿말" 작성해주세요--

################
```

## PR과 커밋은 최대한 작은 단위로 쪼개자

PR과 커밋은 최소 작업단위를 기준으로 나누는 것이 이후 코드 리뷰에도 용이하기 때문에, 최대한 작은 단위로 쪼갭시다!

- 1개의 커밋에는 1개의 행위만 들어있는게 좋다.
- 1개의 PR에는 1개의 작업만 들어있는게 좋다.

```
👉 안좋은 예시

디자인에 맞게 레이아웃을 추가해서 작업했는데 버튼 클릭 처리에 대한 코드를 작성하던중 기존에 사용하던 값을 상수로 빼서 재사용하도록 개선했다. 현재 작성되어 있는 파일의 코드가 정렬이 잘 되어 있지 않아서 IDE에서 제공하는 기능을 통해 코드 리포맷팅 작업도 진행했다.

⛔️ 이 작업에 대한 적절한 커밋이름을 짓기 어렵습니다

⛔️ 커밋 내용중 잘못된 내용이 있어서 특정 작업만 revert해야 하는경우 함께 포함된 작업도 다같이 revert 되어 버립니다

⛔️ 리뷰어가 커밋이름만 보고 어떤 작업을 했는지 명확하게 알기 어렵습니다

⛔️ IDE의 자동리포맷 기능으로 인해 단순하지만 코드가 엄청 많이 변경된것처럼 보여서 리뷰어가 불필요한 변경작업을 모두 봐야 합니다
```

```
👉 좋은 예시

- 디자인에 맞게 레이아웃을 추가해서 작업
- 기존에 사용하던 값을 상수로 빼서 재사용하도록 개선
- IDE에서 제공하는 기능을 통해 코드 리포맷팅 작업

✅ 1개의 작업에 1개의 명확한 커밋이름을 작성할 수 있습니다

✅ 특정작업만 revert해야할때 다른 작업에 영향을 미치지 않고 온전하게 revert 할 수 있습니다

✅ 리뷰어가 커밋이름만 보고도 어떤 작업을 했는지 파악할 수 있습니다

✅ IDE로 자동으로 변경된 내용들은 리뷰어가 확인할 필요가 없습니다
```

비슷한 이유로 **PR도 최대한 작은 단위로 쪼개서 만드는게 좋습니다!**

새로운 화면이나 피쳐를 만들어서 개발할 때 이슈를 여러 개로 쪼개고 여러 개의 PR로 작업합시다!

## feature 브랜치와 sub feature 브랜치로 만들어 merge하는 전략을 사용하자

```
👉 예시

feature 브랜치: feature/1/market-ui
sub feature 브랜치 : feature/1/market-home-ui

sub feature 브랜치를 완성 후 PR
-> feature 브랜치에 merge
-> 다시 sub feature 브랜치를 파서 작업
```

**이렇게 PR을 작은단위로 쪼개면 아래와 같은 장점이 있습니다**

✅ 이슈가 여러개이므로 하나의 피쳐개발을 1명이 아닌 **여러명이 작업**할 수 있습니다

✅ 이슈마다 작성해야 하는 코드양이 적기 때문에 **빠르게 작업**하고 PR을 올릴 수 있습니다

✅ 코드 리뷰어가 리뷰해야 하는 코드가 적기 때문에 **빠르고 정확하게 리뷰**를 할 수 있습니다

✅ 리뷰사항을 반영해야 하는 사항도 적어지므로 리뷰 반영사항으로 인한 **코드 변경도 적어**집니다

✅ 코드 리뷰가 끝날때까지 기다리지 않고 **다른 작업을 수행**할 수 있습니다

![작은 단위의 브랜치](https://github.com/haejunejung/Github_template/assets/99087502/a81ff16c-9a9a-4853-9bb4-129cbb397fe0)

## Github 탬플릿으로 PR 내용과 ISSUE 내용 규격화

ISSUE와 PR을 생성할 때, 어떤 내용을 적어야하는지 모르는 사람과 어떤 내용은 꼭 들어갔으면 하는데...라는 생각을 가져본 적이 있습니다. 이 문제는 ISSUE와 PR 내용을 규격화함으로써 어느정도 해결이 가능합니다.

```
👉 예제 PR 탬플릿

# ISSUE <#00> {이슈 이름}

# MOTIVATIONS 🧐

왜 이것을 진행했나요?

# KEY CHANGES 🙋‍♀️

무엇을 바꿨나요?

# TO REVIEWERS 🗣️

어떤 부분을 확인하면 되나요? 가능한 자세하게 적어주세요.

# TEST 📑

어떤 부분을 테스트하면 되나요? 예시 사진 혹은 예제 코드를 첨부하면 더 좋아요.
```

## 라벨 활용하기

**PR의 상태를 확인하려면 해당 PR에 직접 들어가야 확인이 가능하다 → 라벨을 활용하자!**

라벨을 사용하면 아래와 같은 효과가 있습니다.

- 현재 PR목록들의 전체 상태를 파악 가능
- 내가 코드 리뷰해야하는 PR들이 어떤 것들이 있는지 파악 가능
- 내가 리뷰사항 반영해야 하는 PR들이 어떤어떤 것들이 있는지 파악 가능

![라벨](https://github.com/haejunejung/template/assets/99087502/27e1a56f-c81e-4e6a-ae5f-7b1aa8c5818c)

## 코드리뷰 내용 반영할 때마다 커밋 id남기기

코드리뷰의 내용을 반영하면, 반영이 되었는지 확인이 어렵다
→ 해당 comment에 답글로 해결한 커밋 id남겨놓자
→ 해결된 comment 확인이 가능하며, 리뷰어도 확인하기 용이합니다!

![커밋 id](https://github.com/haejunejung/Github_template/assets/99087502/7340a24a-b314-4209-b30f-4e6999b5ea31)
