# SOLID Principles em C#

Os princípios **SOLID** são cinco diretrizes que ajudam a escrever código mais limpo, modular e fácil de manter. Aqui está uma explicação de cada princípio com exemplos em **C#**.

---

## 1. Single Responsibility Principle (**SRP**)  
**Uma classe deve ter apenas um motivo para mudar.**

### ❌ Código errado (violando SRP)
```csharp
public class Report
{
    public string Content { get; set; }

    public Report(string content)
    {
        Content = content;
    }

    public void SaveToFile(string filePath)
    {
        System.IO.File.WriteAllText(filePath, Content);
    }
}
```

🔴 **Problema**: A classe `Report` tem duas responsabilidades:
1. Gerar o relatório.
2. Salvá-lo em um arquivo.

### ✅ Código correto (seguindo SRP)
```csharp
public class Report
{
    public string Content { get; set; }

    public Report(string content)
    {
        Content = content;
    }
}

public class ReportSaver
{
    public void SaveToFile(Report report, string filePath)
    {
        System.IO.File.WriteAllText(filePath, report.Content);
    }
}
```
✔ **Correção**: Agora `Report` só gera o relatório, e `ReportSaver` é responsável por salvá-lo.

---

## 2. Open/Closed Principle (**OCP**)  
**O código deve estar aberto para extensão, mas fechado para modificação.**

### ❌ Código errado (violando OCP)
```csharp
public class DiscountService
{
    public double ApplyDiscount(double price, string type)
    {
        if (type == "percentage")
            return price * 0.9;
        else if (type == "fixed")
            return price - 10;
        return price;
    }
}
```
🔴 **Problema**: Se precisarmos adicionar um novo tipo de desconto, temos que modificar essa classe.

### ✅ Código correto (seguindo OCP)
```csharp
public abstract class Discount
{
    public abstract double Apply(double price);
}

public class PercentageDiscount : Discount
{
    public override double Apply(double price) => price * 0.9;
}

public class FixedDiscount : Discount
{
    public override double Apply(double price) => price - 10;
}
```
✔ **Correção**: Agora podemos criar novos descontos sem modificar a classe base.

---

## 3. Liskov Substitution Principle (**LSP**)
**Subclasses devem ser substituíveis por suas classes base sem quebrar o código.**

### ❌ Código errado (violando LSP)
```csharp
public class Bird
{
    public virtual void Fly()
    {
        Console.WriteLine("This bird is flying.");
    }
}

public class Penguin : Bird
{
    public override void Fly()
    {
        throw new NotImplementedException("Penguins cannot fly!");
    }
}
```
🔴 **Problema**: `Penguin` herda de `Bird`, mas não pode voar. Isso quebra a substituição.

### ✅ Código correto (seguindo LSP)
```csharp
public abstract class Bird { }

public class FlyingBird : Bird
{
    public void Fly()
    {
        Console.WriteLine("This bird is flying.");
    }
}

public class NonFlyingBird : Bird
{
    public void Walk()
    {
        Console.WriteLine("This bird is walking.");
    }
}
```
✔ **Correção**: Separar pássaros que voam e que não voam em classes diferentes.

---

## 4. Interface Segregation Principle (**ISP**)
**Interfaces devem ser específicas e não forçar classes a implementar métodos que não usam.**

### ❌ Código errado (violando ISP)
```csharp
public interface IWorker
{
    void Work();
    void Eat();
}

public class Robot : IWorker
{
    public void Work() { Console.WriteLine("Robot is working."); }
    public void Eat() { throw new NotImplementedException(); }
}
```
🔴 **Problema**: `Robot` não precisa do método `Eat()`.

### ✅ Código correto (seguindo ISP)
```csharp
public interface IWorkable
{
    void Work();
}

public interface IEatable
{
    void Eat();
}

public class Robot : IWorkable
{
    public void Work() { Console.WriteLine("Robot is working."); }
}

public class Human : IWorkable, IEatable
{
    public void Work() { Console.WriteLine("Human is working."); }
    public void Eat() { Console.WriteLine("Human is eating."); }
}
```
✔ **Correção**: Interfaces separadas para trabalho e alimentação.

---

## 5. Dependency Inversion Principle (**DIP**)
**Dependa de abstrações, não de implementações concretas.**

### ❌ Código errado (violando DIP)
```csharp
public class NotificationService
{
    private readonly EmailSender _emailSender;

    public NotificationService()
    {
        _emailSender = new EmailSender();
    }

    public void Notify(string message)
    {
        _emailSender.SendEmail(message);
    }
}
```
🔴 **Problema**: `NotificationService` depende diretamente de `EmailSender`.

### ✅ Código correto (seguindo DIP)
```csharp
// Criamos uma interface para abstrair o envio da mensagem
public interface IMessageSender
{
    void SendMessage(string message);
}

// Implementamos o envio de email
public class EmailSender : IMessageSender
{
    public void SendMessage(string message)
    {
        Console.WriteLine($"Email enviado: {message}");
    }
}

// Implementamos o envio de SMS
public class SmsSender : IMessageSender
{
    public void SendMessage(string message)
    {
        Console.WriteLine($"SMS enviado: {message}");
    }
}

// NotificationService agora depende da interface, não da implementação concreta
public class NotificationService
{
    private readonly IMessageSender _messageSender;

    public NotificationService(IMessageSender messageSender)
    {
        _messageSender = messageSender;
    }

    public void Notify(string message)
    {
        _messageSender.SendMessage(message);
    }
}

// Podemos trocar Email para SMS sem mudar NotificationService!
class Program
{
    static void Main()
    {
        IMessageSender emailSender = new EmailSender();
        IMessageSender smsSender = new SmsSender();

        NotificationService notificationEmail = new NotificationService(emailSender);
        notificationEmail.Notify("Olá via E-mail!");

        NotificationService notificationSms = new NotificationService(smsSender);
        notificationSms.Notify("Olá via SMS!");
    }
}
```
✔ **Correção**: Agora `NotificationService` depende da abstração `IMessageSender`, permitindo trocar implementações facilmente.

---

Esses exemplos seguem os princípios **SOLID** para melhorar a modularidade e manutenção do código! 🚀

