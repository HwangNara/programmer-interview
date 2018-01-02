# Java
* Java8 
  * Lambda
    * ()->{}
    * @FunctionalInterface
  * Stream
    * map, filter, forEach, limit, skip, reduce, collect
  * String join
    * String.join(“_”, strings);
  * Java 5,6,7별 추가된 기능들
    * Generics, G1 GC, try-with-resources, String Switch ...
* JVM
  * GC 과정
    * Young(Eden, Survivor1, Survivor2): 새로 생성된 객체들 존재
    * Old: 생성된 지 오래된 객체들 존재 (mark-sweep-compactaction)
    * Permanent: class, method code 등 저장
  * GC 방식
    * Serial: 적은 메모리, 적은 CPU 코어 수
    * Parallel: Serial과 같지만 여러 개의 처리 쓰레드
    * Parallel Old: mark-summary-compaction
    * CMS(Concurrent Mark & Sweep)
      * Initial mark: 클래스 로더에서 가까운 살아있는 객체 검사
      * Concurrent mark: 방금 산 객체의 참조객체 검사
      * Remark: 전단계에서 추가되거나 끊긴 객체 검사
      * Concurrent Sweep: 쓰레기 정리
    * G1(Garbage First)
* ThreadLocal
  * 개념: 쓰레드 영역에 변수를 설정할 수 있기 때문에, 특정 쓰레드가 실행하는 모든 코드에서 그 쓰레드에 설정된 변수 값을 사용할 수 있게 된다.
  * 용도
    * 사용자 인증정보 전파 - Spring Security에서는 ThreadLocal을 이용해서 사용자 인증 정보를 전파한다.
    * 트랜잭션 컨텍스트 전파 - 트랜잭션 매니저는 트랜잭션 컨텍스트를 전파하는 데 ThreadLocal을 사용한다.
    * 쓰레드 안전해야 하는 데이터 보관
  * 예시
    ````java
    ThreadLocal<UserInfo> local = new ThreadLocal<UserInfo>();
    local.set(currentUser);
    UserInfo userInfo = local.get();
    ````
* Dump
  * Thread
    * Thread Dump 획득
      ```
      kill -3(QUIT) PID
      ```
    * jstack PID
  * Heap
    ``` 
    jmap -dump:format=b,file=<fileName> <PID> 
    ```
* 기타 
  * NIO(NonBloking Input-Output)
    * Framework: Netty(an asynchronous event-driven network application framework)
  * Reflection
    * 리플렉션이란 객체를 통해 클래스의 정보를 분석해 내는 프로그램 기법
    * 메소드 실행, 객체 생성, 필드 값 변경 등이 가능
    * 예시
      ```` Java
      Class c = Class.forName("클래스이름");
      Method[] m = c.getMethods()
      Field[] f = c.getFields();
      Constructor[] cs = c.getConstructors();
      Class[] inter = c.getInterfaces();
      Class superClass = c.getSuperclass();
      ````
  * 멀티 서버 환경에서 세션 공유 방법
    * 파일로 공유
    * DB로 공유
    * Daemon 사용
* Thread
  * Thread pool
    * 갑작스런 병렬작업의 극대화로 인한 스레드 증폭을 막기 위해 사용
    * 작업 처리에 사용되는 스레드를 제한된 개수만큼 정해 놓고 작업 큐(Queue)에 들어오는 작업들을 하나씩 스레드가 맡아 처리
    * Executors의 다양한 정적 메소드를 이용해서 ExecutorService 구현 객체를 만들 수 있는데, 이것이 바로 스레드 풀
  * Thread safe
    * 개념: 여러 개의 thread에서 동시에 호출해도 문제가 되지 않는 클래스
    * synchronized
  * Daemon thread
    * 주 스레드의 작업을 돕는 보조적인 역할을 하는 스레드
    * 주 스레드가 종료되면 자동으로 같이 종료됨
  * Runnable & Callable
    * Runnable: 작업 처리 후 결과값 없음
    * Callable: 작업 처리 후 결과값 있음

