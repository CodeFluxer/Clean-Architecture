#Chapter 30. 데이터베이스는 세부사항 이다

- 아키텍쳐 관점에서 볼 때 데이터베이스는 엔티티가 아닌 세부사항(아키텍쳐 구성요소)이다
- 아키첵쳐가 건물이라면 데이터베이스는 손잡이라고 비유 할 수 있다
- 데이터베이스는 데이터 모델이 아닌 일개 소프트웨어일 뿐이다

1. 관계형 데이터베이스
    - 특정한 형식의 데이터에 접근하기 편리하다
    - 애플리케이션은 행단위로 배치되는 데이터를 알아서도 안되고 관여해서도 안된다
    - 데이터가 테이블 구조를 가진다는 사실은 외부원에 위치한 최하위 수준의 유틸리티 함수만 알아야한다
    - 테이블과 행이 객체형태로 시스템을 돌아다니는 것은 아키텍쳐적으로 잘못된 설계이다 

2. 데이터베이스 시스템은 왜 이렇게 널리 사용되는가?
    - 회전식 자기 디스크가 데이터 저장소의 중심이던 시절
    - 느린 시간지연으로 인해 최적화(배치,색인,캐시,쿼리, ...)가 필요했고 이로 인해 데이터 접근 및 관리 시스템의 필요성이 대두
        - 파일 시스템과 관계형 데이터베이스 관리 시스템(RDBMS)이 탄생
        - 파일 시스템은 문서기반 (문서 내용이 아닌 이름)
        - RDBM은 내용 기반이지만 정형화된 데이터에만 적합

3. 디스크가 없다면 어떻게 될까?
    - 굳이 테이블구조에 저장하지 않고 용도에 맞는 다양한 구조로 저장할 것이다
    - 이미 대부분의 개발자가 데이터베이스에서 읽어본 데이터를 그런식으로 사용하고 있다
    
4. 세부사항
    - 데이터베이스는 그저 메카니즘에 불과하며 디스크 표면과 RAM사이에서 데이터를 옮길떄 사용할 뿐이다
    - 거대한 저장공간 이상의 의미는 없다
    
5. 성능
    - 아키텍쳐 관점에서 성능을 빼놓을 수 없지만 데이터 저장소의 측면에서 성능은 완전히 캡슐화하여 업무 규칙과 분리할 수 있는 관심사이다
    

        
     