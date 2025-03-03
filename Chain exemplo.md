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
