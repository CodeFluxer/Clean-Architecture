#Chapter 9. 리스코프 치환 원칙(LSP: Liskov Substitution Principle)

>  자료형 S가 자료형 T의 하위형이라면 T의 객체를 S의 객체로 교체(치환)할 수 있어야 한다 

1. 예제
    1. 상속과 LSP
    ```java
       Interface License {
           public long calcFee();
       }
   
       class PersonalLicense implements License {
           public long calcFee(){ // }
       }
   
       class BusinessLicense implements License {
            public long calcFee(){ // }   
       }
    ```
        - License 하위 타입에 의존하지 않음으로써 이들 하위타입이 모두 License 타입을 치환 가능
   
   2. 정사각형/직사각형 문제
   ```java
       class Rectangle {};
       class Square extends Rectangle {};
   ``` 
        - Rectangle 만 높이와 너비 독립적으로 변경가능하므로 하윕타입으로 적절치 않다
        
2. LSP 와 아키텍쳐
    - 초창기에는 이처럼 LSP 는 상속의 가이드 하는 방법으로 여겨졌다
    - 시간에 흐름에 따라 LSP 는 인터페이스와 구현체에도 적용되는 더 광법위한 윈칙으로 변모했다
    
3. 아키텍쳐의 LSP 위반 사례
    - 택시 파견 서비스를 통합하는 어플리케이션이 있다고 가정했을떄 택시 업체 A와 B의 인터페이스가 다르다면
    - 택시 업체 A: purplecb.com/driver/Bob/pickupAddress/24 Maple St./puckupTime/153/destination/ORD
    - 택시 업체 B: acme.com/driver/Bob/pickupAddress/24 Maple St./puckupTime/153/dest/ORD
    - 인터페이스가 치환 가능하지 않다는 사실을 처리하는 추가적이고 복잡한 메커니즘이 필요해진다 
