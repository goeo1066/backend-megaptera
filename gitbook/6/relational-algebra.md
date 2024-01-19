# Relational Algebra

## 관계대수(Relational Algebra)
- 관계대수는 연산이 이루어지는 수식구조이다.
- 수식은 연산자와 피연산자로 이루어지는데, 피연산자는 테이블이다.
- 단항연산은 테이블 하나를 연산하고, 이항연산은 테이블 두 개를 연산한다.

## 연산

하나 이상의 Relation으로 새로운 Relation을 만들 수 있다.

### 단항연산(Unary Operation)
#### 선택연산(Selection)
- 하나의 테이블에서 조건에 만족하는 레코드를 검색한다.
- 연산자 σ
- 형식 σ<조건식>(<테이블이름>)
- 조건식은 비교연산자와 부울연산자의 조합으로 이루어진다.
  - 부울연산자 ∪(or), ∩(and), NOT
  - address = '성남'
  - salary >= 100
  - address = '성남' ∩ salary >= 100

#### 추출연산(Project)
- 사용자가 원하는 필드만을 출력하는 연산이다
- 관계대수는 중복 레코드가 있으면 중복을 제거하지만, DBMS는 중복레코드를 허용한다.
- 연산자 π
- 형식 π<필드리스트>(<테이블이름>)
- 필드리스트는 필드를 ,(Comma)로 구분해준다.
 
#### 재명명연산(Rename)
- 피연산자인 테이블의 이름을 바꾸는 연산이다.
- 테이블의 필드 이름도 바꿀수 있다.
- 연산자 ρ
- 형식 ρ<new테이블이름>(<테이블이름>)
- 형식 ρ<new테이블이름>(<new필드이름리스트>)(<테이블이름>)

#### 상호중첩
- 연산자는 상호 중첩하여 사용가능하다.

### 이항연산(Binary Operation)
#### 집합연산
- 관계대수에서 이항연산은 집합연산을 의미한다.

##### 1. 합집합
- πname,id(student) ∪ πname,id(professor)

##### 2. 교집합
- πcourse_id(course) ∩ πcourse_id(class)

##### 3. 차집합
- πcourse_id(course) - πcourse_id(class)

##### 4. 곱집합(Cartesian Product)
- 테이블1 x 테이블2이다.
- 곱집합은 호환이 필요없다. 생성될수 있는 모든 경우의 수
- 테이블1의 레코드가 (a,1), (b,2)이고 테이블2의 레코드가 (e,3), (f,4), (g,5)라면 곱집합의 결과는 (a,1,e,3), (a,1,f,4), (a,1,g,5), (b,2,e,3), (b,2,f,4), (b,2,g,5)가 된다.
- Relation의 Cartesian Product는 원래 의미와 다르다

### 추가연산자
#### 1. 조인(Join)
- 곱집합과 비교하여, JOIN은 조건에 부합하는 레코드만 모아서 한개의 테이블로 만든다.
- 형식: 테이블 1 ⨝ <조건식> 테이블2

#### 2. 자연 조인(Natural Join)
- JOIN에서 동등조건(=)이 있는 경우에 하나의 필드만을 명시하여 출력하는 연산이다.
- 형식 : 테이블 1 ⨝ 테이블2

#### 3. 외부 조인(Outer Join)
- 동등조건이 성립하지 않으면 null값을 넣에 테이블을 만드는 연산이다.
- Left Outer Join: 왼쪽 테이블 레코드만 추가
- Right Outer Join: 오른쪽 테이블 레코드만 추가
- Full Outer Join: 양쪽 테이블 레코드 추가

#### 4. 지정 연산(Assignment)
- 일종의 변수, 중간 결과에 이름을 부여해서 수식을 간단하게 만든다.
- 연산자 ←
```text
수식 : πname (σ salary>400 ∩ position = '부교수(professor))
중간 결과 : temp1 ← σ salary>400 ∩ position = '부교수(professor)
수식 : πname (temp1)
```

> [참고 블로그](https://lordofkangs.tistory.com/56)
>
> [Understanding of Database](https://product.kyobobook.co.kr/detail/S000001519128)