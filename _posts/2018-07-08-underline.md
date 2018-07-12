---
layout: legal
title: "[일못변 10] 밑줄이라는 원죄"
categories: lawyering
date: 2018-07-08 16:00:00 +0900
---
고백하자면, 나도 밑줄이라는 원죄에서 자유롭지 못하다. 얼마전 작성한 계약서에서도 밑줄을 썼다.

코더들은 밑줄을 싫어한다. `HTML`에서도 `<i>`, `<b>`, `<u>`는 이미 오래전에 `<em>`과 `<strong>`으로 바뀌었다. [마크다운](https://daringfireball.net/projects/markdown/syntax)과 내가 요즘 주력으로 쓰고 있는 [판독 마크다운](https://pandoc.org/MANUAL.html)에서도 밑줄을 지원하지 않는다. 그렇지만 모든 변호사가 성경책처럼 다루는 --- 그러니까 모두 고이 모셔두고 아무도 읽지 않지만 블루북에서 그러라고 했다고 하면 모두 아무 말 하지 않는 --- [블루북](https://www.legalbluebook.com/)은?

내가 저항한 이유이다. 어떻게 감히 블루북에 저항한단 말인가?

Matthew Butterick은 Typography for Lawyers에서 [말한다](https://typographyforlawyers.com/underlining.html).

> 인쇄한 문서에서는 밑줄을 쓰지 말라. 절대로. 추하다. 그리고 내용을 읽기 어렵게 한다.

> In a printed document, don't underline. Ever. It's ugly and it makes texts harder to read.

그 이유도 납득한다. 옛날 타자기를 쓰던 시대의 구시대적 유물이라는 것이다. 그리고, MS 워드에서는 밑줄이 참 예쁘지 않다. 그렇다고 하더라도, 밑줄을 쓰지 않고 어떻게 판례를 인용한단 말인가?

나에게 이것은 참 어려운 일이었다. 마크다운은 밑줄에 적대적이다. 나는 보통 포맷은 LaTeX으로 하고, 내용은 판독 마크다운을 사용하는 업무 프로세서가 가장 편안하다. 물론 돌아갈 방법은 있다. 나는 [soul](https://ctan.org/pkg/soul) 패키지를 사용한다. LaTeX의 여러 패키지에서 밑줄을 어떻게 처리하는지 예는 [Four ways to underline text in LaTeX](https://alexwlchan.net/2017/10/latex-underlines/)을 참고하라. 기본 패키지에서도 MS 워드에서처럼 아래로 내려오는 소문자 ("descender"라고 한다. 예를 들면 j, g, y)를 침범하지는 않지만, 밑줄이 고르지 않다. 그래서 **soul** 패키지를 사용한다.

문제는 이렇게 할 경우 pdf 출력을 하면 문제가 없지만, MS 워드 파일로 변환하면 (가끔씩 이것을 요청하는 나쁜 사람들이 있다) 판독 마크다운의 구문이 아닌 것들은 인식을 못하고 아예 생략한다. 2--30 페이지 계약서에서 이걸 일일이 찾아서 수정하는 것도 큰 일이다. 그래서 나도 밑줄을 안썼으면 좋겠다. 그렇지만 블루북은? 나도 요즘은 (영어의) 외래어, 예를 들어 라틴어는 이탤릭을 사용한다. 그렇지만, 판례명이나 상호참조는?

최근 알아 내었다. 심지어는 (분명히 블루북을 염두에 둔 제목일) 레드북의 저자 Bryan Garner도 밑줄을 쓰지 말라고 한다. 

> 밑줄은 추하다. 특히 컴퓨터로 작업하여 사무실 프린터로 출력하였을 때에는. 줄이 너무 두껍고 폰트에 너무 가깝다. 사실 밑줄이 흔히 문자의 아래삐침을 침범하기 때문에 읽기도 어렵다 [...] *블루북*에서 법원 문서에서 판례명을 밑줄치라고 하는 것에 대해서만은 이런 반동적인 지침을 무시하고 이탤릭을 사용하라.

> Underlining is ugly, especially on computers and office printers. The line is too thick and too close to the type. In fact, it can be hard to read because it typically obliterates the descenders on the letters *f, g, j, p, q,* and *y* [...] To the extent that *The Bluebook* specifies underlining case names in court papers, override that retrograde guidance and italicize. (The Redbook, 79--80)

정확히 내게 필요한 말이다. 나는 사실상 Bryan Garner처럼 권위있는 사람이 이런 말을 해주길 기다렸던 것 같다. 
