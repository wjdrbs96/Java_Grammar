## `인터페이스 특징`

```
모든 멤버 변수는 public static final 이어야 하며, 이를 생략할 수 있다. 
모든 메소드는 public abstract 이어야 하며, 이를 생략할 수 있다. (단, static 메소드와 default 메소드는 예외)
```

<br>

## 인터페이스 default Method, static Method

자바 8버전부터 추가된 `inferface` 기능에 대해서 알아보자.

<br>

### default method

```java
public interface Foo {
    
    void printName();  // 인터페이스 내부 추상메소드는 모두 public
}


class defaultFoo implements Foo {

    @Override
    public void printName() {
        
    }
}
```

위와 같이 `Foo` 인터페이스와 이것을 구현하는 `defaultFoot` 클래스가 존재하는 상황이다. `printName()` 메소드는 추상메소드이기 때문에
구현 클래스에서 반드시 `오버라이딩` 해야한다. 그런데 만약에 `Foo`를 구현하는 클래스가 여러개인데 공통적인 메소드 하나가 필요해서 `Foo`에 추상메소드를
하나 추가한다고 가정해보자.

<br>

그러면 `Foo`를 구현하고 있는 모든 클래스에 추가된 `추상메소드`를 추가해야 한다. 따라서 이럴 때 사용할 수 있게 자바 8버전부터 나온 것이
`default Method`이다.

<br>

```java
public interface Foo {

    void printName();

    default void printNameUpperCase() {
        System.out.println("Foo");
    }
}
```

위와 같이 `default` 메소드를 사용하면 `inferface` 내부에서도 클래스의 구현체를 만들 수 있게 된다.

<br>

그리고 `default Method`는 `Object`가 제공하는 메소드인 `hashCode, equals` 등등은 사용할 수 없다. 예를들면 아래와 같다.

```java
public interface Foo {

    void printName();

    // 컴파일 에러
    default String toString() {
        
    }
}
```

`toString()`도 `Object` 메소드이기 때문에 `default`메소드로 선언할 수 없다. (하지만 추상메소드로는 구현할 수 있다.)


<br>

그리고 또 다른 예제를 봐보자.

```java
public interface Foo {

    default void printName() {
        System.out.println("Foo");
    }
}
```

```java
public interface Bar extends Foo {

    void printName();
}
```

위와 같이 `Foo` 인터페이스를 구현한 `Bar` 인터페이스가 있다고 가정하자. 이 때 Foo 인터페이스에 `default` 메소드가 존재하는데 
이것을 `Bar` 인터페이스에서는 다르게 사용하고 싶다면 위와 같이 `printName()`메소드를 추상메소드로 선언하여 `Bar`를 구현하는 클래스에서
`오버라이딩`해서 사용하면 된다. 

<br>


### 다중 상속

```java
public interface Foo {

    default void printName() {
        System.out.println("Foo");
    }
}
```

```java
public interface Bar {

    default void printName() {
        System.out.println("BAR");
    }
}
```

위와 같이 `Foo`인터페이스와 `Bar`인터페이스 내부에 둘다 `printName()`이라는 `default method`가 존재한다고 가정해보자.

> 인터페이스는 인터페이스로부터만 상속받을 수 있으며, 클래스와는 달리 다중상속, 즉 여러 개의 인터페이스로부터 상속을 받는 것이 가능하다.
>
> '자바도 인터페이스를 이용하면 다중상속이 가능하다' 라고 하는 것일 뿐 자바에서 인터페이스로 다중 상속을 구현하는 경우는 거의 없다. 

<br>

```java
public class Test implements Foo, Bar {

}
```

그리고 위와 같이 `Test`클래스에 `Foo`, `Bar`인터페이스를 모두 구현했을 때, `Test`클래스는 누구의 `default Method`를 사용하게 될까?
정답은 `컴파일에러`이다. 컴파일에러를 피하기 위해서는 `printName()`메소드를 Test 클래스 내부에서 `오버라이딩`해서 사용해야 한다.

<br>

### static method

```java
public interface Foo {

    static void printAnyThing() {
        System.out.println("Foo");
    }
}
```
```java
public class Test {
    public static void main(String[] args) {
        Foo.printAnyThing();
    }
}
```

인터페이스 내부에 `static method`를 선언하면 일반적인 `static method`처럼 사용할 수 있다. (인터페이스의 static 메소드의 접근 제어자는 항상 public 이다.)


<br>

### `Iterable` 기본메소드

* `forEach()` 메소드

forEach() 메소드는 이름으로 알 수 있듯이 for문의 역할을 하는데 인자로 `Consumer` 타입을 받는 메소드이다.

```java
import java.util.ArrayList;
import java.util.List;

public class Test {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>();
        list.add("gyun");
        list.add("hyunwoo");
        list.add("bobae");
        list.add("toby");

        list.forEach((s) -> System.out.println(s));  // 아래 줄 처럼 줄여서 쓰기 가능
        list.forEach(System.out::println);   
    }
}
```

`Iterable` 인터페이스에 `default` 메소드로 정의되어 있는 `forEach()` 메소드를 위와 같이 편리하게 사용할 수 있다.

<br>

* `spliterator()` 메소드

spliterator() 메소드는 `Iterable` 인터페이스 있는 `default` 메소드이다. 메소드 역할은 `iterator()` 메소드에 `split()`기능만 추가된 것이라고
생각하면 된다.


```java
import java.util.ArrayList;
import java.util.List;
import java.util.Spliterator;

public class Test {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>();
        list.add("gyun");
        list.add("hyunwoo");
        list.add("bobae");
        list.add("toby");

        Spliterator<String> spliterator = list.spliterator();
        Spliterator<String> stringSpliterator = spliterator.trySplit();
        while (spliterator.tryAdvance(System.out::println));
        System.out.println("=================");
        while (stringSpliterator.tryAdvance(System.out::println));
    }
}
```

```
bobae
toby
=================
gyun
hyunwoo
```

그래서 위와 같이 `tryAdvance()` 메소드를 사용하면 `Iterable` 메소드의 `hasNext()`와 같은 역할이고 `trySplit()`을 하면 쪼개는 메소드이다. 따라서 결과도 위와 같이 나오는 것도 확인할 수 있다.