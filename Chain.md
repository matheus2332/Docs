# Chain of Responsibility e Middleware Pipeline no .NET Core

## 1. Chain of Responsibility
O **Chain of Responsibility** é um padrão de design comportamental onde uma solicitação passa por uma cadeia de manipuladores até que um deles a processe. Isso permite um fluxo dinâmico, desacoplando remetente e receptor.

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

Aqui, cada manipulador decide se processa a requisição ou a passa para o próximo na cadeia.

---

## 2. Middleware Pipeline no ASP.NET Core
No **ASP.NET Core**, as requisições HTTP passam por um pipeline de middlewares, onde cada middleware pode manipular a requisição ou delegar para o próximo.

### Exemplo de Middleware:

```csharp
app.Use(async (context, next) =>
{
    Console.WriteLine("Middleware 1");
    await next.Invoke(); // Chama o próximo middleware
    Console.WriteLine("Middleware 1 - Resposta");
});

app.Use(async (context, next) =>
{
    Console.WriteLine("Middleware 2");
    await next.Invoke();
    Console.WriteLine("Middleware 2 - Resposta");
});
```

Cada middleware pode:
- Processar a requisição antes ou depois do próximo middleware.
- Interromper o fluxo se necessário.

Este conceito é essencial para configurações como autenticação, logging e manipulação de erros.

---

Esses conceitos ajudam a organizar e modularizar o código, facilitando a manutenção e extensibilidade do sistema. 🚀

