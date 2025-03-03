# Chain of Responsibility, Middleware Pipeline, Factory e Pipeline no .NET Core

## 1. Chain of Responsibility
O **Chain of Responsibility** é um padrão de design comportamental onde uma solicitação passa por uma cadeia de manipuladores até que um deles a processe. Isso permite um fluxo dinâmico, desacoplando remetente e receptor.

### Vantagens:
- Reduz o acoplamento entre remetente e receptor.
- Facilita a adição de novos manipuladores sem alterar a lógica existente.
- Torna o código mais flexível e reutilizável.

### Desvantagens:
- Pode ser difícil de depurar devido à passagem de requisições entre múltiplos handlers.
- Se a cadeia for muito longa, pode impactar a performance.

### Exemplo de Implementação:

```csharp
public abstract class Handler
{
    protected Handler _next;

    public void SetNext(Handler next) => _next = next;

    public abstract void Handle(string request);
}

public class ConcreteHandlerA : Handler
{
    public override void Handle(string request)
    {
        if (request == "A")
            Console.WriteLine("Handled by A");
        else
            _next?.Handle(request);
    }
}
```

---

## 2. Factory Pattern
O **Factory Pattern** é um padrão de criação que permite instanciar objetos sem expor a lógica de criação diretamente ao cliente. Ele é útil para desacoplar a lógica de inicialização de classes.

### Vantagens:
- Facilita a criação de objetos complexos.
- Promove o princípio da inversão de dependência.
- Torna o código mais modular e reutilizável.

### Desvantagens:
- Pode aumentar a complexidade do código, especialmente se houver muitas fábricas.
- Exige um maior número de classes, o que pode tornar o código mais verboso.

### Exemplo de Implementação:

```csharp
public interface IProduct
{
    void Operation();
}

public class ConcreteProductA : IProduct
{
    public void Operation()
    {
        Console.WriteLine("Produto A criado");
    }
}

public class ConcreteProductB : IProduct
{
    public void Operation()
    {
        Console.WriteLine("Produto B criado");
    }
}

public class Factory
{
    public static IProduct CreateProduct(string type)
    {
        return type switch
        {
            "A" => new ConcreteProductA(),
            "B" => new ConcreteProductB(),
            _ => throw new ArgumentException("Tipo de produto desconhecido")
        };
    }
}
```

---

## 3. Pipeline Pattern
O **Pipeline Pattern** é um padrão de design que permite encadear operações de processamento de maneira sequencial, onde cada etapa pode modificar ou processar os dados antes de passá-los para a próxima etapa.

### Vantagens:
- Fácil de entender e manter.
- Permite composição dinâmica de etapas de processamento.
- Funciona bem para cenários de processamento de dados e requisições encadeadas.

### Desvantagens:
- Pode adicionar overhead se houver muitas etapas no pipeline.
- Difícil de implementar rollback em caso de falha em uma etapa intermediária.

### Exemplo de Implementação:

```csharp
public interface IStage
{
    string Execute(string input);
}

public class StageA : IStage
{
    public string Execute(string input)
    {
        return input + " -> Processado por A";
    }
}

public class StageB : IStage
{
    public string Execute(string input)
    {
        return input + " -> Processado por B";
    }
}

public class Pipeline
{
    private readonly List<IStage> _stages = new();

    public Pipeline AddStage(IStage stage)
    {
        _stages.Add(stage);
        return this;
    }

    public string Execute(string input)
    {
        foreach (var stage in _stages)
        {
            input = stage.Execute(input);
        }
        return input;
    }
}
```

Esses conceitos ajudam a organizar e modularizar o código, facilitando a manutenção e extensibilidade do sistema. 🚀

