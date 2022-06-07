# study

1. ClassLoader

Background
- Java는 Complier, Interpreter 모두 존재
- java source(.java) 파일을 Complie하여 byte code(.class)로 변환
- byte code는 JIT Compile하여 Native  code로 변환 & 캐싱. Interpreter로 run-time에 실행
- JVM는 RuntimeArea( Method Area, Stack, Heap...), ExecutionEngine( JIT, Interpreter ), GC( Eden, Survivor, Permernant )로 구성

ClassLoader는?
- .class 파일을 Method Area(class, static)로 동적으로 load하는 모듈
- 왜 동적인가? JVM은 클래스 파일을 참조하는 순간 동적으로 메모리에 Load & Link시킨다
- Loading, Linking, Initializing 3가지 단계를 거쳐 JVM에서 사용가능

Class Load 종류
- Load Time Dynamic Loading : 하나의 클래스를 로드하면서 필요한 다른 클래스를 한번에 로딩한다 (import 문)

public class HelloWorld {
     public static void main(String[] args) {
        System.out.println("안녕하세요!");
     }
 }
부트스트랩 클래스 로더가 생성된 후 
로드되는 클래스는 Object, HelloWorld, String, System

- Run Time Dynamic Loading : ClassLoader.forName(String className)
Class klass = Class.forName("java.lang.String");
Object obj = klass.newInstance();

Bootstrap ClassLoader
- 가장 기본적인 클래스로더.
- jre/lib/rt.jar

Extension ClassLoader
- jre/lib/ext

Application ClassLoader
- "-classpath" 옵션 내에 있는 모든 클래스

ClassLoader 특징
- Delegation 클래스 로딩을 상위 클래스 로더에게 위임
- Visibility 상위 클래스로더는 좀 더 보편적인 클래스를 알고있도록
- Uniqueness 한번 로드한 클래스는 다른 클래스로더에 의해 로드되지 않도록
- 캐시 사용가능

ClassLoader를 사용할 일이 있는가?
- Network, External Path 등의 외부 클래스 로드가 필요할 때.
- 메모리 관리를 위해 동적으로 클래스를 로드할 필요가 있는경우

논의
- Application 사이에서 클래스를 전송할 일이 있는가?
- 약속되지 않은 객체를 전송하는 경우, 이를 위해 사용 가능할까?

2. Serializable

public interface Serializable {
}

- 객체직렬화를 위한 인터페이스
