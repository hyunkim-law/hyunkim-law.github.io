---
layout: post
title: "VS Code의 tasks"
categories: ["how"] # suggestion: gtd, how, lawyering, news, stuff, books, english
excerpt: "VS Code의 태스크 설정하기"
sharing:
  facebook: "VS Code의 태스크 설정하기"
  twitter: "VS Code의 태스크 설정하기"
  linkedin: "VS Code의 태스크 설정하기"
color-scheme: cyan # available: red, orange, green, cyan, blue, magenta, brown 
date: 2020-03-17 15:38:34 +0900
tags: 
math: # true possibly
header-img: lawbook.jpg
# To include book: {% include book.html id='calstory' %}
# To include image: {% include image.html url='FN' description='description' alt='alt' %}
---

VS Code의 [태스크](https://code.visualstudio.com/docs/editor/tasks) 기능 아주 유용하다.

[지킬](https://jekyllrb.com)로 블로그를 운영하면, 커맨드라인과 [VS Code](https://code.visualstudio.com/)를 같이 열어 놓고 쓰겠지만, 태스크 기능을 이용하면 커맨드라인을 굳이 따로 열어 둘 필요가 없다. 메뉴창의 `Terminal` 아래 `Configure Tasks`를 클릭한다. 그 다음 `json` 파일을 편집하여 태스크를 설정할 수 있다. 나의 경우에는 다음과 같이 설정해 두었다.

~~~json
{
    // See https://go.microsoft.com/fwlink/?LinkId=733558
    // for the documentation about the tasks.json format
    "version": "2.0.0",
    "tasks": [
        {
            "label": "runlocal",
            "type": "shell",
            "command": "bundle exec jekyll serve",
            "group": {
                "kind": "build",
                "isDefault": true
            }
        }
    ]
}
~~~

여기에서 `label`은 표시되는 이름, `type`은 `shell`로 설정, `command`에는 실행할 명령어이다. 마지막으로 `group`의 `kind`와 `isDefault`가 필요한 이유는 따로 빌드하지는 않지만, 이렇게 설정해 두면, `Terminal` 클릭한 다음 `Run Task...` 클릭하여 선택하는 대신 `Run Build Task`를 선택하면 훨씬 간단하며, 나아가 여기에는 `Ctrl + Shift + B` 단축키도 주어진다. 생각보다 유용하다.

참고로, `VS Code`에서 터미널을 여는 단축키는 ``Ctrl + Shift + ` ``이다.