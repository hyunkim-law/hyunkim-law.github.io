---
layout: legal
title: "스마트 컨트랙트 또는 덤 로이어 (Smart contract or dumb lawyer)"
categories: law
date: 2018-06-29 18:00:00 +0900
---
변호사라면 스마트 컨트랙트 내지는 영리한 계약 이야기를 들으면 기분이 나빠진다. 일자리 뺏길까봐 그런 것은 아니다. 그건 먼 옛날 이야기이고 ... 또 변호사는 먼 미래에 대해서 그렇게 걱정하지도 않고 기대하지도 않는다. 정작 기분나쁜 것은 누군가 자기네가 스마트 컨트랙트를 만들었다고 하면, 

> 뭐야, 그럼 지금까지 내가 만든 것은 덤 컨트랙트라는거야? 그리고, 덤 컨트랙트를 만든 나는 덤 로이어라는거야?

라는 반응이다. 잠시 숨을 가라앉히고,

**1\.** "원자의 가운데에는 원자핵이 있고, 그 주위를 전자들이 돌고 있지. 마치 태양계의 행성들이 태양 주위를 돌듯이..." 

이런 이야기를 들어 보았을 것이다. 들어가 봤어? 어떻게 알아? 아, 그건, 그게 아니고, 여러가지 실험을 해 보니까 그럴 거라는 거지... 

