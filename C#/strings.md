# 문자열 다루기

모든 프로그래밍언어엔 문자열이 있으며 모든 언어를 통틀어 가장 많이 사용되는 자료형 중 하나입니다.
`.NET Framework` 또한 강력한 문자열 기능들이 제공됩니다.
콘솔에서도 마찬가지지만 특히 `GUI` 프로그래밍에서의 문자열은 땔래야 땔 수 없는 존재입니다.
문자열을 다루는 기술은 반드시 익혀야하는 필수 기술입니다.

## 문자열이 뭔가요?

`C#`에서의 문자열은 `string`형식을 가진 자료입니다.

``` csharp
string my_string = "abcdefg";
```

가령, 위 코드에선 `my_string`이라는 `string`형 변수는 `abcdefg`라는 문자열을 담고 있는 변수입니다. 간단하죠?
문자열은 단어의 뜻과 같이 문자들로 이루어진 배열입니다. 여기서 문자는 `char`라는 자료형을 가지고 있습니다.

``` csharp
static void Main(string[] args)
{
    string myInput = Console.ReadLine();

    char first_ch = myInput[0];
}
```

위와 같이 `string`의 첫 글자를 `frist_ch`라는 문자형 변수에 넣을 수도 있습니다.

## 문자열 다듬기

`.NET Framework`는 문자열을 다루기 위한 많은 기능들을 제공해줍니다.
`C#`의 문자열 함수들은 대부분 `string` 클래스안에 구현이되어있습니다.
그 중에 가장 많이 쓰이는 기능들 먼저 소개해드릴께요.

### Split

거의 모든 언어에 있는 정석과도 같은 함수입니다.
이 함수는 어떤 구분자를 기준으로 문자열을 나누는 함수입니다.
C언어에 `strtok`이라는 함수와 조금 비슷합니다.
예제를 보시죠.

``` csharp
static void Main(string[] args)
{
    string path = "C:\\Windows\\notepad.exe";
    string[] split = path.Split('\\');

    string file_name = split[split.Length - 1];

    Console.Write(file_name);
    Console.Read();
}
```

