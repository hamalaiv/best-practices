# Best practises

This is a collection of best practises I have learned and figured out during my 10+ years of programmin. Beware that some of them might be highly opinionated.

// TODO: Work in progress

## Programmin, common

### Return early on exception conditions

In most cases the code becomes more readable and easier to maintain when you return early on exception cases.

```
if (condition1 == null)
{
    return default;
}

if (condition2 == null)
{
    return default;
}

...

return result;
```


### Use parametrisized tests

In C# XUnit it would look like this:
```
[InlineData(true, "test1")]
[InlineData(false, "test2")]
public void TestFunction(bool param1, string param2)
{
    ...
}
```

In typescript jest it would look like this:
```
const testCases = [
    {
        param1: true,
        param2: "test1"
    },
    {
        param1: false,
        param2: "test2"
    }];

testCases.forEach(testCase => {
    it(`Should test with param1 ${testCase.param1} and param2 ${testCase.param2}` () =>
    {
        ...
    });
});
```

## EF Core

### Performace

- Use `IQueryable` as long as possible before converting to IEnumerable
- Use `AsNoTracking` when possible
- Use cancellation token for the query in web requests (especially big queries)
- Use pagination
- Avoid cartesian explosion with `AsSplitQuery`
- Use `ExecuteUpdate` and `ExecuteDelete` if possible (especially on big updates/deletes)
- When performance is an issue use `Select` for individual fields instead of `Include`

#### References

- [Microsoft learn](https://learn.microsoft.com/en-us/ef/core/performance/efficient-querying)
- [ND Conference talk by Jernej Kavka](https://youtu.be/oE8lEP4mKjk?si=SSNkvrYmE_ALVlUa)
