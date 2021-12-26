# Patr�n de dise�o: Factory Method

[![Github][github-shield]][github-url]
[![Kofi][kofi-shield]][kofi-url]
[![LinkedIn][linkedin-shield]][linkedin-url]
[![Khanakat][khanakat-shield]][khanakat-url]

## Implementaci�n del Factory Method

Para implementar un patr�n de m�todo de f�brica, vamos a crear una aplicaci�n de aire acondicionado simple. Nuestra aplicaci�n recibir� una entrada de un usuario y, en base a esa entrada, activar� una acci�n requerida (enfriar o calentar la habitaci�n). As� que comencemos con una interfaz:

```csharp
public interface IAirConditioner
{
    void Operate();
}
```

Ahora, necesitamos clases concretas para implementar esta interfaz:

```csharp
public class CoolingManager : IAirConditioner
{
    private readonly double _temperature;

    public CoolingManager(double temperature)
    {
        _temperature = temperature;
    }

    public void Operate()
    {
        Console.WriteLine($"Cooling the room to the required temperature of {_temperature} degrees");
    }
}
```

```csharp
public class WarmingManager : IAirConditioner
{
    private readonly double _temperature;

    public WarmingManager(double temperature)
    {
        _temperature = temperature;
    }

    public void Operate()
    {
        Console.WriteLine($"Warming the room to the required temperature of {_temperature} degrees.");
    }
}
```

Estupendo. Hemos preparado nuestra funcionalidad base. Ahora creemos un creador de f�brica para estos objetos.

## Clase Factory

Vamos a empezar con la clase abstracta `AirConditionerFactory` :

```csharp
public abstract class AirConditionerFactory
{
    public abstract IAirConditioner Create(double temperature);
}
```

Esta clase abstracta proporciona una interfaz para la creaci�n de objetos en clases derivadas. Dicho esto, implementemos nuestras clases de creadores concretas:

```csharp
public class CoolingFactory : AirConditionerFactory
{
    public override IAirConditioner Create(double temperature) => new CoolingManager(temperature);
}
```

```csharp
public class WarmingFactory : AirConditionerFactory
{
    public override IAirConditioner Create(double temperature) => new WarmingManager(temperature);
}
```

Excelente. Ahora estamos listos para comenzar a usar nuestros m�todos de f�brica. En muchos ejemplos, podemos ver la declaraci�n de cambio que cambia a trav�s de la entrada del usuario y selecciona la clase de f�brica requerida.

Eso funciona bien.

Pero imag�nese si tenemos muchas clases de f�brica, lo cual es bastante com�n en proyectos grandes. Eso conducir�a a una declaraci�n de caso de cambio bastante grande que es bastante ilegible. Por lo tanto, usaremos otro enfoque.

## Ejecuci�n de Factory

Comencemos con una enumeraci�n simple para definir las acciones del aire acondicionado:

```csharp
public enum Actions
{
    Cooling,
    Warming
}
```

Para continuar, vamos a crear la clase `AirConditioner` donde el usuario puede especificar el tipo de acci�n y ejecutar la f�brica correspondiente. Nuestras f�bricas de hormig�n heredan de la clase abstracta y vamos a utilizar esa estructura en nuestra implementaci�n posterior:

```csharp
public class AirConditioner
{
    private readonly Dictionary<Actions, AirConditionerFactory> _factories;

    public AirConditioner()
    {
        _factories = new Dictionary<Actions, AirConditionerFactory>
        {
            { Actions.Cooling, new CoolingFactory() },
            { Actions.Warming, new WarmingFactory() }
        };
    }
}
```

Esta es una mejor manera de implementar nuestra ejecuci�n de f�brica que usar una declaraci�n de caso de cambio. Pero podemos hacerlo de otra manera m�s din�mica, donde no tengamos que agregar manualmente la acci�n y el creador de f�brica para cada acci�n. Introduzcamos la reflexi�n en nuestro proyecto:

```csharp
public class AirConditioner
{
    private readonly Dictionary<Actions, AirConditionerFactory> _factories;

    public AirConditioner()
    {
        _factories = new Dictionary<Actions, AirConditionerFactory>();

        foreach (Actions action in Enum.GetValues(typeof(Actions)))
        {
            var factory = (AirConditionerFactory)Activator.CreateInstance(Type.GetType("FactoryMethod." + Enum.GetName(typeof(Actions), action) + "Factory"));
            _factories.Add(action, factory);
        }
    }
}
```

