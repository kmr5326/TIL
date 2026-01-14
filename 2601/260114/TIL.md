# Call By Value와 Call By Reference
값에 의한 호출(Call By Value) 은 메서드를 호출할 때, 값 자체를 넘겨주는 방식입니다. 메서드를 호출하는 함수의 변수와 호출된 함수의 파라미터는 서로 다른 변수입니다.

참조에 의한 호출은(Call By Reference) 는 메서드를 호출할 때, 참조를 직접 전달하는 방식입니다. 참조를 직접 전달하기 때문에 호출하는 함수의 변수와 호출된 함수의 파라미터는 동일한 변수입니다.

java는 값에 의한 호출(Call By Value)만 존재합니다.
호출자 변수와 수신자 파라미터는 Stack 영역 내에서 각각 독립적으로 존재하는 다른 변수입니다.

```java
public class CallByExampleTest {     
    @Test    
    void referenceTest() {        
    int[] arr = { 10 }; // 0x001                
    newArr(arr);         
    assertThat(arr).isEqualTo("0x001");    
    }     

    void newArr(int[] arrArg) {        
    arrArg = new int[]{ 20 }; // 0x002    
    }
}

```