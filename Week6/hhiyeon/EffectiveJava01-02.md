### 📌 1장 : 들어가기
- 컴포넌트 : 개별 메서드부터 여러 패키지로 이뤄진 복잡한 프레임워크까지 재사용 가능한 모든 소프트웨어 요소
- 자바 자료형(type) 
  - 참조 타입(reference type) : 인터페이스, 클래스, 배열
  - 기본 타입(primitive type)
- annotation : 인터페이스의 일종
- enum : 클래스의 일종
---
### 📌 2장 : 객체 생성과 파괴
#### 아이템 1. 생성자 대신 정적 팩터리 메서드를 고려하라
- 생성자 : 클라이언트가 클래스의 인스턴스를 얻는 수단
- 클래스는 생성자 대신에 정적 팩토리 메소드(static factory method)를 제공할 수 있다.
- 정적 팩토리 메소드의 장점
  1. 이름을 가질 수 있다.
     - 생성자보다 객체의 특성을 이름으로 묘사할 수 있다.
  2. 호출될 때마다 인스턴스를 새로 생성하지 않아도 된다.
     - 인스턴스 통제 클래스 : 반복되는 요청에 같은 객체를 반환하는 식으로 정적 팩토리 방식의 클래스는 언제 어느 인스턴스를 살아 있게 할지 통제할 수 있다.
     - 인스턴스를 통제하면, 클래스를 싱글톤 패턴 or 인스턴스화 불가로 만들 수 있다.
     - 또한, 불변 값 클래스에서 동치 인스턴스가 단 하나임을 보장할 수 있다.
     - ex. a == b 일 때, a.equals(b)가 성립
  3. 반환 타입의 하위 타입 객체를 반화할 수 있는 능력이 있다.
     - 구현 클래스를 공개하지 않아도, 그 객체를 반환할 수 있어 API 생성을 할 때 작게 유지 가능하다.
  4. 입력 매개변수에 따라 매번 다른 클래스의 객체를 반환할 수 있다.
  5. 정적 팩토리 메소드를 작성하는 시점에는 반환할 객체의 클래스가 존재하지 않아도 된다.
     - 서비스 제공자 프레임워크 3개의 핵심 컴포넌트
       - 서비스 인터페이스(service interface) : 구현체의 동작을 정의
       - 제공자 등록 API(provider registration API) : 제공자가 구현체를 등록할 때 사용
       - 서비스 접근 API(service access API) : 클라이언트가 서비스의 인스턴스를 얻을 때 사용
     - 종종 서비스 제공자 인터페이스(service provider interface)라는 네 번째 컴포넌트도 쓰인다.
       - 서비스 인터페이스의 인스턴스를 생성하는 팩토리 객체를 설명해준다.
     - ex. JDBC 
       - 서비스 인터페이스 : Connection
       - 제공자 등록 API : DriverManager.registerDriver
       - 서비스 접근 API : DriverManager.getConnection
       - 서비스 제공자 인터페이스 : Driver
- 정적 팩토리 메소드 패턴의 단점
  1. 상속을 하려면 public, protected 생성자가 필요하다. 정적 팩토리 메소드만 제공하면 하위 클래스를 만들 수 없다.
  2. 정적 팩토리 메소드는 프로그래머가 찾기 어렵다.
     - 알려진 규약을 따라 이름을 짓는 것으로 문제점을 완화한다.
     - from : 매개 변수를 하나 받아서 해당 타입의 인스턴스를 반환하는 형변환 메소드<br> `Date d = Date.from(instant);`
     - of : 여러 매개변수를 받아 적합한 타입의 인스턴스를 반환하는 집계 메소드<br> `Set<Rank> faceCards = EnumSet.of(JACK, QUEEN, KING);`
     - valueOf : from과 of의 자세한 버전<br> `BigInteger prime = BingInteger.valueOf(Integer.MAX_VALUE);`
     - instance 혹은 getInstance : (매개 변수를 받으면) 매개 변수로 명시한 인스턴스를 반환하지만, 같은 인스턴스임을 보장하지 않는다.<br> `StackWalker luke = StackWalker.getInstance(options);`
     - create 혹은 newInstance : instance, getInstance 와 같지만 매번 새로운 인스턴스를 생성해 반환한다.<br> `Object newArray = Array.newInstance(classObject, arrayLen);`
     - getType : getInstance 와 같지만, 생성할 클래스가 아닌 다른 클래스에 팩토리 메소드를 정의할 때 쓴다.<br> `FileStore fs = Files.getFilesStore(path);`
     - newType : newInstance 와 같지만, 생성할 클래스가 아닌 다른 클래스에 팩토리 메소드를 정의할 때 쓴다.<br> `BufferReader br = Files.newBufferReader(path);`
     - type : getType 과 newType 의 간결한 버전<br> `List<Complaint> litany = Collections.list(legacyLitany);`
---
#### 아이템 2. 생성자에 매개변수가 많다면 빌더를 고려하라

---
#### 아이템 3. private 생성자나 열거 타입으로 싱글턴임을 보증하라


---

