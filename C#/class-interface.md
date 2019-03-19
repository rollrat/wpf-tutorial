# 클래스와 인터페이스

`C++`에서 클래스를 다뤄보셨던 분이라면 `C#`에서의 클래스도 쉽게 이해할 수 있습니다.
클래스는 데이터와 데이터를 다루는 함수들의 집합을 말합니다.

## 클래스

``` csharp
class Program
{
    static void Main(string[] args)
    {
        Console.WriteLine("Hello World!");
    }
}
```

지금까지 우리도 클래스를 사용하고 있었다는 사실을 눈치채셨나요?
`Console Application`의 경우 `Program`클래스의 `Main`함수가 프로그램의 진입점이 됩니다.
`C`나 `C++`의 `main`함수와 같은 의미죠.
`C#`에선 `C++`에서와는 다르게 클래스 바깥에, 즉 전역함수를 정의할 수 없습니다.
무조건 클래스 내부에서만 작성할 수 있습니다.
따라서, `C#`에선 클래스가 매우 중요합니다.

클래스를 선언하는 방법은 간단합니다.

``` csharp
class MyClass
{
    public void Print(string message)
    {
        Console.WriteLine(message);
    }
}
```

함수의 안쪽이 아니고, 네임스페이스의 바깥쪽이 아니라면, 어디에서라도 클래스를 선언할 수 있습니다.
그래서 클래스 안에서도 선언이 가능하죠!

### 클래스와 인스턴스

https://social.msdn.microsoft.com/Forums/vstudio/en-US/fa92d20f-06e9-443d-b594-72b48c86c16b/what-is-difference-between-an-instance-and-object-of-a-class?forum=csharpgeneral

클래스는 그 자체만으로도 고귀한 존재입니다. 한 번 선언하면 절때 바뀌지 않거든요.
하지만 인스턴스는 다릅니다. 인스턴스는 클래스를 다루기위한 또 다른 데이터들일 뿐이죠.
적개는 수개, 많게는 수만개가 클래스의 인스턴스로 존재할 수 있습니다.
그렇다고 인스턴스가 의미없는 존재란 것은 아닙니다.

클래스는 그 자체만으로도 고귀한 존재입니다. 하지만, 클래스 혼자서는 할 수 있는게 없습니다.
인스턴스가 있어야 제대로된 기능들을 수행할 수 있죠.
일반적으로 인스턴스가 없다면 클래스를 다룰 수가 없습니다.
다음 예제를 보시죠.

``` csharp
class ConsoleController
{
    private int line_number = 0;
    public void Print(string message)
    {
        line_number += 1;
        Console.WriteLine($"{line_number}: {message}");
    }
}

class Program
{
    static void Main(string[] args)
    {
        ConsoleController my_controller = new ConsoleController();

        my_controller.Print("Hello World!");
        my_controller.Print("My name is Koromo!");
    }
}
```

`ConsoleController` 클래스는 `line_number`라는 변수와, `Print`라는 함수를 포함하고 있습니다.
이 클래스를 이용하기 위해선 `new <class>` 구문을 통한 인스턴스 생성과정이 필요합니다.
`my_controller` 변수는 `new ConsoleController`를 통해 `ConsoleController` 클래스의 인스턴스를 가지므로, `my_controller`는 `ConsoleController`의 인스턴스가 됩니다.

이제 클래스를 다루기위한 인스턴스가 생겼으니 마음껏 인스턴스를 다뤄보세요!

## 클래스의 구성요소

### 필드

필드는 클래스 내부에 선언된 변수를 말합니다.

### 메서드

메서드는 클래스 내부에 정의된 함수를 말합니다.

### 프로퍼티

프로퍼티는 은닉화의 구현체입니다.

## 제너릭

`C++`를 배우셨던 분이라면, `template`에 익숙하실 겁니다.
`C++`의 `template`과 같이 한 번의 클래스 선언으로 여러 타입을 취하는 클래스의 기능을 제너릭이라합니다.

## 인터페이스 (interface)

## 추상 클래스 (abstract class)

## 전역 클래스 (static class)



## internal 클래스

`internal` 클래스는 해당 바이너리가 아닌 외부에서의 접근을 막는 키워드입니다.
`internal` 클래스가 선언되면 바이너리 어디서든 해당 클래스의 메서드를 호출할 수 있습니다.