[러더포드 모델](https://en.wikipedia.org/wiki/Rutherford_model)이라고 한다. 이건 그냥 모델일 뿐이다. 그러니까, 현실은 이럴 것이라고 상상해서 그린 것일 뿐이다. 모델이 바뀐다고 해서 모델에 대응하는 현실이 바뀌는 것은 아니다. 솔직히 현실은 모델 따위는 신경도 쓰지 않는다.

**2\.** 옛날에는 누가 땅문서를 들고 나가서 집안 재산을 다 팔아먹었다는 등의 이야기를 들었을 것이다. 도대체 집문서가 왜? 그따위 종이쪼가리 가지고 가서 팔았다고 해서 그게 뭐? 옛날에는 땅문서로 매매를 했지만, 요즘은 다 전산화가 되어 있어서 사실상 중요한 것은 등기소의 데이터이다. 위의 모델과는 달리 옛날에는 땅과 종이가 1:1로 매핑이 되어 있었던 것이고, 요즘은 등기소의 데이터와 1:1로 매핑이 되어 있는 것이다.

**3\.** 모델과 매핑은 다르다. 디지털 세계의 특징은 무한복사가 가능하다는 것이다. 그러니까 컴퓨터는 모델링에는 엄청난 힘을 자랑하지만, 매핑은 글쎄... 이 문제를 해결한 것이 [사토시 나카모토](https://en.wikipedia.org/wiki/Satoshi_Nakamoto)의 유명한 논문 [Bitcoin: A Peer-to-Peer Electronic Cash System](https://bitcoin.org/bitcoin.pdf) (2009)이라는 논문이었다. 이 논문의 핵심 주제가 이중지급을 어떻게 방지할 것인가에 대한 것이었다. 여기서 "이중지급"이라는 문제를 "복사"라고 바꾸고 생각해 보라. 디지털 세계에서 디지털 세계를 디지털 세계답게 만드는 특징을 제거하자는 것이다.

가장 쉬운 방식은 등기소와 같은 중앙집중 저장소를 만드는 것이다. 그렇지 않으면? 이것이 바로 비트코인이다. 화폐는 중앙집중식이다. 한국은행에서 발행하면 화폐이다. 중앙의 절대권자가 없는 화폐 시스템은 어떻게 가능할까? 사토시 나카모토의 해법은 돈 자체에 돈의 거래 이력을 저장하자는 것이다. 그러니까, 거래이력을 저장한 파일이 바로 돈인 것이다. 거래이력 자체를 돈이라고 부르자는 말이다. 내가 가지고 있는 천원짜리 만원짜리 지폐가 돈인 이유와 사실상 다를 것이 없다. 이것을 암호화하고, 그 암호화된 내용을 누군가가 풀면 그것을 거래의 증명으로 삼자는 것이다. 옛날에는 은행에 금을 맡겨 두면 은행에서 증명서를 발행하였다(고 한다). 그 증명서를 은행에 주면 금과 바꾸어 주니 사실상 화폐의 역할을 하는 셈이다. 증명서 대신 내지는 증명서에 거래 이력을 모조리 적어 놓으면? 그게 바로 수표에 "이서"하는 것이다. 다른 사람에게 줄 때마다 그 사실을 화폐 자체에 적어 놓는 것이다.

복사방지는 매핑으로 가는 첫걸음이다. 비트코인은 복사가 안되지만 --- 그러니까 파일은 복사가 되지만, 거래 이력 자체는 고유하다는 뜻 --- 아직은 현실과 매핑되어 있지 않다.

**4\.** 이 문제를 해결하고자 하는 것이 스마트 컨트랙트이다. 프로그래밍 코드를 삽입하여 어떤 조건이 성취되면 그 코드가 실행되도록 하는 것이다. 이 이야기를 처음 한 사람은 [Nick Szabo](https://en.wikipedia.org/wiki/Nick_Szabo)라고 한다. 1997년 그는 이렇게 썼다.[^1]

[^1]: Nick Szabo, [The Idea of Smart Contracts](https://web.archive.org/web/20150328060814/http://szabo.best.vwh.net/smart_contracts_idea.html)

> 많은 종류의 계약 조항들을 (예를 들면, 담보, 채권, 재산권의 명시 등) 우리가 다루는 하드웨어와 소프트웨어에 삽입함으로써 계약의 위반자로서는 계약 위반의 비용을 높일 수 있다 (원한다면 위반이 불가능할 정도로). 대표적인 현실의 예를 들자면, 이것은 스마트 컨트랙트의 원시 조상이라고 할 수 있는데, 평범한 자동판매기이다. 손해를 볼 가능성이 있지만 제한적인 범위 내에서 (돈 상자 속의 금액은 기계의 작동을 망가뜨리는 비용보다 적어야 한다) 이 기계는 동전을 받고, 단순한 작동방식으로 --- 이 방식은 컴퓨터과학 신입생의 유한오토마타 설계 문제이다 --- 표시된 가격에 따라 잔돈을 거슬러주고 제품을 준다. 자동판매기는 주인과의 계약이다. 동전이 있는 사람이라면 누구나 주인과의 거래에 참여할 수 있다. 잠금장치와 기타 보안장치들은 보관된 동전과 내용을 공격자로부터 보호하고, 이로써 다양한 분야에서 자동판매기를 활용할 수 있게 된다.

> Many kinds of contractual clauses (such as collateral, bonding, delineation of property rights, etc.) can be embedded in the hardware and software we deal with, in such a way as to make breach of contract expensive (if desired, sometimes prohibitively so) for the breacher. A canonical real-life example, which we might consider to be the primitive ancestor of smart contracts, is the humble vending machine. Within a limited amount of potential loss (the amount in the till should be less than the cost of breaching the mechanism), the machine takes in coins, and via a simple mechanism, which makes a freshman computer science problem in design with finite automata, dispense change and product according to the displayed price. The vending machine is a contract with bearer: anybody with coins can participate in an exchange with the vendor. The lockbox and other security mechanisms protect the stored coins and contents from attackers, sufficiently to allow profitable deployment of vending machines in a wide variety of areas.

**5\.** [Jeffrey M. Lipshaw](https://papers.ssrn.com/sol3/cf_dev/AbsByAuth.cfm?per_id=381790)는 말한다.

> 예를 들어 5만 평방피트의 사무실공간을 10년간 임대할 때 발생할 수 있는 우발상황들의 입출력을 정리할 수 있는 프로그램의 경우, 계약은 물리 세계를 매핑하거나 대체하는 부동산 사업과 법률의 복잡한 세계를 가상으로 창조할 수 있어야 한다.

> [...] say in connection with a program that can sort out the puts and takes of ten years' worth of contingency in a 50,000 square foot office lease, the contracts needs to be able to create virtually a complex world of real estate business and law that either maps on or substitutes for the physical version. (p. 7)

그보다 더 심각한 문제는 이런 복잡한 디지털 [평행우주](https://en.wikipedia.org/wiki/Multiverse)가 서로의 간섭 없이 무한히 생성되고 현실과는 독립적으로 존재할 수 있다는 것이다.

**6\.** 복제방지 기술을 만들었다고 해서, 매핑 문제가 해결된 것은 아니다. 또, 매핑 문제가 해결된다고 해서, 수많은 대안우주 가운데 진짜 우주와 1:1로 매핑이 되지 않는 한은 그것도 문제이다. 그러니까, 시스템 내에서의 복제 문제를 해결했다고 하더라도, 시스템 자체의 복제 문제는 해결되지 않았다는 것이다. 수많은 가상화폐 내지는 암호화폐의 난립을 보라. 그 가운데 --- 적어도 아직은 --- 현실의 화폐와 1:1로 매핑된 것은 없다. 그러므로, 지금의 암호화폐는 본질적으로 [자유지상주의](https://en.wikipedia.org/wiki/Libertarianism) 또는 [아나키즘](https://en.wikipedia.org/wiki/Anarchism)에 더 가까운 것이다. 비록 "돈 때문에" 정부를 불신하는 것이긴 해도 ... (내 돈이 네 돈보다 더 낫단 말이야!)(조금 있으면 돈 때문에 하는 공산주의가 나올 수도? 혹시 기본소득이?)

**7\.** 1995년 8월 9일 [넷스케이프](https://en.wikipedia.org/wiki/Netscape)가 상장했을 때 사람들은 그야말로 광기에 휩싸였다. 웹브라우저가 왜? 한 가지 이론은 (내 생각은) 인터넷 초창기에 사람들이 인터넷과 웹브라우저를 혼동했던 것 같다. 혹시 지금도?

Jeffrey M. Lipshaw, [The Persistence of "Dumb" Contracts](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=3202484)를 읽다가 생각나서 몇 마디 적어 보았다.
