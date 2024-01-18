# Code specific design patterns
In this guide, we’ll look at some design patterns used in coding. Some of these patterns are also used outside of coding (like Proxy), but this guide focuses on their use in code. We’ll only cover the ones that are commonly used or interacted with on a daily basis. These patterns can be divided into several subgroups.

## Creational Patterns
Creational patterns deal with object creation mechanisms, trying to create suitable objects for a situation.

### Factory
The main idea of the factory method is to provide a way to delegate the instantiation logic to child classes. We should use a function from a predefined interface to create the object for us.

```c#

public interface IBall
{
    string GetBallType();
}

public interface IFactory
{
    IBall GenerateBall(string type);
}

public class BallFactory : IFactory
{
    public IBall GenerateBall(string type)
    {
        switch (type)
        {
            case "Football":
                return new Football();
            case "Basketball":
                return new Basketball();
            default:
                throw new Exception("Invalid type");
        }
    }
}


```

This allows us to just use the Factory to hide the creation logic in a seperate class

### Builder
The Builder pattern shines when you’re constructing an object that requires various configuration options. In the example below, we’ve encapsulated most of the configuration associated with the keywords ‘select’, ‘from’, and ‘where’. This encapsulation leads to a more readable and adaptable approach when crafting complex objects.


```c#

var queryBuilder = new SqlQueryBuilder();
string query = queryBuilder.
                    Select("*"
                    .From("Employees")
                    .Where("Salary > 50000").Build();


public class SqlQueryBuilder
{
    private string _query;

    public SqlQueryBuilder Select(string column)
    {
        _query += $"SELECT {column} ";
        return this;
    }

    public SqlQueryBuilder From(string table)
    {
        _query += $"FROM {table} ";
        return this;
    }

    public SqlQueryBuilder Where(string condition)
    {
        _query += $"WHERE {condition} ";
        return this;
    }

    public string Build()
    {
        return _query.TrimEnd() + ";";
    }
}


```

### Singleton

