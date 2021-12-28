# Patr�n de dise�o: Command

[![Github][github-shield]][github-url]
[![Kofi][kofi-shield]][kofi-url]
[![LinkedIn][linkedin-shield]][linkedin-url]
[![Khanakat][khanakat-shield]][khanakat-url]

## Implementaci�n del patr�n de dise�o de comandos

El patr�n de dise�o de Command consta de la clase Invoker, la clase / interfaz Command, las clases de comando Concrete y la clase Receiver. Teniendo eso en cuenta, en nuestro ejemplo, vamos a seguir la misma estructura de dise�o.

Entonces, lo que vamos a hacer es escribir una aplicaci�n simple en la que vamos a modificar el precio del producto que implementar� el patr�n de dise�o de Command.

Dicho esto, comencemos con la clase `Product` de receptor, que debe contener la l�gica empresarial base en nuestra aplicaci�n:

```csharp
public class Product
{
    public string Name { get; set; }
    public int Price { get; set; }

    public Product(string name, int price)
    {
        Name = name;
        Price = price;
    }

    public void IncreasePrice(int amount)
    {
        Price += amount;
        Console.WriteLine($"The price for the {Name} has been increased by {amount}$.");
    }

    public void DecreasePrice(int amount)
    {
        if(amount < Price)
        {
            Price -= amount;
            Console.WriteLine($"The price for the {Name} has been decreased by {amount}$.");
        }
    }

    public override string ToString() => $"Current price for the {Name} product is {Price}$.";
}
```

As� que esta es nuestra clase de receptor, que tiene una l�gica bastante sencilla. Simplemente aumentamos o disminuimos condicionalmente el precio del producto. Finalmente, tenemos el ToStringm�todo, para poder imprimir nuestro objeto.

Ahora la clase Cliente puede crear una instancia de la Productclase y ejecutar las acciones necesarias. Pero el patr�n de dise�o de Command establece que no deber�amos usar clases de receptor directamente. En su lugar, deber�amos extraer todos los detalles de la solicitud en una clase especial: Command.

Y eso es exactamente lo que vamos a hacer.

Lo primero que vamos a hacer es agregar la interfaz `ICommand`:

```csharp
public interface ICommand
{
    void ExecuteAction();
}
```

Solo para enumerar nuestras acciones de modificaci�n de precios, agregaremos una enumeraci�n simple `PriceAction` :

```csharp
public enum PriceAction
{
    Increase,
    Decrease
}
```

Finalmente, agreguemos la clase `ProductCommand`:

```csharp
public class ProductCommand : ICommand
{
    private readonly Product _product;
    private readonly PriceAction _priceAction;
    private readonly int _amount;

    public ProductCommand(Product product, PriceAction priceAction, int amount)
    {
        _product = product;
        _priceAction = priceAction;
        _amount = amount;
    }

    public void ExecuteAction()
    {
        if(_priceAction == PriceAction.Increase)
        {
            _product.IncreasePrice(_amount);
        }
        else
        {
            DecreasePrice(_amount);
        }
    }
}
```

Como podemos ver, la clase `ProductCommand` tiene toda la informaci�n sobre la solicitud y en base a eso ejecuta la acci�n requerida.

Para continuar, agreguemos la clase `ModifyPrice`, que actuar� como Invoker:

```csharp
public class ModifyPrice
{
    private readonly List<ICommand> _commands;
    private ICommand _command;

    public ModifyPrice()
    {
        _commands = new List<ICommand>();
    }

    public void SetCommand(ICommand command) => _command = command;

    public void Invoke()
    {
        _commands.Add(_command);
        _command.ExecuteAction();
    }
}
```

Esta clase puede trabajar con cualquier comando que implemente la interfaz `ICommand` y tambi�n almacenar todas las operaciones.

Ahora, podemos empezar a trabajar con la parte del cliente:

```csharp
class Program
{
    static void Main(string[] args)
    {
        var modifyPrice = new ModifyPrice();
        var product = new Product("Phone", 500);

        Execute(product, modifyPrice, new ProductCommand(product, PriceAction.Increase, 100));
           
        Execute(product, modifyPrice, new ProductCommand(product, PriceAction.Increase, 50));

        Execute(product, modifyPrice, new ProductCommand(product, PriceAction.Decrease, 25));

        Console.WriteLine(product);
    }

    private static void Execute(Product product, ModifyPrice modifyPrice, ICommand productCommand)
    {
        modifyPrice.SetCommand(productCommand);
        modifyPrice.Invoke();
    }
}
```

Este deber�a ser nuestro resultado:

![img01](/img/01.png)

Excelente. Podemos ver el orden de nuestras acciones y el precio correcto despu�s de las modificaciones.

Teniendo en cuenta que estamos realizando un seguimiento de nuestras acciones en la clase Invoker, podemos usar eso para deshacer nuestras operaciones si queremos.

Entonces, intentemos eso.

## Implementaci�n de la operaci�n Deshacer en el patr�n de dise�o de comandos

Para implementar la operaci�n Deshacer, comencemos con la modificaci�n de la interfaz `ICommand` :

```csharp
public interface ICommand
{
    void ExecuteAction();
    void UndoAction();
}
```

Luego, modifiquemos la clase `ProductCommand` agregando el m�todo `UndoAction`:

```csharp
public void UndoAction()
{
    if (_priceAction == PriceAction.Increase)
    {
        _product.DecreasePrice(_amount);
    }
    else
    {
        _product.IncreasePrice(_amount);
    }
}
```