`Split`함수를 통해 `\`문자를 기준으로 경로를 나눈 모습입니다.
`Split`는 이렇게 나눈 문자열들을 배열로 출력합니다. 이때 배열은 `string[]`이라는 형식을 가지고 있습니다.
그렇다면 위 코드의 `split`는 세 개의 요소 `C:`, `Windows`, `notepad.exe`를 가진 배열이 되겠네요.
또한, 배열에는 `Length`라는 `Property (속성)`이 있어 그 배열의 길이를 가져오는게 가능합니다.
위 코드에선 `split.Length - 1`이 `2`가 되므로, `notepad.exe`라는 문자열이 `file_name`의 값이 되겠죠.

`"C:\\Windows/notepad.exe"` 이런 식으로 구분자가 뒤죽박죽인 경우에도 `Split`는 여전히 유용합니다.

``` csharp
static void Main(string[] args)
{
    string path = "C:\\Windows/notepad.exe";
    string[] split = path.Split(new char[] { '\\', '/' });

    string file_name = split[split.Length - 1];

    Console.Write(file_name);
    Console.Read();
}
```

`Split`함수는 문자라는 구분자를 기준으로 문자열을 나누는 함수입니다.
구분자가 하나있든 여러개있든 상관없이 `Split`함수 입장에선 다 똑같은 구분자입니다.
그래서 위와 같이 두 개의 구분자를 같이 넣어주어도 상관없죠.

위 코드에서 `Split` 부분은 다음과 같이 쓸 수도 있습니다.

``` csharp
string[] split = path.Split(new[] { '\\', '/' });
```

이렇게 쓰거나, 더 간단하게

``` csharp
string[] split = path.Split('\\', '/');
```

이렇게도 가능하죠.

그렇다면, 문자가 아닌 문자열을 구분자로 사용하여 `Split`를 쓸 수는 없을까요?
다음 코드를 보시죠.

``` csharp
static void Main(string[] args)
{
    string path = "010--7722--2277";
    string[] split = path.Split(new[] { "--" }, StringSplitOptions.None);

    string mid_pnumber = split[1];

    Console.Write(mid_pnumber);
    Console.Read();
}
```

`Split`함수에는 `Split(params string[], StringSplitOptions)` 이라는 오버로딩 함수가 있습니다.
이 함수가 바로 문자열을 기준으로 `Split`를 수행하는 함수입니다.

### Replace

`Split`함수와 더불어 가장 많이 쓰이는 함수인 `Replace`함수입니다.
이름만 들어도 어떤 함수인지 감이오시죠?
사용법은 정말 간단합니다.

``` csharp
static void Main(string[] args)
{
    string path = "010--7722--2277";
    string p_number = path.Replace("--", "-");

    Console.Write(p_number);
    Console.Read();
}
```

`Replace(대상문자, 바꿀문자)`를 호출해주면 대상문자가 바꿀문자로 치환된 문자열이 생성됩니다.

### Trim

이 함수는 문자열 앞뒤의 선형 공백을 제거해주는 함수입니다.

``` csharp
static void Main(string[] args)
{
    string path = "   010-7722-2277   ";
    string p_number = path.Trim();

    Console.Write(p_number);
    Console.Read();
}
```

이렇게 문자열 앞이나 뒤에 공백이 있는 경우에 `Trim`함수를 통하여 공백을 제거할 수 있습니다.
앞의 공백만 지울 수 있는 `TrimStart`나, 뒤쪽 공백만 지울 수 있는 `TrimEnd`라는 함수도 제공합니다.

이 함수를 통해서 공백뿐만아니라 문자 집합도 제거할 수 있습니다.

``` csharp
static void Main(string[] args)
{
    string path = "<$<010-7722-2277>$>";
    string p_number = path.TrimStart('<', '$').TrimEnd('>', '$');

    // 또는

    string p_number = path.Trim('<', '$', '>');

    Console.Write(p_number);
    Console.Read();
}
```

`Split`함수의 입력방식과 동일합니다.

### PadLeft, PadRight

이 함수들은 `Trim`과는 다르게 공백이나 문자를 삽입하는 함수입니다.
그냥 삽입하는 것은 아니고, 문자열의 길이에 맞추어 삽입합니다.
다음은 `PadLeft` 함수의 예제입니다.

``` csharp
static void Main(string[] args)
{
    string text = "1:2:3:4";
    string p_number = text.PadLeft(10);

    Console.Write(p_number);
    Console.Read();
}
```

```
   1:2:3:4
