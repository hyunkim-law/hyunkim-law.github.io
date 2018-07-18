---
layout: legal
title: "오픈소스 도구를 이용한 법률문서 코딩과 문서작성 자동화"
categories: lawyering, tools
date: 2018-07-19 02:00:00 +0900
---

변호사는 자고로 능력이 있어야 하고, 기술을 잘 활용할 수 있어야 한다 ([지난번 글](/blog/22018/06/technological-competence.html) 참고). 변호사는 많은 경우 시간당 보수를 청구한다. 그렇다면 기술을 잘 몰라서 과다청구하게 되면 비윤리적인가? 그렇다. 위 글에서도 말한 것처럼 변호사가 코더가 아닌 이상 기술 발전을 아주 잘 알 필요는 없지만, 합리적인 수준에서 기술을 잘 활용할 수 있어야 한다. 옛날에는 부하변호사에게 시켰던 일들---예를 들어, 문서 자동화(document automation 또는 document assembly)을 거의 직접 한다. 기술 발전의 혜택이다. 요즘 (미국) 법조계에서 화두이기도 하다.

이를 위한 솔루션도 많다. 어떤 블로그 글에서는 직접 하는 것이 가장 좋다고 한다.

> 이상적으로는 변호사들이 직접 문서를 자동화하는 것이 좋다. 가장 효과적인 시스템은 변호사들이 마이크로소프트 워드를 이용하여 자기 양식을 직접 자동화함으로써 IT 전문가를 활용하여 법률문서 템플릿을 자동화할 필요를 없애는 것이다. 이렇게 하면, 업무를 주제에 대하여 전문성이 없는 사람에게 시킬 때 어쩔 수 없이 발생하는 리스크를 없앨 수 있고 템플릿 유지를 쉽게 한다. 변호사가 자기의 문서 템플릿을 자동화뿐 아니라 *유지를* 할 수 있게 하는 문서 자동화 소프트웨어를 사용하는 것만이 편지병합 이상의 무엇을 추구하는 프로젝트에는 유일하게 지속가능한 솔루션이다. --- 
[What is document automation?](http://www.lawtechnologytoday.org/2015/01/document-automation/)에서; 번역은 내가

나는 그냥 직접 한다. 소프트웨어는 변한다. 유행도 변한다. 그리고 내가 마이크로소프트 워드를 잘 사용하지 않는 이유를 여러차례 이야기했지만, 사실 가장 큰 이유는 문서를 텍스트로 저장해야만 문서자동화뿐 아니라 계약관리와 버전관리에 유용하기 때문이다. 이 과정을 궁금해 하는 고객들도 꽤 있었고, 고객 또는 경우에 따라 다른 변호사와 협업할 때도 유용할 것 같고, 나도 내 나름 정리해 두면 좋을 것 같아 정리해 둔다. 그리고, 지금까지는 [일못변] 시리즈에서 남들 못하는 것 지적질만 했기 때문에, 나는 어떻게 하는지도 정리해야 하겠다고 생각이 들었다. 나름대로는 오랜 시행착오를 거쳐 정립된 나만의 방법이다.

아래에서는 내가 일을 진행하는 방법을 간략히 정리해 보고자 한다. 편의상 예를 들어, 한 소프트웨어 회사가 앱을 만들었는데 이 앱을 이용하여 미국시장에 진출하고자 하는 경우를 생각해 보자. 상담 결과 법률환경 등에 대한 리서치 결과와 로드맵을 정리한 리서치 의견서와 이를 반영한 약관, 개인정보 사용에 대한 동의 및 [Privacy Policy](https://en.wikipedia.org/wiki/Privacy_policy)를 작성하기로 하였다. 참고로, Privacy Policy는 개인정보의 수집과 사용과 관리에 대한 회사의 방침을 기술한 문서이다. 일종의 유행같은 것이다. 새로 나온 핸드폰처럼 꼭 없어도 되지만, 일단 가지려면 제대로 된 걸 가져야 한다. 꼭 있어야 하는 이유는 남들이 다 가지고 있기 때문이다. 이게 회사의 운영 현실과 맞지 않으면 사기로 처벌받을 수도 있다.

## makefile로 로드맵 만들기

일단 프로젝트를 시작하면, 나는 가장 먼저 [makefile](https://en.wikipedia.org/wiki/Makefile)을 만든다. 예를 들면 다음과 같다.

~~~makefile
MEMO = $(shell date +%F)-memo.pdf
TERMS = $(shell date +%F)-terms-and-conditions.pdf
CONSENT = $(shell date +%F)-consent.pdf
PRIVACYPOLICY = $(shell date +%F)-privacy-policy.pdf
YAML = common.yaml
CONTRACTTEMPLATE = contractTemplate.tex
MEMOTEMPLATE = memoTemplate.tex
ENGINE = lualatex
MEMODRAFT = memo.md
TERMSDRAFT = terms.md
CONSENTDRAFT = consent.md
PRIVACYPOLICYDRAFT = privacyPolicy.md
BIBFILE = research.bib

memo: $(YAML) $(MEMOTEMPLATE) $(MEMODRAFT) $(BIBFILE)
	pandoc --filter pandoc-citeproc -o $(MEMO) $(YAML) $(MEMODRAFT) --template=$(MEMOTEMPLATE) --pdf-engine=$(ENGINE)
terms: $(YAML) $(CONTRACTTEMPLATE) $(TERMSDRAFT)
	pandoc -o $(TERMS) $(YAML) $(TERMSDRAFT) --template=$(CONTRACTTEMPLATE) --pdf-engine=$(ENGINE)
consent: $(YAML) $(CONTRACTTEMPLATE) $(CONSENTDRAFT)
	pandoc -o $(CONSENT) $(YAML) $(CONSENTDRAFT) --template=$(CONTRACTTEMPLATE) --pdf-engine=$(ENGINE)
privacypolicy: $(YAML) $(CONTRACTTERMS) $(PRIVACYPOLICYDRAFT)
	pandoc -o $(PRIVACYPOLICY) $(YAML) $(PRIVACYPOLICYDRAFT) --template=$(CONTRACTTEMPLATE) --pdf-engine=$(ENGINE)
~~~

`makefile`이 무엇인지 아는 사람은 금방 이해했겠지만, 여기에는 프로젝트 전체의 로드맵이 있다. 사실 프로젝트 관리에 `makefile`보다 좋은 것은 없다. 모든 결과물에는 `$(shell date +%F)`가 붙어 있으므로, 자동으로 맨 앞에 날짜가 추가된다. 예를 들어, 메모 파일의 최종본은 (오늘 컴파일했다면) `2018-07-19-memo.pdf`가 된다. 여기에서는 4건의 결과물이 있다.

그리고, 모든 프로젝트에 공통으로 적용되는 내용 (예를 들어, 고객명, 주소, 날짜 등)은 모두 `YAML` 파일 하나에 기록하여 공유한다. 그리고, 두 개의 템플릿이 있다. 계약서용 템플릿이 있고, 메모/의견서용 템플릿이 있다. 엔진은 `lualatex`을 사용한다. 출력물을 만드는 것은 `pandoc`을 사용한다.

그리고 다섯 개의 초안을 작성하여야 한다. 이 파일들을 솔직히 `tex`으로 작성하는 것이 더 편하다. 마크다운을 아주 좋아하지만, 심각한 문제는 커멘트를 할 수 있는 공식적인 방식이 없다는 것이다. 이 문제는 조금 더 심각한게 `git` 자체에서도 커멘트를 사용할 수 없다. `github`이나 `gitlab`의 `issue` 같은 서비스를 이용해야 한다. 여기에 대해서는 나중에 다시 이야기하겠다. 한 가지 장점이라면, 만약 고객이 소스파일을 원하거나 소스파일로 협업하기를 원할 경우에는 마크다운이 `tex` 파일보다는 조금 더 읽기 편하고, 작업하기 편하다는 것이다.

이제 해야하는 것은 각각의 파일들을 만드는 것 뿐이다.

## 문서자동화

이것만으로도 훌륭한 문서자동화가 가능하다. 문제가 복잡하거나, 계약이 좀 더 복잡하다면, 두 가지 방법이 있다. 첫째는 여러 파일로 나누는 것이다. `latex`의 `\input{}`을 사용하거나, 아니면 `md` 파일을 여럿으로 나누어 위 `makefile`에서 순서대로 정렬해 두기만 하면 된다.

두 번째 방법은 `pandoc template`를 만들어 두는 것이다. 이것은 흔히 자주 사용하는 계약, 예를 들어 자문계약서 등의 경우에 유용하다. 항상 포함되는 조항 등은 템플릿을 만들어 여기 포함시켜 두고, 특정 경우에만 적용되는 것은 별도 파일에 기록하는 방식이다.

나름 꽤나 오랫동안 수정과 변경을 거쳐 정리한 방법이지만, 아주 효율적이다. 나는 이 방법을 통하여 계약서 작성이나 프로젝트 진행 시간을 크게 줄였다.
