# Entity-Relationship Model

## 개체 관계 모델, 
Entity-Relationship Model
> [Entity-Relationship Model](https://en.wikipedia.org/wiki/Entity–relationship_model)
>
> [The Entity Relationship Data Model](https://opentextbc.ca/dbdesign01/chapter/chapter-8-entity-relationship-model/)

가장 인기있는 개념적 데이터 모델

>Jpa Entity와 다름
>
>같은 철자의 용어를 봤을때 그 의미야! 라고 하지 말고 진정한 의미를 찾아보자 (의미를 넘겨 짚지 말자)
기존에 알고 있는 데이터들과 섣불리 연결하지 말자.
연결하려는 노력은 좋지만, 진정한 의미를 찾으려는 노력을 하자

대게 개체들간 관계를 가지고
정규화를 통해서 엔티티와 관계를 추출한다.

## 정규화

물리적인 모델 들어가기전 개념적으로 만져볼수 있는게 있으면 좋겠다 -> Entity-Relationship Model
Entity: 개별적으로 다룰수 있는 데이터
Entity Type: 같은 Attributes를 가진 Entity들의 "집합"

## ERD
> [ER Diagram MMORPG](https://commons.wikimedia.org/wiki/File:ER_Diagram_MMORPG.png)
> 
> [Cardinality (data modeling)](https://en.wikipedia.org/wiki/Cardinality_(data_modeling))
>

> 논리적인 모델을 시각화 하는 방법
>
> ERD를 도구나 표기법에 집착하지 말고 
>
> ERD를 모델을 검증하는 "도구로" 활용하자

관계(마름모)를 꼭 그려보자
관계를 읽어보고 말이 되는지 확인하자
Crow's Foot Notation을 쓰더라도 Relationship을 꼬박꼬박 써줄 수도 있다.

→ [ERD-artist-performs-song](https://commons.wikimedia.org/wiki/File:ERD-artist-performs-song.svg)