```

이렇게 `PadLeft`함수는 문자열의 총 길이를 10으로 맞추게끔 문자열의 왼쪽에 공백을 삽입합니다.
문자열의 총 길이가 10보다 크면 아무동작도 하지않습니다.

다음은 `PadRight` 함수의 예제입니다.

``` csharp
static void Main(string[] args)
{
    string text = "1:2:3:4";
    string p_number = text.PadRight(10);

    Console.Write(p_number + ".");
    Console.Read();
}
```

```
1:2:3:4   .
```

마찬가지로 문자열의 총 길이를 10으로 맞추면서 오른쪽에 공백을 삽입합니다.

### Substring, Remove

`Substring`, `Remove` 이 두 함수도 문자열을 자르는 함수이지만, `Split`와는 쓰임새가 조금 다른 함수입니다.
예제부터 봅시다.

``` csharp
static void Main(string[] args)
{
    string text = "1:2:3:4";
    string p_number = text.Substring(2);
    
    Console.Write(p_number);
    Console.Read();
}
```

```
2:3:4
```

`Substring` 함수는 문자열의 시작부분을 다시 설정하는 함수입니다.
이 함수는 두 개의 오버로드를 가지고 있으며, 두 번째 오버로딩함수는 가져올 문자열의 길이를 설정합니다.

``` csharp
string p_number = text.Substring(2,2);
```

```
2:
```

`Remove`함수는 `Substring`과 반대로 동작하는 함수입니다.

``` csharp
static void Main(string[] args)
{
    string text = "1:2:3:4";
    string p_number = text.Remove(2);
    
    Console.Write(p_number);
    Console.Read();
}
```

```
1:
```

이 함수는 문자열의 끝 부분을 다시 설정하는 함수입니다.
이 함수 또한 두 개의 오버로드를 가지고 있고, 두 번째 오버로딩 함수는 삭제할 문자열의 길이를 같이 설정합니다.

``` csharp
string p_number = text.Remove(2,2);
```

```
1:3:4
```

## 문자열 매칭

위 함수들이 문자열을 다듬는 함수였다면 앞으로 소개할 함수들은 문자열을 변화시키지 않고, 문자열에 특정 문자열이 있는지 등을 검사할 때 쓰는 함수들 입니다.

### Contains

`Conatins` 함수는 문자열안에 특정 문자나 문자열이 포함되어 있는지를 검사합니다.

``` csharp
static void Main(string[] args)
{
    string text = "Carpe diem, quam minimum, credula postero.";

    if (text.Contains("diem"))
    {
        Console.Write("diem이 포함되어 있습니다!");
    }
    else
    {
        Console.Write("diem이 없네요");
    }
}
```

위 예제와 같이 특정 문자열에 문자열이나 문자가 들어있다면, `true`를, 들어있지 않다면 `false`를 반환합니다.

### IndexOf, LastIndexOf

`IndexOf`와 `LastIndexOf`는 `Contains`와 비슷합니다. 다만, 차이점은 `true`, `false`와 같이 `boolean`값을 반환하는 것이 아닌, 문자열의 위치를 반환한다는 점입니다. 문자열의 위치는 당연히 `0`부터 시작하는 값입니다. 만약, 만족시키는 특정 문자열이 문자열안에 없다면 `-1`를 반환합니다.

`IndexOf`는 처음 만나는 문자열의 위치를 가져옵니다.

``` csharp
static void Main(string[] args)
{
    string text = "Carpe diem, quam minimum, credula postero.";

    Console.Write($"{text.IndexOf("diem")}");
}
```

```
6
```

`LastIndexOf`는 이와 반대로 마지막으로 만나는 문자열의 위치를 가져옵니다.

### StartsWith, EndsWith

이 함수들은 문자열의 시작부분과 끝부분의 일치여부를 검사하는 함수입니다.
예제를 보세요!

``` csharp
static void Main(string[] args)
{
    string text = "https://www.youtube.com/watch?v=d8NIN6DRj6I";

    if (text.StartsWith("http://") || text.StartsWith("https://"))
    {
        Console.Write("HTTP 형식입니다.");
    }
    else
    {
        Console.Write("옳바른 HTTP 형식이 아닙니다.");
    }
}
```

`StartsWith`함수는 위와 같이 문자열의 첫 부분부터 일치하는 지의 여부를 검사하는 함수입니다.

`EndsWith`는 그 반대로 뒷 부분부터 일치하는 지의 여부를 검사하는 함수입니다.

``` csharp
static void Main(string[] args)
{
    string text = @"C:\Windows\regedit.exe";

    if (text.EndsWith(".exe") || text.EndsWith(".sys") || text.EndsWith(".dll"))
    {
        Console.Write("실행파일 형식입니다.");
    }
    else
    {
        Console.Write("옳바른 실행파일 형식이 아닙니다.");
    }
}
```

## ToString

`ToString`함수는 어떤 `object`를 `string`형식으로 바꿔주는 함수입니다.
이 함수는 `object` 클래스에 포함되어 있으며, 하위 클래스들이 오버라이드하고 있습니다.
`ToString`함수는 문자열로 바꾸어줄 뿐만아니라 특정 형식도 지정할 수 있습니다.

다음은 `ToString` 함수를 이용해 문자열 형식을 지정하는 예제입니다.

``` csharp
static void Main(string[] args)
{
    Console.Write(123456789.ToString("#,#"));
}
```

```
123,456,789
```

`ToString` 문법은 `printf` 만큼 복잡해서 링크로 대체합니다.

https://docs.microsoft.com/ko-kr/dotnet/standard/base-types/standard-numeric-format-strings

https://docs.microsoft.com/ko-kr/dotnet/standard/base-types/custom-numeric-format-strings