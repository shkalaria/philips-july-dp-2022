Refactor Below Code and remove code pollution

``` c#
public class ConcreteCalculator : ICalculator
{
    public int Add(int x, int y)
    {
        Print("Add(x={0}, y={1})", x, y);

        var addition = x + y;

        Print("result={0}", addition);

        return addition;
    }
}
```

Refactored Code :

``` C#
using System;

// decorator pattern or proxy pattern can be used

public interface ICalculator {
    int Add(int x, int y);
}

public class LogCalculatorDecorator: ICalculator {
    ICalculator _target;
    public LogCalculatorDecorator(ICalculator cal) {
        this._target = cal;
    }

    public int Add(int x, int y) {
        Console.WriteLine("Add(x={0},y={1})",x,y);
        int add = _target.Add(x,y);
        Console.WriteLine("result={0}", add);
        return add;
    }
}

public class ConcreteCalculator : ICalculator
{
    public int Add(int x, int y)
    {
        var addition = x + y;
        return addition;
    }
}

public class Program
{
    public static void Main() {
        ICalculator _cal = new ConcreteCalculator();
        _cal = new LogCalculatorDecorator(_cal);
        _cal.Add(10,20);
    }
}
```
