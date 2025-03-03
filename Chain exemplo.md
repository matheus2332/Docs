# Exemplo 1: Processamento de Pedidos em um E-commerce

### Descrição
Este exemplo demonstra como aplicar o padrão *Chain of Responsibility* no contexto de um e-commerce. O pedido de um cliente precisa passar por várias etapas de validação, como a verificação de estoque, validação de pagamento e verificação de fraudes. Cada etapa é tratada por um manipulador diferente na cadeia.

### Código

#### 1. Interface do Manipulador

```csharp
public interface IOrderHandler
{
    void SetNext(IOrderHandler handler);
    void Handle(Order order);
}
```
#### 2. Manipuladores de Validação
Validação de Estoque
```csharp
public class StockHandler : IOrderHandler
{
    private IOrderHandler _nextHandler;

    public void SetNext(IOrderHandler handler)
    {
        _nextHandler = handler;
    }

    public void Handle(Order order)
    {
        if (order.IsInStock())
        {
            Console.WriteLine("Estoque validado!");
            _nextHandler?.Handle(order);
        }
        else
        {
            Console.WriteLine("Produto fora de estoque.");
        }
    }
}
```
Validação de Pagamento

```csharp
public class PaymentHandler : IOrderHandler
{
    private IOrderHandler _nextHandler;

    public void SetNext(IOrderHandler handler)
    {
        _nextHandler = handler;
    }

    public void Handle(Order order)
    {
        if (order.IsPaymentValid())
        {
            Console.WriteLine("Pagamento validado!");
            _nextHandler?.Handle(order);
        }
        else
        {
            Console.WriteLine("Pagamento inválido.");
        }
    }
}
```

Verificação de Fraude

```csharp
public class FraudHandler : IOrderHandler
{
    private IOrderHandler _nextHandler;

    public void SetNext(IOrderHandler handler)
    {
        _nextHandler = handler;
    }

    public void Handle(Order order)
    {
        if (order.IsFraudFree())
        {
            Console.WriteLine("Verificação de fraude completada!");
            _nextHandler?.Handle(order);
        }
        else
        {
            Console.WriteLine("Pedido marcado como fraude.");
        }
    }
}
4. Cliente
```csharp
class Program
{
    static void Main(string[] args)
    {
        // Criar os manipuladores
        IOrderHandler stockHandler = new StockHandler();
        IOrderHandler paymentHandler = new PaymentHandler();
        IOrderHandler fraudHandler = new FraudHandler();

        // Definir a cadeia
        stockHandler.SetNext(paymentHandler);
        paymentHandler.SetNext(fraudHandler);

        // Criar um pedido e passar pela cadeia
        var order = new Order();
        stockHandler.Handle(order);
    }
}
```
Saída Esperada

```plaintext
Estoque validado!
Pagamento validado!
Verificação de fraude completada!
```
### Vantagens do Padrão Chain of Responsibility no Exemplo 1
#### . Separation of Concerns (Separação de Responsabilidades)
#### . Extensibilidade (Facilidade de Adicionar Novos Processos)
#### . Facilidade de Manutenção e Testabilidade
#### . Atenção a Falhas Específicas
#### . Facilidade de Reuso
#### . Controle do Fluxo
