# JVM
자바 프로그램 실행환경을 만들어 주는 소프트웨어이다.

1. 자바 프로그램 실행하면 JVM은 OS로부터 메모리를 할당받는다.
2. 자바 컴파일러(javac)가 자바 소스코드(.java)를 자바 바이트코드(.class)로 컴파일한다.
3. Class loader는 동적 로딩을 통해 필요한 클래스들을 Runtime Data Area에 올린다.
4. Runtime Data Area에 로딩 된 바이트 코드는 Execution Engine을 통해 해석된다.
5. Execution Engine에 의해 Garbage collector 작동과 Thread 동기화가 이루어진다.

# Garbage Collection
JVM의 힙 영역에서 필요 없게 된 Garbage를 JVM의 Garbage Collector가 불필요한 메모리를 알아서 정리해준다.

- Young 영역
  - 새롭게 생성된 객체가 할당되는 영역
  - young 영역에 대한 가비지 컬렉션을 Minor GC라고 부른다
- Old 영역
  - Young영역에서 살아남은 객체가 복사되는 영역
  - Young영역보다 크게 할당되며, 영역의 크기가 큰 만큼 가비지는 적게 발생한다.
  - Major GC 또는 Full GC라고 부른다.

Stop The World: JVM이 애플리케이션의 실행을 멈추고, GC를 실행하는 쓰레드 제외한 모든 쓰레드들의 작업이 중단되고 GC가 완료되면 작업 재개

Mark and Sweep: 사용되고 있는 메모리를 식별하는 과정을 Mark, Mark 되지 않은 객체들을 제거하는 과정을 Sweep

- Minor GC
  - Eden 영역: 새로 생성된 객체가 할당되는 영역
  - Survivor 영역: 최소 1번의 GC 이후 살아남은 객체가 존재하는 영역
- Major GC: Old 영역의 메모리가 부족해지면 실행