# Type 완벽히 다루기!

런타임때 변수를 수정하고 함수를 호출하는 방법들에 대해 알아봅시다!

이게 뭔 소리냐구요? 그냥 지금부터 알아보죠!

## Type?

`object`를 상속받는 모든 클래스의 인스턴스는 `GetType`함수를 통해 `Type` 정보를 가져올 수 있습니다. 클래스의 인스턴스의 `Type`이니 클래스 선언부에 대한 내용을 담고 있겠죠?

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

        my_controller.Print(my_controller.GetType().ToString());
        my_controller.Print(args.GetType().ToString());
    }
}
```

```
1: ConsoleApp1.ConsoleController
2: System.String[]
```

`ConsoleApp1`은 프로젝트 이름에 따라 다르게 출력될껍니다.

위 예제를 보면 클래스의 선언부를 `namespace` 정보와 함께 가져오는 모습을 볼 수 있습니다.

## 필드 열거

`Type` 클래스에는 `GetFields`라는 함수가 있습니다.
`GetFields`를 통해 필드의 정보를 가져올 수 있습니다.

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

        BindingFlags DefaultBinding = BindingFlags.NonPublic |
                     BindingFlags.Instance | BindingFlags.IgnoreCase | BindingFlags.Public | BindingFlags.FlattenHierarchy;

        foreach (var field in my_controller.GetType().GetFields(DefaultBinding))
        {
            my_controller.Print(field.ToString());
        }
    }
}
```

```
1: Int32 line_number
```

`BindingFlags`는 필드 속성의 필터역할을 해준다고 볼 수 있습니다.

## 필드 값 가져오기

``` csharp
static void Main(string[] args)
{
    ConsoleController my_controller = new ConsoleController();

    BindingFlags DefaultBinding = BindingFlags.NonPublic |
                 BindingFlags.Instance | BindingFlags.IgnoreCase | BindingFlags.Public | BindingFlags.FlattenHierarchy;

    my_controller.Print("first");
    my_controller.Print("second");
    my_controller.Print("third");


    foreach (var field in my_controller.GetType().GetFields(DefaultBinding))
    {
        my_controller.Print(field.GetValue(my_controller).ToString());
    }
}
```

```
1: first
2: second
3: third
4: 3
```
