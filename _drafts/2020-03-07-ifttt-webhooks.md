---
layout: post
title: "게으른 자의 페이스북포스팅: IFTTT Webhooks 사용기"
categories: ["how"] # suggestion: gtd, how, lawyering, news, stuff, books, english
excerpt: "게으른 자를 위한 IFTTT의 Webhooks를 이용하여 커맨드라인에서 페이스북 포스팅하기"
sharing:
  facebook: "게으른 자의 터미널에서 페이스북 포스팅하기를 정리해 보았습니다"
  twitter: "게으를 자의 터미널에서 페이스북 포스팅하기"
color-scheme: cyan # available: red, orange, green, cyan, blue, magenta, brown 
date: 2020-03-07 11:08:29 +0900
tags: 
math: # true possibly
# To include book: {% include book.html id='calstory' %}
# To include image: {% include image.html url='FN' description='description' alt='alt' %}
---

갑자기 페이스북에 뭔가 포스팅할 거리가 생각났다고 해 봅시다. 일단 컴퓨터를 켜고, 브라우저를 열고, 페이스북 주소를 입력하여 간 다음, `게시물 만들기`를 클릭하고, 글을 쓰는 동안 배경에 나오는 여러가지 사진과 동영상과 글에 현혹되지 않고 글을 쓸 수 있어야 합니다.

그게 제가 지금까지 페이스북의 수동적 사용자였던 이유였습니다. 그걸 바꿔 보려 하는데, 그러려면 일단 완벽한 환경을 먼저 갖춰야 합니다. 제가 지금까지 글을 잘 못 쓴 이유는 완벽한 환경이 없었기 때문이니까요. 이상적인 환경은 터미널에서 바로 쓰는 것입니다. 아니면, 내가 좋아하는 편집기 예를 들어 `VS Code`같은 것으로 쓰는 것입니다.

이게 제대로 문서화가 안되어 있어서 찾기가 꽤 까다로왔습니다. 그래서 따로 정리해 둡니다. 

이걸 위해서는 몇 가지를 갖춰야 합니다. 우선 [IFTTT](https://ifttt.com)의 [Webhooks](https://ifttt.com/maker_webhooks)를 이용합니다. 말은 어렵지만, `IFTTT`는 특정 조건이 성취되면 할 일을 정해 놓은 서비스를 제공합니다. `Webhooks`란 인터넷상으로 어떤 정보를 주고받는 것입니다. 그걸 위해서는 우선 주소를 알아야 합니다. [IFTTT](https://ifttt.com) 홈페이지로 가서, 로그인한 다음 주소창에 [https://ifttt.com/maker_webhooks](https://ifttt.com/maker_webhooks)라고 입력합니다. 이렇게 하고싶지는 않지만, 바로 가는 링크를 저는 찾을 수가 없더라구요. 굳이 주소를 입력하기 싫다면, 오른쪽 위의 `Explore` 버튼을 누른 다음, 아래 창에서 `Connections`에 가 있는데 옆의 `Services`로 간 다음에, 검색창에 `webhooks`라고 치면, 파란 상자가 보입니다. 다시 오른쪽 위에 있는 `Documentation` 또는 `Settings` 둘 가운데 아무거나 누르면, 본인의 키값을 알 수 있습니다. 이걸 어딘가에 잘 적어 둡니다. 어차피 컴퓨터로 하는 것이니 그냥 파일에 저장해 둬도 되겠네요. `key`라는 파일에 저장해 뒀다고 해 봅시다. 혹시 `Documentation` 페이지로 갔다면, 간단한 사용법이 있습니다.

