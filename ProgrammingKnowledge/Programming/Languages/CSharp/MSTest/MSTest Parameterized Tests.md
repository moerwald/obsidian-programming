Mit `DataRow` kann man einfache Datentypen als Testparameter verwenden.

```csharp
```c#
[TestMethod]
[DataRow("1900-01-01", false, DisplayName = "Year divisible by 4 and 100, but not 400")]
[DataRow("2000-01-01", true, DisplayName = "Year divisible by 4, 100, and 400")]
[DataRow("2019-01-01", false, DisplayName = "Year not divisible by 4")]
[DataRow("2020-01-01", true, DisplayName = "Year divisible by 4, but not 100 or 400")]
public void TestLeapYearHelper(string dateInput, bool expectedValue)
{
    var date = new DateTime(dateInput);

    var isLeapYear = date.IsLeapYear();

    Assert.AreEqual(expectedValue, isLeapYear);
}
```

Um komplexe Datentypen als Parameter zu verwenden gibt es zwei Möglichkeiten.

1.  [Dynamic Data Attribut](https://www.mmp.dev/articles/2019-11-09-DynamicData/): Ähnlich zu NUnits `TestCaseSource` Attribut.
2. [ITestDataSource](https://www.meziantou.net/mstest-v2-data-tests.htm): Basierend auf dem Interface kann ein eigenes Attribut definiert werden.


### Dynamic Data

```csharp

[TestClass]
public class MathTests
{
    [DataTestMethod]
    [DynamicData(nameof(Data), DynamicDataSourceType.Property)]
    public void Test_Add_DynamicData_Property(int a, int b, int expected)
    {
        var actual = MathHelper.Add(a, b);
        Assert.AreEqual(expected, actual);
    }

    public static IEnumerable<object[]> Data
    {
        get
        {
            yield return new object[] { 1, 1, 2 };
            yield return new object[] { 12, 30, 42 };
            yield return new object[] { 14, 1, 15 };
        }
    }
}

```


### ITestDataSource

```csharp
public class CustomDataSourceAttribute : Attribute, ITestDataSource
{
    public IEnumerable<object[]> GetData(MethodInfo methodInfo)
    {
        yield return new object[] { 1, 1, 2 };
        yield return new object[] { 12, 30, 42 };
        yield return new object[] { 14, 1, 15 };
    }

    public string GetDisplayName(MethodInfo methodInfo, object[] data)
    {
        if (data != null)
            return string.Format(CultureInfo.CurrentCulture, "Custom - {0} ({1})", methodInfo.Name, string.Join(",", data));

        return null;
    }
}


[DataTestMethod]
[CustomDataSource]
public void Test_Add(int a, int b, int expected)
{
    var actual = MathHelper.Add(a, b);
    Assert.AreEqual(expected, actual);
}
```




#MsTest