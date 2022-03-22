---
title: "Github Blog"
tags:
  - git
  - github blog
  - Notion
categories:
  - git
  - github blog
author: "minkuen"
date: '2022-03-22'
---

### 깃허브 블로그

-IT 프로그래밍 관련

—> 소스 코드 / 결과 / 이미지

신입은 포폴 x

경력 이직 —> 직장에서 했던 프로젝트

—> 신기술을 써봤냐? 안 써봤냐?  —> 깃허브로 증명 가능


### 깃 설치 이후에 다음 내용 진행.

구글링 : nodejs → LTS 버전 다운로드 → 경로 중 add path?에 놓는다. 

→ ‘atuomatically install....’ 을 체크 → install

→ 바탕화면 —> 우클릭 → git bash here → node -v 입력 후 enter → v16.14.1 출력되면 성공

*컴퓨터 내에서 검색 : 자격 증명 → 자격 증명 관리자 → window 자격 증명’ 확인하기

*다음 링크 참조

[https://dschloe.github.io/settings/hexo_blog/](https://dschloe.github.io/settings/hexo_blog/)

바탕화면 우클릭 → git bash here

→ 다음을 복사 `npm install -g hexo-cli`

→ git bash here 에 Shift + insert 하여 붙여넣고 enter

→ (위 링크에 있는 몇몇 과정은 설명을 생략했다고 하심)

→ (~desktop 위치에서) `hexo init` myblog              *### 다시 할 때는 여기부터*

→ 바탕화면에 myblog 폴더가 생성되면 성공

→ myblog에 우클릭 후 ‘Open Folder as PyCharm Community...’ 클릭    

→ 파이참 하단에 Terminal 클릭 → 옆에 화살표 눌러서 gitbash 켜기

→ `hexo server` 입력

→ 링크 클릭

→ 블로그 입장 성공

깃허브 

→ 로그인

→ 우측상단 프로필 옆 클릭 → your repository → new

→ repository name에 myblog 입력 ( hexo init 명령에서 만든 폴더와 같아야 함 )  

→ create repository

→ 파이참으로 이동

→`echo "# myblog" >> [README.md](http://README.md)`  

→`git init`

→`git add README.md`

→`git commit -m "first commit"`

→ unable to auto-detect... 에러 발생 시 다음 입력

→ git config --global [user.email](http://user.email) “alsrbs0219@gmail.com”

→ git config --global [user.name](http://user.name) “kmk3593”

→  다시 `git commit -m "first commit"`

 → `git branch -M main`

→ `git remote add origin https://github.com/kmk3593/myblog.git`

→ `git push -u origin main`                  ##깃허브에서 복붙으로 편하게 진행 가능

git add 파일명#  ⇒  해당 파일명을 내가 올리겠다.

git add .#  ⇒ 모든 파일 올리겠다(띄어쓰기 주의) 

git commint -m “updated”

git push  # 최종 단계: 모든 파일을 깃허브(사이트)에 올려라

세팅 끝나면 다음 세 가지만 쓰면 된다.

`git add README.md`    # 단, README 는 그때 그때 다르게 쓴다.

`git commit -m "first commit"`  #단, first commit 은 그때 그때 다르게 쓴다.

`git push -u origin main`

ex) `git add .`

`git commit -m "first commit"`

`git push`

`hexo server`

→ 링크타고 이동

→ 파이참 왼쪽 목록에서 mblog →  source → post → hello world 열기

→  내용 써보기 #첫번째글 안녕하세요 

→ 깃허브에서 source/_post를 클릭 → hello world .md 클릭   // 안녕하세요가 반영 안 되어있다. 반영해보자.

→`git add .`    (파이참에서 실행)

`git commit -m "update"`

`git push`

→ 이제 깃허브를 다시 확인  →  ‘안녕하세요’가 적혀있다면 성공

→ 다음을 입력하여 설치 (단, mblog 위치에서 해야 함 = cd mblog ) 

```
$ npm install
$ npm install hexo-server --save
$ npm install hexo-deployer-git --save
```

→ 파이참 왼쪽 목록에서 mblog →  config.yml 열기

→ #URL 부분에 `[https://kmk3593.github.io](https://kmk3593.github.io)` 입력

→ config 맨 하단에 #Deployment 에서 다음과 같이 입력

```
deploy:
  type: git
  repo: https://github.com/kmk3593/kmk3593.github.io.git
  branch: main
```

→ [kmk3593.github.io](http://kmk3593.github.io) 복사해서 → 깃허브 your repository → new에서 repository name에 붙여넣기

→ 생성

→ 파이참에서 `hexo generate`

→ `hexo deploy`

→ INFO Deploy INFO : git 이 출력되면 배포 성공.              # 오류나면 npm install 3개를 다시 진행

→ 깃허브 새로고침

→ 깃허브에서 active 상태될 때까지 기다린다.

→ ****[kmk3593.github.io](https://github.com/kmk3593/kmk3593.github.io)를 복사해서 주소창에 입력**

→ 배포가 완료됬음을 확인 할 수 있다.

파이참 

→ `hexo new “MY New Post”`     # 새 파일 만들기 

→ `hexo server`                          # 반영됬는지 링크타고 확인하자.

→ `hexo generate --deploy`    # 배포 한 줄로 하기

→ 왠지 모르게 반영이 안된다. 일단 넘어가자.

### 테마 (이카루스)

[https://ppoffice.github.io/hexo-theme-icarus/uncategorized/getting-started-with-icarus/#install-npm](https://ppoffice.github.io/hexo-theme-icarus/uncategorized/getting-started-with-icarus/#install-npm)

링크 들어가서

→ 다음을 파이참에 붙여넣어 설치

→ `npm install -S hexo-theme-icarus`  

→ `hexo config theme icarus`

→ config.yml이 변경되었음을 알 수 있다.

→ `hexo server`

→ 만약 에러 나오면) `npm install --save bulma-stylus@0.8.0 hexo-renderer-inferno@^0.1.3`

→ 만약 에러 나왔다면) 다시 `hexo server`

→ 나오는 링크타고 이동 → 제대로 페이지가 출력되면 성공

→ hexo clean ( 청소하기 )

→ `hexo generate --deploy`   #배포 재시도

→ 링크 들어가서 확인

재확인하기

파일 내용 막 써보고

→ `hexo server` → 링크 들어가서 확인

→ `hexo generate --deploy` 

→ ****[kmk3593.github.io](https://github.com/kmk3593/kmk3593.github.io)  들어가서 확인**

### 주의사항

1. 데이터셋 or 파일크기 —> 50MB 이상은 깃허브에 올리면 안 됨
    
—> 못 올리나요?  추가적인 설정이 필요.
    
2. 깃허브 상에 파일 편집 금지!!  →> 아예 마우스로 건드리지 마시오

### 반영이 잘 안된다면

구글링 : github status 확인

### R MarkDown 올리기

참고 : [Hexo Blog 이미지 추가 - Data Science | DSChloe](https://dschloe.github.io/settings/hexo_img/) 

temp프로젝트

→ R MakrDown → 저장 → knit 실행 → 저장한이름.html 생성됨

→ 다음과 같이 작성

![Untitled](/images/git_myblog/Untitled.png)

→ knit 실행 → 저장한 [이름.md](http://이름.md) 생성됨

→ 다음과 같이 md 파일을 복사하여 다음 경로에 붙여넣기

![Untitled](/images/git_myblog/Untitled%201.png)

→ 파이참에 md 파일이 생성된다.

→ `hexo server`  하여 링크로 들어가 반영여부를 확인

→ 다음 경로에  images파일을 만들고 다음과 같이 blog_files를 복사하여 그 안에 넣는다.

![Untitled](/images/git_myblog/Untitled%202.png)

→ 파이참의 md파일에 /images/를 덧붙여서 다음과 같이 작성한다.   *( ctrl+ R 로 하면 편리 )

![Untitled](/images/git_myblog/Untitled%203.png)

→ `hexo server` 하여 링크로 확인. 

→ 이미지가 추가되었다면 성공.

*’블로그 이름’폴더 → source → images 폴더 생성 → images안에 ‘블로그 이름’_files를 넣는게 핵심

[깃허브 블로그 실습]

이전에 과제로 작성한 R MarkDown파일인 stat_01을 깃허브에 올려보자.

→ 이미지가 없어서 그러지 images에 넣을 _files 폴더가 생성되지 않았다.

→ 배포까지 완료했다. 

→ 성공

### 노션 올리기

노션 

→ 올릴 페이지 선정

→ 다음 그림과 같이 우측 상단의  ººº 을 선택

![Untitled](/images/git_myblog/Untitled%204.png)

→ 내보내기 → Markdown & CSV 선택 → 내보내기

→ 압축파일이 다운로드됨 → 압축해제 → 폴더 이름 재정의

→ Markdown 올리기와 똑같이 파일을 source와 images에 복사 붙여넣기한다.

→ 파이참에 md파일이 생겼을 것이다.

→ 맨 위에 세팅 부분이 없을 건데, 다음과 같은 형식으로 작성해준다.

![Untitled](/images/git_myblog/Untitled%205.png)

→ 이미지링크를  수정해야한다 → 링크 복사 → images에 있는 해당 폴더를 우클릭

→ copy path/reference → Path From Repository Root 

→ 다음과 같이 앞부분을 /images/파일명/ 으로 변경해야 한다.

![Untitled](/images/git_myblog/Untitled%206.png)

→ `hexo server` 하여 반영되었는지 확인

→ `hexo generate --deploy` 하여 배포

### 파이썬 올리기

크롬 브라우저

→ 구글 검색 : google colab

→ 파일 → 다운로드 → ipynb 다운로드

→ 다운로드한 파일을 바탕화면으로 옮기고 colab_intro로 이름 변경

→ anaconda navigator 관리자 권한으로 켜기 

→ JupyterLab 

→ 이전에 다운받은 colab_intro 클릭

→ file → Save and Export Notebook As → Markdown

→ 파일이 다운된다. → 바탕화면으로 옮기고 압축 해제

→ markdown 때와 같이 폴더를 복사 붙여넣기

→ 파이참에서 md 파일 확인

→ 맨 위에 세팅 부분이 없을 건데, 다음과 같은 형식으로 작성해준다.

![Untitled](/images/git_myblog/Untitled%207.png)

→ 이미지링크를  수정해야한다 → 링크 복사 → images에 있는 해당 폴더를 우클릭

→ copy path/reference → Path From Repository Root 

→ 다음과 같이 앞부분을 /images/경로/파일명/ 으로 변경해야 한다.

![Untitled](/images/git_myblog/Untitled%208.png)

→ `hexo server` 하여 반영되었는지 확인

→ `hexo generate --deploy` 하여 배포

### 태그 카테고리

[hexo 블로그를 꾸며보자!! 카테고리 작업을 해보자!! — SteemCoinPan](https://www.steemcoinpan.com/hive-101145/@goodhello/4ntcr1-hexo)

-다음과 같이 tags와 categories를 써넣어라

![Untitled](/images/git_myblog/Untitled%209.png)

구글링 : hexo multiple categories

### 팁

-깃허브 프로젝트 주소

-깃허브 블로그 주소

이 2가지는 회사에  자기 PR 할 때는 발표자료에 적어야 한다.

그러니 반드시 배포까지 완료해야 한다.