Por supuesto, tambi�n tenemos que modificar la clase `ModifyPrice` agregando el m�todo `UndoActions`:

```csharp
public void UndoActions()
{
    foreach (var command in Enumerable.Reverse(_commands))
    {
        command.UndoAction();
    }
}
```

Tenga en cuenta que no estamos utilizando el m�todo Linq Reverse sino el `Enumerable.Reverse()`. Eso es porque el m�todo Linq mutar�a nuestra lista y no queremos eso. Todo lo que queremos es solo una lista invertida pero sin alterar la lista original en s�.

Ahora, cuando la clase Cliente llame al m�todo `UndoActions`, iterar� a trav�s de todas las operaciones de la lista y ejecutar� la operaci�n opuesta a la requerida anteriormente.

Probemos eso:

```csharp
class Program
{
    static void Main(string[] args)
    {
        var modifyPrice = new ModifyPrice();
        var product = new Product("Phone", 500);

        Execute(product, modifyPrice, new ProductCommand(product, PriceAction.Increase, 100));
          
        Execute(product, modifyPrice, new ProductCommand(product, PriceAction.Increase, 50));

        Execute(product, modifyPrice, new ProductCommand(product, PriceAction.Decrease, 25));

        Console.WriteLine(product);
        Console.WriteLine();

        modifyPrice.UndoActions();
        Console.WriteLine(product);
    }

    private static void Execute(Product product, ModifyPrice modifyPrice, ICommand productCommand)
    {
        modifyPrice.SetCommand(productCommand);
        modifyPrice.Invoke();
    }
}
```

El resultado:

![img02](/img/02.png)

Todo funciona como deber�a.

## Mejorando la Soluci�n

Hemos implementado el patr�n de dise�o Command en nuestra aplicaci�n y no hay nada de malo en eso. Pero hay una falla en nuestra soluci�n que no est� relacionada con el patr�n Command sino con la l�gica empresarial en general.

Si tuvi�ramos que cambiar la cantidad disminuida de 25 a 2500, por ejemplo, �qu� pasar�a? Bueno, tenemos la protecci�n para eso en el m�todo `DecreasePrice` y no afectar� el resultado, y tienes raz�n. Pero afectar� las acciones de Deshacer.

Veamos como:

```csharp
...

Execute(product, modifyPrice, new ProductCommand(product, PriceAction.Decrease, 2500));

...
```

Este ser� el resultado:

![img03](/img/03.png)

Como puede ver, nuestro precio no ha bajado, pero la operaci�n se ha conservado en nuestra tienda, lo que provoc� que fallara la acci�n Deshacer.

Entonces, arreglemos eso.

Lo primero que vamos a hacer es modificar el m�todo `DecreasePrice` en la clase `Product`:

```csharp
public bool DecreasePrice(int amount)
{
    if(amount < Price)
    {
        Price -= amount;
        Console.WriteLine($"The price for the {Name} has been decreased by {amount}$.");
        return true;
    }
    return false;
} 
```

Ahora, tambi�n podemos modificar la clase `ProductCommand`:

```csharp
public class ProductCommand : ICommand
{
    private readonly Product _product;
    private readonly PriceAction _priceAction;
    private readonly int _amount;

    public bool IsCommandExecuted { get; private set; }

    public ProductCommand(Product product, PriceAction priceAction, int amount)
    {
        _product = product;
        _priceAction = priceAction;
        _amount = amount;
    }

    public void ExecuteAction()
    {
        if(_priceAction == PriceAction.Increase)
        {
            _product.IncreasePrice(_amount);
            IsCommandExecuted = true;
        }
        else
        {
            IsCommandExecuted = _product.DecreasePrice(_amount);
        }
    }

    public void UndoAction()
    {
        if (!IsCommandExecuted)
            return;

        if (_priceAction == PriceAction.Increase)
        {
            _product.DecreasePrice(_amount);
        }
        else
        {
            _product.IncreasePrice(_amount);
        }
    }
}
```

Y eso es todo. Ahora, si iniciamos nuestra aplicaci�n con una cantidad reducida de 2500, el resultado ser�a correcto:

![img04](/img/04.png)

## Conclusi�n

Aunque el patr�n de dise�o de Command introduce complejidad en nuestro c�digo, puede resultar muy �til.

Con �l, podemos desacoplar clases que invocan operaciones de clases que realizan estas operaciones. Adem�s, si queremos introducir nuevos comandos, no tenemos que modificar las clases existentes. En cambio, podemos simplemente agregar esas nuevas clases de comando a nuestro proyecto.

<!--- reference style links --->
[github-shield]: https://img.shields.io/badge/-@fernandocalmet-%23181717?style=flat-square&logo=github
[github-url]: https://github.com/fernandocalmet
[kofi-shield]: https://img.shields.io/badge/-@fernandocalmet-%231DA1F2?style=flat-square&logo=kofi&logoColor=ff5f5f
[kofi-url]: https://ko-fi.com/fernandocalmet
[linkedin-shield]: https://img.shields.io/badge/-fernandocalmet-blue?style=flat-square&logo=Linkedin&logoColor=white&link=https://www.linkedin.com/in/fernandocalmet
[linkedin-url]: https://www.linkedin.com/in/fernandocalmet
[khanakat-shield]: https://img.shields.io/badge/khanakat.com-brightgreen?style=flat-square
[khanakat-url]: https://khanakat.com