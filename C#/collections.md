# 컬렉션

https://docs.microsoft.com/ko-kr/dotnet/csharp/programming-guide/concepts/collections

## 반복자 (Enumerator)

`C#`에선 Iterator라는 이름대신 Enumerator라는 이름으로 구현되어 있습니다.

반복자가 사용되는 한 예로, `foreach` 키워드는 컴파일 타임에 `GetEnumerator`를 호출하여 `Enumerator`를 가져옵니다.
이로 인해 `foreach`로 열거가능한 모든 컬랙션들은 `IEnumerator`라는 인터페이스를 상속받습니다.

다음은 `IEnumerator`의 구현부입니다.

``` csharp
// https://referencesource.microsoft.com/#mscorlib/system/collections/ienumerator.cs
public interface IEnumerator
{
    // Interfaces are not serializable
    // Advances the enumerator to the next element of the enumeration and
    // returns a boolean indicating whether an element is available. Upon
    // creation, an enumerator is conceptually positioned before the first
    // element of the enumeration, and the first call to MoveNext 
    // brings the first element of the enumeration into view.
    // 
    bool MoveNext();

    // Returns the current element of the enumeration. The returned value is
    // undefined before the first call to MoveNext and following a
    // call to MoveNext that returned false. Multiple calls to
    // GetCurrent with no intervening calls to MoveNext 
    // will return the same object.
    // 
    Object Current {
        get; 
    }

    // Resets the enumerator to the beginning of the enumeration, starting over.
    // The preferred behavior for Reset is to return the exact same enumeration.
    // This means if you modify the underlying collection then call Reset, your
    // IEnumerator will be invalid, just as it would have been if you had called
    // MoveNext or Current.
    //
    void Reset();
}
```

## ArrayList

``` csharp
public void foo()
{
    ArrayList list = new ArrayList();
    list.Add("asdf");
    list.Add(65535);
    list.Add('a');
}
```

`ArrayList`는 어떤 자료형이든 담을 수 있는 리스트 클래스입니다.
어떤 자료형이든 담을 수 있지만 내부적으로 박싱, 언박싱으로 인한 IO 딜레이가 커질 수 있어
ArrayList를 사용하는 것은 특별한 상황이 아니라면 좋은 방법이 아닙니다.

## List

``` csharp
public void foo()
{
    List<string> list = new List<string>();

    list.Add("asdf");
    list.Add("qwerty");
    list.Add("zxcva");

    foreach (var str in list)
        Console.WriteLine(str);
}
```

`List<>` 클래스는 Generic한 List 구현입니다.
`ArrayList`와는 달리 지정된 자료형만 담을 수 있지만, 성능은 매우 좋은 편입니다.

내부적인 구현은 일반적인 동적 리스트 구현과는 달리 `Add` 호출 때마다 이전 크기의 두 배에 해당하는 크기를 할당합니다.

리스트 소스코드 : https://referencesource.microsoft.com/#mscorlib/system/collections/generic/list.cs

자주 쓰이는 메서드는 다음과 같습니다.

### Contains

어떤 요소가 리스트안에 있는지 검사합니다.
완전탐색으로 0 인덱스부터 검사하므로 매우 느립니다.

### BinarySearch

리스트가 정렬되어 있는 상태라면 `BinarySearch`를 사용해 원하는 요소를 빠르게 탐색할 수 있습니다.

### Sort

지정된 Comparer로 리스트를 정렬합니다.

가령, 다음 코드는 문자열 리스트를 문자열 길이 오름차순으로 정렬합니다.

``` csharp
list.Sort((x, y) => x.Length.CompareTo(y.Length));
```

## Hashtable

## HashSet

``` csharp
public void foo()
{
    HashSet<int> set = new HashSet<int>();

    Random rand = new Random();
    for (int i = 0; i < 100; i++)
        set.Add(rand.Next() % 100);

    for (int i = 0; i < 100; i++) {
        int next = rand.Next() % 100;
        if (set.Contains(next))
            Console.WriteLine(next);
    }
}
```

`HashSet`는 중복된 값들을 검사할 때 매우 유용하게 사용할 수 있는 컬랙션입니다.
정렬되지 않은 `List`의 `Contains`를 사용할 때보다 빠릅니다.

## Dictionary
