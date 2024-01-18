# Code specific design patterns
Here we will take a look at some design patterns used when writing code, sure some of these are used outside of code (E.x Proxy) but this file just refers to code specific patterns. Also we will not be covering all of them just the ones which I find myself implementing or interacting with daily. These can be split into the following subgroups.

## Creational Patterns
Creational patterns refer to how we create certain objects for example instantiating an object for later use.

### Factory
One of the first goals of the factory method is to hide all the logic around creating an object of a specific type. Instead we should call a function from a predefined interface which generates this object for us.

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

### Singleton

