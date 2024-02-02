# Unit Test

## V-Model

> [V-Model](https://ko.wikipedia.org/wiki/V\_%EB%AA%A8%EB%8D%B8)

<figure><img src="../../.gitbook/assets/image (1).png" alt="" width="350"><figcaption><p>V-Model's Software Development Process(Source: <a href="https://ko.wikipedia.org/wiki/V_%EB%AA%A8%EB%8D%B8">Wikipedia</a>)</p></figcaption></figure>

> 우리는 문제를 해결하기 위해 프로그래밍을 한다. (특히 비즈니스 문제)
>
> 문제를 잘 정의하고, 문제가 해결된 모습을 미리 그려보면 -> 문제가 잘 해결되었는지 절반정도는 확신할수 있다.
>
> 폭포수 모델은 뒤로 돌아갈수 없으며, 이는 현실과는 맞지 않지만 -> 폭포수 모델이 다루는 단계들은 매우 유용하다.

V-Model은 각 단계에 대한 테스트를 나누고, 처음부터 어떻게 테스트해야 하는지 결정하려고 노력한다.

1. 인수 테스트 - 요구사항 분석 (사용자 중심)
2. 시스템 테스트 - "시스템을 설계"하고 "시스템의 사양을 결정"
3. 통합 테스트 - 아키텍처 설계 (고수준 설계)
4. 단위 테스트 - 모듈 설계 (저수준 설계)
5. 구현 - 코딩

## Test Matrix

> [Internal And External Quality](https://wiki.c2.com/?InternalAndExternalQuality)
>
> [My Agile testing project](http://www.exampler.com/old-blog/2003/08/21.1.html)
>
> [Developer Testing](https://developertesting.rocks/)

## 내적 품질을 높이면 좋은 이유

일반적으로 말하는 외적 품질도 중요하지만, 내적 품질도 신경쓰자.

* 비즈니스 적인 가치보다 "엉망인채로 가면 큰일난다"
  * ~~맛만 좋으면 되지, 주방이 깨끗할 필요가 있냐 (식당)~~
* 내적 품질이 우수하면, 외적 품질 향상도 쉬워진다.
  * 도구를 개선하는 도구가 장기적으로 생산성을 높인다.

## JUnit

> [JUnit 5](https://junit.org/)
>
> [SUT](http://xunitpatterns.com/SUT.html)
>
> [E2E Test (End to End)](https://medium.com/delivus/e2e-%ED%85%8C%EC%8A%A4%ED%8A%B8-%EA%B5%AC%EC%B6%95%EA%B8%B0-used-aws-step-functions-2fccb930218c)

SUnit(SmallTalk) -> XUnit

* 자동화된 테스트를 지원
* 단위 테스트 뿐 아니라 통합테스트 작성, E2E를 작성하는데도 사용된다.

<figure><img src="../../.gitbook/assets/image (1) (1).png" alt="" width="360"><figcaption><p>Testing Pyramid (Source: <a href="https://medium.com/delivus/e2e-%ED%85%8C%EC%8A%A4%ED%8A%B8-%EA%B5%AC%EC%B6%95%EA%B8%B0-used-aws-step-functions-2fccb930218c">Medium</a>)</p></figcaption></figure>

## E2E 테스트

"사용자의 관점"에서 애플리케이션이 의도대로 작동하는지 테스트

## 단위 테스트

* 믿고 쓸수 있는 부품인가?
* 믿을 수 있는 부품이 있다면 어떻게 하면 되는가?

### 단위 테스트 작성

테스트 작성 시에는 생각나는 테스트를 다 해보는게 좋다.

1. 처음에는 "몇가지 부품이 있다고 가정"하고 코드를 작성한다. ([Newton's Method 예시](https://mitp-content-server.mit.edu/books/content/sectbyfn/books\_pres\_0/6515/sicp.zip/full-text/book/book-Z-H-10.html#%\_sec\_1.1.7))

```c
(define (sqrt-iter guess x)
  (if good-enough? guess x)
    guess
    (sqrt-iter (improve guess x)
      x)))
```

* 자바로 옮기면 이렇게 된다.

```java
public double sqrtIter(double guess, double x) {
  if (goodEnough(guess, x)) {
    return guess;
  }
  return sqrtIter(improve(guess, x), x);
}
```

> 참고
>
> [The Practical Test Pyramid](https://martinfowler.com/articles/practical-test-pyramid.html)
>
> [“Mocking 때문에 테스트 코드를 작성하기 어렵나요” 영상](https://youtu.be/RoQtNLl-Wko)
>
> [“프론트엔드도 테스트해야 하나요?” 영상](https://youtu.be/-kUmsKRmOnA)

### 테스트 코드 여정 (참고)

> 먼저 테스트에 실패하고, 최대한 빠르게 테스트를 통과하는 것이 목적. 테스트가 통과된 후 리팩토링을 진행한다.

#### goodEnough() 테스트

* 테스트 하기에 좋은 값들을 선정

```java
class NewtonMethodTest {
	private NewtonMethod sut;  // System Under Test
	
	@BeforeEach
	void setUp() {
		sut = new NewtonMethod();
	}
	
	@Test
	void goodEnough() {
		// 아래 둘은 너무 명확한 경우
		assertThat(sut.goodEnough(2, 4)).isTrue();
		assertThat(sut.goodEnough(1, 4)).isFalse();
	
		// 이 정도면 괜찮다 싶은 경우
		assertThat(sut.goodEnough(1.999999, 4)).isTrue();
	}
}
```

* goodEnough 구현

```java
public boolean goodEnough(double guess, double x) {
	final double epsilon = 0.001;
	return Math.abs(Math.pow(guess, 2) - x) < epsilon;
}
```

#### improve() 테스트

핵심인 improve를 만들기 위해 뉴튼법으로 2의 제곱근을 구하는 과정을 살펴보자.

> Guess: 1 → (2/1) = 2 → ((2 + 1)/2) = **1.5**
>
> Guess: 1.5 → (2/1.5) = 1.33333 → ((1.33333 + 1.5)/2) = **1.4166**
>
> Guess: 1.4166 → (2/1.4166) = 1.41183 → ((1.4166 + 1.41183)/2) = **1.4142**

* 테스트 코드 작성

```java
@Test
void improve() {
	DecimalFormat decimalFormat = new DecimalFormat("0.####");
	assertThat(decimalFormat.format(sut.improve(1, 2))).isEqualTo("1.5");
	assertThat(decimalFormat.format(sut.improve(1.5, 2))).isEqualTo("1.4166");
	assertThat(decimalFormat.format(sut.improve(1.4166, 2))).isEqualTo("1.4142");
}
```

* improve 구현

```java
public double improve(double guess, double x) {
	return (guess + (x / guess)) / 2;
}
```

#### sqrt(), sqrtIter() 테스트

* 테스트 코드 작성

```java
@Test
void sqrtIter() {
	DecimalFormat decimalFormat = new DecimalFormat("0.######");
	assertThat(decimalFormat.format(sut.sqrtIter(1, 2))).isEqualTo("1.414216");
	assertThat(decimalFormat.format(sut.sqrtIter(1, 3))).isEqualTo("1.732143");
	assertThat(decimalFormat.format(sut.sqrtIter(1, 4))).isEqualTo("2");
}

@Test
void sqrt() {
	DecimalFormat decimalFormat = new DecimalFormat("0.######");
	assertThat(decimalFormat.format(sut.sqrt(2))).isEqualTo("1.414216");
	assertThat(decimalFormat.format(sut.sqrt(3))).isEqualTo("1.732143");
	assertThat(decimalFormat.format(sut.sqrt(4))).isEqualTo("2");
}
```

* 최종 구현

```java
public double sqrt(double x) {
	return sqrtIter(1, x);
}
```

단순한 UnitTest가 가장 많아야, 신뢰할수 있는 토대를 구축할수 있다.

> **참고**
>
> [Mockito](https://site.mockito.org/)
