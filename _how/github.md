---
layout: page
title: 깃헙 페이지로 홈페이지/블로그 만들기
author: Hyun Kim
category: web
order: 001
---

## 목차
{:.no_toc}

* ToC
{:toc}

---

## 성질 급한 사람을 위한 요약



## 깃헙에 새로운 페이지 만들기
깃헙 페이지란 지킬을 이용하여 홈페이지 또는 블로그를 만들고 관리할 수 있는 서비스이다.[^fn1] 왜 이걸 만들어야 할까?  첫째, [깃헙](https://github.com)은 거의 전세계 개발자가 다 사용하고 있는 서비스이다.  여기에 자기소개나 이력서같은 것을 올려 놓으면 아주 좋다. 둘째, **공짜** 이다!  셋째, 다양한 프로젝트를 여기에 저장할 수 있다.  공개 프로젝트는 무제한 호스팅이 가능하고, 월 7달러만 내면 비공개 프로젝트도 무제한 호스팅을 할 수 있다.

[^fn1]: 자세한 정보는 [깃헙 페이지 설명](https://pages.github.com/)을 참고하라.

## 깃헙에 아이디와 페이지 만들기
일단 깃헙에 아이디를 만든다 (없다면).  유일하게 필요한 것은 이메일이다. 그 다음에는 깃헙 페이지용 저장소를 만든다.  이걸 하려면, 반드시 `아이디.github.io`라는 형태로 만들어야 한다. 예를 들어, 만든 아이디가 `abc`라면, `abc.github.io`라는 저장소를 만들어야 한다.  

그 다음에는 이걸 가지고 온 다음 간단히 파일 하나를 추가한다.  여기에서는 아이디가 `username`이라고 가정하였다.

~~~bash
$ git clone https://github.com/username/username.github.io
$ cd username.github.io
$ echo "Hello World" > index.html
~~~

그리고, 이렇게 수정한 내용을 원격으로 깃헙에 보낸다.

~~~bash
$ git add --all
$ git commit -m "Initial commit"
$ git push -u origin master
~~~

이렇게 하고 나면, 인터넷 브라우저로 `username.github.io` 페이지를 찾아가면 홈페이지가 보일 것이다.  

## ssh 설정


### 여러 아이디 사용에 대한 노트
일단 이해해야 하는 것은 

~~~bash
$ git clone http://vcs.icer.msu.edu/git-repos/project.git
$ git clone https://username@vcs.icer.msu.edu/git-repos/project.git
$ git clone ssh://username@vcs.icer.msu.edu/git-repos/project.git
~~~

~~~bash
$ git config user.name
$ git config --global user.email
$ git config user.email
$ git config --global user.email
~~~

환경설정 파일 `.ssh/config`에 두 개의 아이디를 입력한다.

~~~
Host github.com
HostName github.com
IdentityFile /path/to/your/personal/github/private/key
User personal

Host github-work
HostName github.com
IdentityFile /path/to/your/work/github/private/key
User company
~~~

그 다음, 두 번째 사용자로 저장소를 가지고 오려면, 

~~~bash
$ git clone git@github-work:company/project.git
~~~

또 다른 방법은 `core.sshCommand`라는 것을 설정하는 것이다.

~~~bash
$ cd /path/to/my/repo
$ git config core.sshCommand 'ssh -i private_key_file' 
$ git clone host:repo.git
~~~

## 도메인 설정하기

만일 `github.io`로 끝나는 도메인이 마음에 들지 않는다면, 자기가 따로 산 도메인을 지정하여 사용할 수 있다.  모든 도메인 작업이 다 그렇지만, 이 설정은 두 군데에서 해야 한다.  첫째, 도메인 서비스를 제공하는 곳, 그리고 둘째는 도메인이 연결될 곳 - 그러니까 이 경우에는 깃헙 - 이다.  쉬운 것부터 하자면, 깃헙에서는 위에서처럼 최초로 푸시를 하고 나면 (즉 내용이 있으면) 페이지가 설정이 된다.  그 다음에 해당 프로젝트 페이지의 `Settings`를 찾아 가서 커스텀 도메인(Custom Domain)을 클릭한 다음 원하는 도메인명을 넣고 확인하면 된다.

그 다음이 좀 더 까다롭다. 왜냐하면, 도메인 서비스를 제공하는 사람은 아주 많고, 각자 아주 다양한 종류의 서비스를 제공하기 때문이다.  전체적인 설정에 대한 도움말은 [깃헙 페이지에 커스텀 도메인 사용법](https://help.github.com/articles/using-a-custom-domain-with-github-pages/)에서 확인할 수 있다.

우선 도메인에 대하여 조금 이해해야 한다.  도메인은 모두 가운데 점이 하나 찍힌 형태이다.  예를 들어, 이 사이트의 도메인은 `hyunkim.lawyer`이다. 