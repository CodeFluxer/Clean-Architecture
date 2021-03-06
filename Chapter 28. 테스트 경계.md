#Chapter 28. 테스트 경계

- 아키텍쳐 관점에서 모든 테스트(단위, 통합, 인수, 기능, ...)는 동일하다
- 테스트는 태생적으로 의존성 규칙을 따르며 세부적이고 구체적이다
- 테스트는 아키텍쳐의 가장 바깥쪽 원으로, 테스트는 시스템의 컴포넌트에 의존하는 단방향 의존관계
- 테스트는 독립적으로 배포 가능하며 시스템 컴포넌트 중에 가장 고립되어 있다

1. 테스트를 고려한 설계
    - 종종 테스트가 시스템의 설계 범위 밖에 있다고 여기는데 이는 치명적인 실수
    - 테스트가 시스템의 설계와 잘 통합되지 않으면 테스트는 깨지지 쉬워지고 시스템은 변경하기 어려워진다
    - 시스템에 강하게 결합된 테스트라면 사소한 변경으로 인해 수많은 테스트가 깨지고 테스트가 변경되어야 한다
        - 깨지기 쉬운 테스트 문제(Fragile Tests Problem)
    - 변동성이 있는 것에 의존하지 말라
        - ex. GUI
    
2. 테스트 API
    - 모든 업무 규칙을 검증하는 용도
    - 보안 제약사항을 무시
    - 비싼 자원 (ex.DB) 건너뜀
    - 테스트 가능한 특정 상태로 강제
    - 테스트-UI 분리 뿐만 아니라 테스트-애플리케이션 분리 목적
    
3. 구조적 결합
    - 테스트 결합중에 가장 강하고 은밀하게 퍼져나가는 유형
    - 모든 상용 클래스에 테스트 클래스가 각각 존재하고 모든 상용 메서드에 테스트 메서드가 존재하는 테스트 스위트 가정
        - 애플리케이션 구조에 강하게 결합되어 있다
        - 상용 클래스나 메서드가 변경된다면 딸려있는 다수의 테스트가 변경 되어야한다
    - 테스트 API의 역할은 애플리케이션의 구조를 테스트로부터 숨기는데 있다 
    - 시간이 지날수록 **테스트는 계속해서 더 구체적이고 더 특화된 형태로 변하고**
    - **상용 코드는 더 추상적이고 범용적인 형태로 변한다** 

4. 보안
    - 테스트 api가 지닌 강력한 힘을 운영 시스템에 잘못 배포하면 회사에서 짤린다 
    
5. 결론
    - 테스트는 시스템의 외부에 있는 것이 아닌 시스템의 일부이다.
    - 시스템의 일부로 설계하지 않으면 깨지기 쉬운 테스트가 되고 유지보수하기 어려워져 결국 버려진다.
   
    