# Framework
* 스프링
  * DI/IoC
  * AOP
    * Aspect
    * Pointcut
    * JoinPoint
    * Advice
    * Weaving(Cross cutting)
  * PSA(Portable Service Abstraction)
  * Spring Boot
  * Annotation
    * @ComponentScan
    * @Transactional
  * Bean Scope
    * Singleton: 컨테이너에 1개. 계속 유지(컨테이너가 존재하는 한)
    * Request: HTTP요청 생길 때 마다
    * Session: HTTP 세션별로 생성
    * Prototype: 컨테이너에 빈을 요청할 때마다 생성
  * Quartz/Spring batch
    * Quartz: a scheduling framework. Like "execute something every hour or every last Friday of the month"
    * Spring batch: a framework that defines that "something" that will be executed. You can define a job, that consists of steps
    * 결론
      * Spring Batch Job을 실행시키기 위해 Quartz를 사용
      * Spring Batch defines what should be done, Quartz defines when it should be done.
    * Request Context
* JPA(Java Persistance API)
  * 사용 이유
    * 생산성, 유지보수, 패러다임의 불일치 해결, 성능, 데이터 접근 추상화와 벤더 독립성, 표준
  * Annotation
    * @Entity, @Table, @Id, @Column ...
* Mybatis
  * #과 $의 차이

# 디자인패턴
* 종류
  * Singleton
  * Factory Method
  * Template Method
  * Strategy
  * Adapter
  * Proxy
* 용어
  * Aggregation: 구성(라이프 사이클이 다름. 사람과 주소)
  * Composition: 부분(라이프 사이클이 같음. 자동차와 엔진)

# Javascript
* Jsonp(Json With Padding)
  * Same Origin Policy를 피하기 위해 사용하는 기법으로, 응답 json을 padding(함수명)으로 감싸서 불러오는 방식
* JS scope
  * 실행 컨텍스트(활성화 객체, Scope Chain, this) 내의 variables들이 각각 생성
  * 전역변수의 오,남용이 없는 깔끔한 스크립트를 작성 할 수 있음

# 자료구조 & 알고리즘
* Tree
  * Binary Search Tree(BST): 부모는 2개의 자식만 가지며, 왼쪽은 서브트리는 부모노드의 값보다 보다 작고 오른쪽 서브트리는 부모노드의 값보다 큰 값들로 이루어진 트리
  * B-Tree: 균형잡힌 외부 다진 검색트리
  * Red black tree
    * 루트는 블랙, 모든 리프(NIL)는 블랙, 노드가 레드이면 자식은 블랙, 루트 노드에서 임의의 리프 노드에 이르는 경로에서 만나는 블랙 노드의 수는 모두 같음
* Hash Table
  * 해시 함수, 해시 값, 적재율(저장된 원소수/테이블 크기)
  * 충돌: 주소에 이미 다른 값이 존재
    * 체이닝: LL로 연결
    * 개방주소방법: 다음 빈자리에 들어 감. 추가 공간 허용 않음. 적재율 <= 1
      * 선형조사: 한 칸씩 이동해서 자리 찾음. 1차군집 발생
      * 이차원조사: 이차함수에 의해 넓혀가며 자리 찾음. 2차군집 발생
      * 더블해싱: 두 개의 함수를 사용. 
* 기타
  * LCS(Longest Common Subsequence)
  * LIS(Longest Increase Subsequence)
  * Levenshtein Distance: 편집 거리(↓: 삭제, ↘: 수정, →: 추가)

# 개발 방법론
* TDD
  * Junit
  * Spock
  * Unit 테스트
* DDD

# 전공기초
* OS
  * HA(High Availability): 클러스터링, 이중화, RAID 등의 방법이 있음
  * RAID 방식
    * 0: striping. 여러 디스크를 묶어서 하나처럼 사용
    * 1: mirroring. 같은 데이터를 여러 디스크에 저장
    * 5: striping + parity. Parity drive는 복구용 정보를 보관
* Network
  * 로드 밸런싱: L4, L7 스위치로 여러 서버로 고르게 분배
