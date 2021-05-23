## Key Point
- 함수형 프로그래밍에서의 변수 상태에 초점
- 함수형 언어에서 변수는 변경되지 않는다
- 함수형 프로그래밍은 변수 할당에 부과되는 규율이다. 

## Functional Programming 정의 
함수형 프로그래밍은 `순수 함수`로 나누어 문제를 해결하는 기법, 작은 문제를 해결하기 위한 함수를 작성하고 사용 

- 자료 처리를 수학적 함수의 계산으로 취급하고 **상태**와 **가변 데이터**를 멀리하는 프로그래밍 패러다임의 하나
- 명령형 프로그래밍에서는 **상태**를 변경하는 것을 강조하는것과 달리, 함수형 프로그래밍은 함수의 응용을 강조한다.

Side Effect가 없는 Pure Function을 [1급객체](https://ko.wikipedia.org/wiki/%EC%9D%BC%EA%B8%89_%EA%B0%9D%EC%B2%B4)로 

**Pure Function**
- [설명](https://ko.wikipedia.org/wiki/%ED%95%A8%EC%88%98%ED%98%95_%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D)
- Side effect가 없는 함수 (함수의 실행이 외부에 영향을 끼치지 않는 함수, thread-safe) 
   - 함수가 결과값 이외에 다른 상태를 변경시킬 때 side-effect가 있다고 말함.
   - e.g.) 함수가 전역변수나, static 변수를 수정 / 인자를 변경 등 
   - 이러한 side-effect는 프로그램 동작을 이해하기 어렵게 만든다. 

<br>

> Functional Programming is programming without assignment statements

출처:clean code 

<br>

**함수형 프로그래밍이 아닌 경우의 예시**

자바는 가변변수를 사용하는데, 가변 변수 프로그램은 실행중에 상태가 변할 수 있다. 
- i에는 1~25까지의 값이 할당되어지고 상태는 계속 변한다. 

```java
public class Squint {
	public static void main(String args[]) {
    	for (int i=0; i<25; i++)
        	System.out.println(i*i);
    }
}
```

함수형 언어인 클로저로 이를 작성하면 아래와 같다. 

```closure
(println //출력한다. 
	(take 25 // 처음부터 25까지
    	(map (fn [x] (* x x)) //제곱을, 익명항수 
        	(range)))) //정수의
```

자바의 예제에서는 반복문을 제어하는 변수인 i는 가변변수이다. 그러나 **클로저에서는 x와 같은 변수가 한번 초기화 되면 절대로 변하지 않는다.**

명령형 프로그래밍에서는 메소드 호출시 변수의 메모리 값이 변경될 수 있음. 그러나 **함수형 프로그래밍에서는 이러한 대입문이 없기에 한번 할당된 값은 변할 수 없음**

<br>

### 불변성과 아키텍처 
가변 변수로 인해 발생하는 문제들은 다음과 같다.

- 경합(race)
- 교착상태(deadlock)
- 동시 업데이트(concurrent update)
- 만약 어떠한 변수도 갱신되지 않는다면 경합 조건이나 동시 업데이트 문제가 일어나지 않는다.

동시성 어플리케이션에서 가변성이 없다면 절대로 문제가 생기지 않음.. 

불변성이 가능하다면 이는 대체로 긍정적이다.

단, 저장 공간이 무한하고 프로세서의 속도가 무한히 빠르다고 전제하는 경우에 말이다.
자원은 무한대가 아니다. 따라서 일종의 타협이 필요하다.

### 가변성의 분리 
- 불변성과 관련해 가장 주요한 타협 중 하나는 애플리케이션, 또는 애플리케이션 내부의 서비스를 가변 컴포넌트와 불변 컴포넌트로 분리하는 일이다.
- 불변 컴포넌트에서는 순수하게 함수형 방식으로만 작업이 처리되며, 가변 변수는 사용되지 않는다.

![image](https://user-images.githubusercontent.com/20153890/119259491-8bbbcb80-bc09-11eb-8f6a-b1595ebdaca8.png)

- 현명한 아키텍트라면 가능한 한 많은 처리를 불변 컴포넌트로 옮겨야 하고, 가변 컴포넌트에서는 가능한 한 많은 코드를 빼내야 한다.

<br>

### 이벤트 소싱 
https://mjspring.medium.com/%EC%9D%B4%EB%B2%A4%ED%8A%B8-%EC%86%8C%EC%8B%B1-event-sourcing-%EA%B0%9C%EB%85%90-50029f50f78c

<br>

## 번외편 

### 자바의 함수형 
자바는 Functional Interface를 기반으로 입력에 의해서만 출력이 결정되도록하는 Pure function을 표현할 수 있게 되었고
이를 람다식으로 표현함으로 익명함수를 정의, 또한 higher-order function을 정의할 수 있게 됨 

### Lambda final keyword 
불변의 예로 자바 lambda는 final 키워드가 붙은 변수이거나, effectively final 변수가 아니면 사용할 수 없음 (compile error) 

- effectively final: 변수에 final 키워드를 붙이지는 않았지만, 변수를 재 할당하지 않아 참조가 변경되지 않는 변수 

```java
	@Test
	public void test() {
		Integer a = 10; // effectively final
		// a = 20; // a의 상태에 변경이 일어나면 effectively final 변수가 아님. 

		IntStream.range(1, 10)
				.map(e -> e + a)
				.map(e -> e * e)
				.forEach(System.out::println);

		Flux.range(1, 10)
				.map(e -> e + a)
				.map(e -> e * e)
				.doOnNext(System.out::println)
				.blockLast();
	}
```

### 람다 캡쳐링 
- 람다식의 매개변수가 아닌 외부에서 정의된 변수를 `자유 변수`라고 부름
- 람다 캡쳐링은 람다 바디에서 자유변수를 참조하는 행위 

인스턴스 변수이거나, static 변수인 경우는 관계없으나, **지역변수가** final / effectively final이 아닌 경우는 안됨 

```java
	@Test
	public void test2() {
		Integer a = 10; // effectively final
		// a = 20; // a의 상태에 변경이 일어나면 effectively final 변수가 아님. 

		IntStream.range(1, 10)
				.map(e -> e + a) // e는 람다식의 매개변수, a는 외부 지역변수이므로 `자유변수`
				.map(e -> e * e)
				.forEach(System.out::println);

		Flux.range(1, 10)
				.map(e -> e + a) // e는 람다식의 매개변수, a는 외부 지역변수이므로 `자유변수`
				.map(e -> e * e)
				.doOnNext(System.out::println)
				.blockLast();
	}
```

### 람다식의 외부 지역변수는 복사본
지역 변수는 해당 스레드 스택에 생성됨. 지역변수가 선언된 block이 끝나면 스택에서 제거 됨
   - 메소드 내에서 지역변수를 참조하는 람다식이 있는 경우, 메소드 block이 끝나면 지역변수가 스택에서 제거되므로 참조 불가일 수 있음 

람다식이 실행되는 스레드가 동일하지 않을 수 있다. 
   - 람다식이 다른 스레드에서 실행되면 해당 지역변수를 참조할 수 없다. 
   
### 외부 지역 변수가 final 속성이여야 하는 이유
- 멀티 스레드 환경에서 람다식 사용시, 모두 람다 캡쳐링을 진행 
   - 이때 외부 지역 변수에 변경이 일어나면 sync 문제가 발생할 수 있음 
   - 예를들어 값이 10으로 복사되어 왔어도 실제로 다른 스레드에서는 11, 12인 상태로 작업이 시작될 수 있음
   - 따라서 이 sync를 맞춰주기 위해 **final / effectively final**을 사용해야함 
