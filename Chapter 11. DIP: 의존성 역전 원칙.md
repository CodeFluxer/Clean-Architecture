### Key Point
- 안정된 추상에 의존시키며 구체에 의존 X 
- 소스 코듸 의존성과 제어 흐름은 반대로 -> 이 원칙이 `의존성 역전` 

## DIP
의존성 역전 원칙에서 말하는 `유연성이 극대화된 시스템`이란 소스 코드 의존성이 추상에 의존하며 구체에는 의존하지 않는 시스템

<br>

- 자바와 같은 정적 타입 언어에서 이 말은 `import` 구문이 오직 인터페이스나 추상 클래스 같은 추상적인 선언만을 참조해야한다는 뜻 
- 구체적인 대상에 절대로 의존해서는 안됨 

이러한 아이디어를 규칙으로 보기에는 비현실적 측면이 있음 

<br>

### Java String 구체 클래스 
그 예시로 자바의 `String`은 구체 클래스이며, 이를 추상 클래스로 만드려는 시도는 현실성이 없음. 이 경우 구체 클래스에 대한 의존성은 벗어날 수 없고, 벗어나서도 안됨 

String은 매우 안정적이다. 클래스가 변경되는 일이 거의 없고 있더라도 엄격하고 통제 됨. 
이러한 이유로 DIP를 논할 때 안전성이 보장된 환경에서는 무시하는 편 

- **피하고자 하는 것은 변동성이 큰 구체적인 요소!** 
- 그리고 이 구체적인 요소는 우리가 개발하는 중이라 자주 변경될 수 밖에 없는 모듈들 

<br>

### 안정된 추상화
대다수의 경우 구현체에 변경이 생기더라도 인터페이스는 변경이 없다. 따라서 인터페이스는 구현체보다 변동성이 낮다! 
인터페이스의 변동성을 낮추기 위해 노력해라 .. 소프트웨어 설계의 기본이다. 

즉 `안정된 소프트웨어 아키텍처`란 **변동성이 큰 구현체에 의존하는 일은 지양하고, 안정된 추상 인터페이스를 선호하는 아키텍처**

DIP가 전달하고자 하는 내용은 다음과 같이 구체적인 코딩 실천법으로 요약할 수 있다. 
- **변동성이 큰 구체 클래스를 참조하지 말라** : 대신 추상 인터페이스를 참조해라 
- **변동성이 큰 구체 클래스로부터 파생하지 말라** : 정적 타입 언어에서 상속은 소스 코드에 존재하는 모든 관계중 가장 강력한 동시에 뻣뻣해서 변경하기 어려움. 신중..
- **구체 함수를 오버라이드 하지 말라** : 대체로 구체 함수는 소스 코드 의존성을 필요로함. 구체 함수를 오버라이드 하면 이러한 의존성을 제거할 수 없게 되며, 실제로는 그 의존성을 상속하게 됨. 차라리 추상 메소드로 선언하고 각자 용도에 맞게 구현해야함. 
- **구체적이며 변동성이 크다면 절대로 그 이름을 언급하지 말라**

<br>

### 팩토리 
DIP를 준수하려면 변동성이 큰 구체적인 객체는 주의해서 생성해야함. 

**Abstract Fatory**

Application은 Service interface를 통해 ConcreteImpl 을 사용하지만, Application에서는 어떤식으로든 ConcreteImpl 인스턴스를 생성해야한다. 

ConcreteImpl에 대해 소스 코드 의존성을 만들지 않으면서 이 목적을 이루기 위해 ServiceFactory#makeSvc 호출 

![image](https://user-images.githubusercontent.com/20153890/120923232-6c906400-c708-11eb-9132-c6452d92541f.png)

왜 service..?

곡선은 구체적인 것들로부터 추상적인 것들을 분리함. 소스 코드 의존성은 해당 곡선과 교차될 때 모두 한방향, 즉 추상적인 쪽으로 향한다. 

**제어 흐름은 소스 코드 의존성과는 정반대 방향으로 곡선을 가로지른다는 점에 주목하자.** (어디서 가로지르는지..? Application -> ConcreteImpl)

다시 말해 소스코드 의존성은 제어흐름과는 반대 방향으로 역전된다. 이러한 이유로 이 원칙을 `의존성 역전` 이라 부른다. 

<br>

### 구체 컴포넌트 
위 그림에서 `구체 컨포넌트`에는 하나의 구체적인 의존성이 존재함 (ServiceFactoryImpl --> ConcreteImpl), 따라서 DIP 위배된다. 그러나 이는 일반적인 경우

DIP 위배를 모두 없앨 수 없음. 

대다수의 시스템은 이러한 구체 컴포넌트를 최소한 하나는 포함하게 됨. 보통 이 컴포넌트를 main이라 부르는데 메인함수를 포함하기 때문 

위 그림의 경우는 main 함수는 ServiceFatroyImpl 인스턴스를 생성한 후, 이 인스턴스를 ServiceFactory 타입으로 전역변수에 저장해 사용. 


<br>
<br>

**의존성 역전**

![image](https://user-images.githubusercontent.com/20153890/120923951-4076e200-c70c-11eb-9d4e-7836fd1d905a.png)