* DB
  * ACID
    * Atomicity: 성공하거나 실패
    * Consistency: 트랜잭션 방향은 한곳으로만. 무결성제약조건
    * Isolation: 한 트랜잭션 방해 받지 않음
    * Durability: 트랜잭션 이후 잘 반영
  * Isolation 단계
    * Read Uncommitted
      * SELECT 문장을 수행하는 경우 해당 데이터에 Shared Lock이 걸리지 않는 Level
      * 어떤 사용자가 A라는 데이터를 B라는 데이터로 변경하는 동안 다른 사용자는 B라는 아직 완료되지 않은(Uncommitted 혹은 Dirty) 데이터 B를 읽을 수 있음
    * Read Committed
      * SELECT 문장이 수행되는 동안 해당 데이터에 Shared Lock이 걸림
      * 어떠한 사용자가 A라는 데이터를 B라는 데이터로 변경하는 동안(commit 되기 전) 다른 사용자는 해당 데이터에 접근할 수 없음(대기 상태)
    * Repeatable Read
      * 트랜잭션이 완료될 때까지 SELECT 문장이 사용하는 모든 데이터에 Shared Lock이 걸리므로 다른 사용자는 그 영역에 해당되는 데이터에 대한 수정이 불가능
      * Select col1 from A where col1 between 1 and 10을 수행하였고 이 범위에 해당하는 데이터가 2건이 있는 경우(col1=1과 5) 다른 사용자가 col1이 1이나 5인 Row에 대한 UPDATE이 불가능합니다. 하지만, col1이 1과 5를 제외한 나머지 이 범위에 해당하는 Row를 INSERT하는 것이 가능
    * Serializable
      * 트랜잭션이 완료될 때까지 SELECT 문장이 사용하는 모든 데이터에 Shared Lock이 걸리므로 다른 사용자는 그 영역에 해당되는 데이터에 대한 수정 및 입력이 불가능
      * 완벽한 읽기 일관성 모드
  * Lock 세기
    * Shared Lock
      * Select를 할 때 발생
      * 다른 Shared Lock과는 호환, Exclusive Lock과는 호환불가
    * Exclusive Lock
      * 데이터 변경 시 발생
      * 이 Lock이 해제될 때까지 다른 트랜잭션은 해당  리소스 접근 불가
    * Update Lock
  * 블로킹과 교착상태
    * 블로킹: Lock 경합이 발생해 특정 세션이 작업을 진행하지 못하고 멈춤
    * S-Lock과 X-Lock은 함께 설정될 수 없어서 발생
    * 해결방법: Commit or Rollback
    * 최소화 방법: 트랜잭션을 짧게, 같은 데이터 갱신의 트랜잭션 동시 발생제거
  * Index
  * 조인
    * JOIN table2 ON 조건
    * Left Right Outer Join: Left혹은 Right가 기준(Null일수 없음)
    * Cross Join (Cartesian Product)
      ``` 
      SELECT ENO, ENAME, DNAME FROM EMP CROSS JOIN DEPT; 
      == SELECT ENO, ENAME, DNAME FROM EMP, DEPT;
      ```
  * 실행계획(plan): 쿼리가 동작하는 순서. 튜닝 위해 사용
    * 과정: Parse → Execute → Fetch
  * 힌트(hint): 특정 조건을 사용(메모리 사용량, 인덱스 사용유무 등)
  * 파티션(partition): 디비나 테이블을 일정 규칙으로 나누어서 관리.
  * Subquery (Inline View)
  * DB 확장 방법
    * Replication, Query Off Loading: Master(CDU)와 Slave(R)로 구성
    * 샤딩(Sharding): 물리적으로 다른 데이터베이스에 데이터를 수평 분할
      * 단점: 여러 DB대상으로 작업해야 하므로 Join, 일관성, 복제 등에 불리
      * 방식
        * 수평적: 종류별(ex. Korea, US, ..., China)
        * 수직적: 범위별(ex. 10대, 20대, ..., 80대)