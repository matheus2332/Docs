# Novidades do C# 12

O C# 12 introduziu várias melhorias que facilitam a escrita de código mais limpo e legível. Aqui estão as principais novidades com exemplos:

## 1. Construtores Primários Simplificados

O C# 12 facilita a criação de construtores primários em classes e estruturas, permitindo inicializar propriedades diretamente no parâmetro do construtor.

### Exemplo:
**Antes de C# 12:**

```csharp
public class Person
{
    public string Name { get; }
    public int Age { get; }

    public Person(string name, int age)
    {
        Name = name;
        Age = age;
    }
}
```
**Com C# 12:**

```csharp
public class Person(string Name, int Age);
```

Agora, você pode declarar as propriedades diretamente nos parâmetros do construtor, simplificando o código.

## 2. Suporte a Matrizes e Coleções
O C# 12 facilita a criação de matrizes, spans e coleções com inicializadores mais intuitivos.

###Exemplo com Matrizes:
Antes de C# 12:

```csharp

int[] numbers = new int[3];
numbers[0] = 1;
numbers[1] = 2;
numbers[2] = 3;
```
Com C# 12:
```csharp
int[] numbers = { 1, 2, 3 };
```
Exemplo com Listas:
```csharp
var numbers = new List<int> { 1, 2, 3 };
```

##3. Constantes de Tipo Simples
O C# 12 introduz suporte aprimorado para constantes de tipo, facilitando o uso de valores mais complexos como constantes.

```csharp
const string message = "Olá, C# 12!";
Console.WriteLine(message);  // Saída: Olá, C# 12!
```

Essa melhoria torna o código mais legível e facilita a manutenção de valores constantes.
