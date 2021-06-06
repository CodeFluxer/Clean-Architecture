#Chapter 7. 단일 책임 원칙(SRP: Single Responsibility Principle)

단일 책임원칙 이란 모듈이 하나의 일만 해야한다는 의미가 아니다

> 하나의 모듈은 오직 하나의 액터에 대해서만 책임져야 한다

- 모듈은 일반적으로 소스파일을 의미한다고 볼 수 있다

1. SRP 위반 징후

    1. 우발적 중복

    ```
    // 하나의 모듈이 여러 액터(CFO팀, COO팀, CTO팀) 에 대해서 책임진다
    class Employ {
        // 회계팀에서 CFO 에게 보고
        public long calulatePay();
        // 인사팀에서 COO 에게 보고 
        public void reportHours();
        // DBA 가 기능을 정의 후 CTO 에게 보고 
        publuc void save();
    }
    ```
    
    - 서로 다른 팀에서 적용한 변경 사항이 하나의 모듈 안에 있으므로 상호 영향 끼친다

    2. 병합 (Merge)
    
    - 많은 사람이 서로 다른 목적으로 동일한 소스 파일을 변경하는 경우에 병합이 일어나고 병합에는 위험이 따른다
    
2. 해결책 : 메서드를 각기 다른 클래스도 이동 시킨다 

    1. 데이터와 메서드를 분리
    ```java
      class PayCalculator {
          private EmployeeData employeeData;
          public long calulatePay();
      }
      
      class HourReporter {
          private EmployeeData employeeData;
          public void reportHours();
      }
      
      class EmployeeSaver {
          private EmployeeData employeeData;
          publuc void save(); 
      }
      
      class EmployeeData {
          // data about employee
      }
   
      // Facade 패턴 : 서브시스템에 대한 통합된 인터페이스 제공
      class EmployeeFacade {
          private PayCalculator payCalculator;
          private HourReporter hourReporter;
          private EmployeeSaver employeeSaver;
          public long calulatePay { return payCalculator.calculatePay(); }
          public void reportHours { return hourReporter.reportHours(); }
          public void save { return emplyeeSaver.save(); }
      }
    ```

    2. 중요한 업무 규칙을 데이터와 가깝게 배치
    ```java
       class Employee {
           private EmployeeData employeeData;
           private HourReporter hourReporter;
           private EmployeeSaver employeeSaver;
           public long calulatePay() { //implement }
           public void reportHours { return hourReporter.reportHours(); }
           public void save { return emplyeeSaver.save(); } 
       }
    ``` 

