# Chain of Responsibility Example

Цей репозиторій містить приклад патерну проектування "Ланцюжок обов'язків".

## Патерн Ланцюжок обов'язків (Chain of Responsibility)

Патерн "Ланцюжок обов'язків" дозволяє уникнути жорсткого зв'язування між запитом та обробником. Кожен обробник у ланцюгу отримує запит і може обробити його або передати далі.

### Приклад коду:

```csharp
using System;

// Базовий клас обробника
abstract class Handler
{
    protected Handler _nextHandler;

    public void SetNext(Handler nextHandler)
    {
        _nextHandler = nextHandler;
    }

    public abstract void HandleRequest(string request);
}

// Конкретний обробник A
class ConcreteHandlerA : Handler
{
    public override void HandleRequest(string request)
    {
        if (request == "A")
        {
            Console.WriteLine("Обробник A обробив запит.");
        }
        else if (_nextHandler != null)
        {
            _nextHandler.HandleRequest(request);
        }
    }
}

// Конкретний обробник B
class ConcreteHandlerB : Handler
{
    public override void HandleRequest(string request)
    {
        if (request == "B")
        {
            Console.WriteLine("Обробник B обробив запит.");
        }
        else if (_nextHandler != null)
        {
            _nextHandler.HandleRequest(request);
        }
    }
}

// Конкретний обробник C
class ConcreteHandlerC : Handler
{
    public override void HandleRequest(string request)
    {
        if (request == "C")
        {
            Console.WriteLine("Обробник C обробив запит.");
        }
        else if (_nextHandler != null)
        {
            _nextHandler.HandleRequest(request);
        }
    }
}

// Клієнтський код
class Program
{
    static void Main(string[] args)
    {
        var handlerA = new ConcreteHandlerA();
        var handlerB = new ConcreteHandlerB();
        var handlerC = new ConcreteHandlerC();

        handlerA.SetNext(handlerB);
        handlerB.SetNext(handlerC);

        // Запити
        handlerA.HandleRequest("A");
        handlerA.HandleRequest("B");
        handlerA.HandleRequest("C");
        handlerA.HandleRequest("D");
    }
}