Ya sea que elijamos el primer o el segundo ejemplo, el resultado deber�a ser el mismo:

![img01](/img/01.png)

Hay una cosa m�s que debemos agregar a esta clase. Y ese es el m�todo que va a ejecutar la creaci�n apropiada:

```csharp
public class AirConditioner
{
    //previous constructor code

    public IAirConditioner ExecuteCreation(Actions action, double temperature) =>_factories[action].Create(temperature);
}
```

Ahora, solo tenemos que hacer una llamada de un cliente. En un proyecto del mundo real, seguramente verificar�amos primero la temperatura actual y luego solo tendr�amos una f�brica para decidir si deber�amos reducirla o aumentarla. Pero en aras de la simplicidad, solo vamos a hacer una simple llamada a nuestra clase de `AirConditioner`:

```csharp
class Program
{
    static void Main(string[] args)
    {
        var factory = new AirConditioner().ExecuteCreation(Actions.Cooling, 22.5);
        factory.Operate();
    }
}
```

Nuestro resultado deber�a ser el esperado:

![img02](/img/02.png)

## Uso de la t�cnica de refactorizaci�n del factory method

Podemos usar el m�todo Factory para reemplazar nuestro constructor mientras creamos un objeto. Si nuestro constructor consta de mucho c�digo, deber�amos reemplazarlo con el m�todo de f�brica. Adem�s, podemos tener m�ltiples m�todos de f�brica con nombres significativos y nombres de par�metros que reemplazan a un solo constructor.

Esto mejora mucho la legibilidad del c�digo.

Finalmente, nos ayuda a implementar una sintaxis de encadenamiento.

Entonces modifiquemos la clase `AirConditioner` con el m�todo de f�brica:

```csharp
public class AirConditioner
{
    private readonly Dictionary<Actions, AirConditionerFactory> _factories;

    private AirConditioner()
    {
        _factories = new Dictionary<Actions, AirConditionerFactory>();

        foreach (Actions action in Enum.GetValues(typeof(Actions)))
        {
            var factory = (AirConditionerFactory)Activator.CreateInstance(Type.GetType("FactoryMethod." + Enum.GetName(typeof(Actions), action) + "Factory"));
                _factories.Add(action, factory);
        }
    }

    public static AirConditioner InitializeFactories() => new AirConditioner();

    public IAirConditioner ExecuteCreation(Actions action, double temperature) =>_factories[action].Create(temperature);
}
```

Nuestra llamada de cliente tambi�n debe modificarse:

```csharp
class Program
{
    static void Main(string[] args)
    {
        AirConditioner
            .InitializeFactories()
            .ExecuteCreation(Actions.Cooling, 22.5)
            .Operate();
    }
}
```

Excelente. El resultado deber�a ser el mismo, pero ahora estamos usando la t�cnica de refactorizaci�n del factory method.

## Conclusi�n

Al leer este art�culo, hemos aprendido:

- C�mo implementar el patr�n de dise�o del m�todo de f�brica en la aplicaci�n
- Varias formas de reemplazar declaraciones de cambio de may�sculas y min�sculas mediante el uso de un diccionario o una reflexi�n
- C�mo refactorizar su c�digo utilizando la t�cnica de refactorizaci�n del factory method

<!--- reference style links --->
[github-shield]: https://img.shields.io/badge/-@fernandocalmet-%23181717?style=flat-square&logo=github
[github-url]: https://github.com/fernandocalmet
[kofi-shield]: https://img.shields.io/badge/-@fernandocalmet-%231DA1F2?style=flat-square&logo=kofi&logoColor=ff5f5f
[kofi-url]: https://ko-fi.com/fernandocalmet
[linkedin-shield]: https://img.shields.io/badge/-fernandocalmet-blue?style=flat-square&logo=Linkedin&logoColor=white&link=https://www.linkedin.com/in/fernandocalmet
[linkedin-url]: https://www.linkedin.com/in/fernandocalmet
[khanakat-shield]: https://img.shields.io/badge/khanakat.com-brightgreen?style=flat-square
[khanakat-url]: https://khanakat.com