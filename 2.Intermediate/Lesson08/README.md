# Interfaces

[![Github][github-shield]][github-url]
[![Kofi][kofi-shield]][kofi-url]
[![LinkedIn][linkedin-shield]][linkedin-url]
[![Khanakat][khanakat-shield]][khanakat-url]

## Definici�n de una interfaz

Para definir una interfaz, necesitamos usar la palabra clave `interface`. Es bastante similar a definir una clase, solo que usamos otra palabra clave. Dentro de esa interfaz, especificamos nuestros miembros sin modificador de acceso ni implementaci�n. Entonces, solo proporcionamos una declaraci�n para los miembros, una implementaci�n es un trabajo para una clase que implementa esa interfaz:

```csharp
interface InterfaceName
{
    returnType methodName(paramType paramName...);
}
```

## Implementar una interfaz

Para implementar una interfaz, declaramos una clase o estructura que hereda de la interfaz e implementa todos los miembros de ella:

```csharp
class ClassName: InterfaceName
{
    //members implementation
}
```

Veamos todo esto a trav�s del ejemplo:

```csharp
public interface IWriter
{
    void WriteFile();
}

public class XmlWritter: IWriter
{
    public void WriteFile()
    {
        Console.WriteLine("Writing file in the XmlWriter class.");
    }
}

public class JsonWriter: IWriter
{
    public void WriteFile()
    {
        Console.WriteLine("Writing file in the JsonWritter class.");
    }
}
```

Como podemos ver, despu�s de que nuestras clases hereden de una interfaz, deben implementar el miembro `WriteFile()`. De lo contrario, obtendr�amos un error del compilador.

Cuando implementamos una interfaz, debemos asegurarnos de proporcionar la implementaci�n del m�todo siguiendo estas reglas:

- Los nombres de los m�todos y los tipos de retorno deben coincidir exactamente
- Cualquier par�metro debe coincidir exactamente
- Todos los m�todos deben ser p�blicos durante la implementaci�n. Este no es el caso con la implementaci�n expl�cita de la interfaz (hablaremos de eso un poco m�s adelante)

Una clase puede heredar de una clase e implementar una interfaz al mismo tiempo. Pero si este es un caso, primero debemos especificar una clase base y luego una interfaz separada por comas:

```csharp
public interface IWriter
{
    void WriteFile();
}

public class FileBase
{
    public virtual void SetName()
    {
        Console.WriteLine("Setting name in the base Writer class.");
    }
}

public class XmlWritter: FileBase, IWriter
{
    public void WriteFile()
    {
        Console.WriteLine("Writing file in the XmlWriter class.");
    }

    public override void SetName()
    {
        Console.WriteLine("Setting name in the XmlWriter class.");
    }
}

public class JsonWriter: FileBase, IWriter
{
    public void WriteFile()
    {
        Console.WriteLine("Writing file in the JsonWritter class.");
    }

    public override void SetName()
    {
        Console.WriteLine("Setting name in the JsonWriter class.");
    }
}
```

## Hacer referencia a clases a trav�s de interfaces

De la misma manera que podemos hacer referencia a un objeto usando una variable de clase, podemos definir un objeto usando una variable de interfaz:

```csharp
XmlWriter writer = new XmlWriter();
writer.SetName(); //overridden method from a base class
writer.WriteFile(); //method from an interface
```

Como podemos ver, todos los m�todos est�n disponibles a trav�s del objeto `writer`. Pero ahora usemos un objeto de interfaz para hacer referencia a la acci�n:

```csharp
IWriter writer = new XmlWriter();
writer.WriteFile(); //method from an interface
writer.SetName(); //error the SetName method is not part of the IWriter interface
```

Si usamos una interfaz para crear un objeto, podemos acceder solo a los miembros declarados en esa interfaz.
Como mencionamos anteriormente, la interfaz proporciona un contrato para la clase que hereda de ella. Y esta es una gran ventaja de usar interfaces, siempre podemos estar seguros cuando una clase hereda de nuestra interfaz implementar� todos sus miembros.

Pero la implementaci�n de la interfaz tiene a�n m�s ventajas. Uno de ellos es el desacoplamiento de objetos.

## Usar una interfaz para desacoplar clases

Cuando una clase depende de otra clase, esas clases est�n acopladas. Esto es algo que queremos evitar porque si algo cambia en la clase A y la clase B depende en gran medida de la clase A, existe una gran posibilidad de que tengamos que cambiar tambi�n una clase B. O al menos, no estaremos seguros de si la Clase B a�n funciona correctamente. En consecuencia, queremos que nuestras clases est�n acopladas o "desacopladas" de manera flexible.

Veamos qu� pasar�a si creamos nuestras clases fuertemente acopladas:

```csharp
public class XmlFileWriter
{
    private XmlWriter _xmlWriter;

    public XmlFileWriter(XmlWriter xmlWriter)
    {
        _xmlWriter = xmlWriter;
    }

    public void Write()
    {
        _xmlWriter.WriteFile();
    }
}
```

Esta `XmlFileWriter` es una clase que tiene el prop�sito de escribir en un archivo xml. Ahora podemos crear una instancia de nuestra clase `XmlWriter`, enviar el objeto a trav�s del constructor `XmlFileWriter` y llamar al m�todo `Write`:

```csharp
class Program
{
    static void Main(string[] args)
    {
        XmlWriter xmlWriter = new XmlWriter();
        XmlFileWriter fileWriter = new XmlFileWriter(xmlWriter);
        fileWriter.Write();
    }
}
```

Ok, todo funciona muy bien por ahora.

Pero tenemos un par de problemas aqu�. Nuestra clase `XmlFileWriter` est� fuertemente acoplada a la clase `XmlWriter`. Si cambiamos el m�todo `WriteFile` dentro de la clase `XmlWriter`, tambi�n debemos cambiarlo en la clase `XmlFileWriter`. Entonces, el cambio en una clase conduce a un cambio en otra. No es as� como queremos que funcione nuestro c�digo.

Otra cosa. Seguramente queremos tener el mismo comportamiento para nuestra clase `JsonWriter`. No podemos usar esto `XmlFileWriter` (porque acepta solo el XmlWriterobjeto), debemos crear otra clase y repetir todas nuestras acciones. Esto tambi�n es bastante malo.

Finalmente, podemos preguntarnos, si realmente necesitamos dos clases para el mismo trabajo. �Por qu� no podemos usar solo uno? Bueno, ah� es donde entran las interfaces.

Modifiquemos la clase `XmlFileWriter`:

```csharp
public class FileWriter
{
    private readonly IWriter _writer;

    public FileWriter(IWriter writer)
    {
        _writer = writer;
    }

    public void Write()
    {
        _writer.WriteFile();
    }
}
```

Excelente. Esto es mucho mejor.

Ahora nuestro nombre de clase nos dice que esta clase no escribe solo archivos xml. Adem�s, no estamos restringiendo nuestro constructor para que acepte solo la clase `XmlWiter`, sino todas las clases que heredan de la interfaz `IWriter`. Nuestro m�todo `WriteFile` no puede cambiarse de nombre ahora debido a nuestra interfaz `IWritter`, que establece que todas las clases deben implementar un m�todo con un nombre id�ntico. Podemos ver ahora que la clase `FileWriter` est� desacoplada de `XmlWriter` o de `JsonWriter`, y que podemos enviar objetos de ambas clases a la clase `FileWriter`:

```csharp
class Program
{
    static void Main(string[] args)
    {
        XmlWriter xmlWriter = new XmlWriter();
        JsonWriter jsonWriter = new JsonWriter();

        FileWriter fileWriter = new FileWriter(xmlWriter);
        fileWriter.Write();

        fileWriter = new FileWriter(jsonWriter);
        fileWriter.Write();

        Console.ReadKey();
    }
}
```

Resultado:

```bash
Writing file in the XmlWriter class.
Writing file in the JsonWriter class.
```

�No es esto mucho mejor?

Ahora tenemos una clase que hace su trabajo para cualquier clase que herede de la interfaz `IWriter`.

Esta funci�n se conoce como inyecci�n de dependencia.

## Trabajar con m�ltiples interfaces

Una clase puede heredar solo de una clase base, pero puede implementar m�ltiples interfaces. La clase debe implementar todos los m�todos definidos en esas interfaces:

```csharp
public interface IFormatter
{
    void FormatFile();
}

public class XmlWriter: FileBase, IWriter, IFormatter
{
    public void WriteFile()
    {
        Console.WriteLine("Writing file in the XmlWriter class.");
    }

    public override void SetName()
    {
        Console.WriteLine("Setting name in the XmlWriter class.");
    }

    public void FormatFile()
    {
        Console.WriteLine("Formatting file in XmlWriter class.");
    }
}
```

## Implementaci�n de interfaz expl�cita

Como ya dijimos, una clase puede implementar m�s de una interfaz. No es inusual que dos de esas interfaces tengan un m�todo con el mismo nombre, pero a�n necesitamos implementarlas en nuestra clase. Para hacer eso, no implementamos un m�todo como lo hicimos antes, pero necesitamos indicar el nombre de la interfaz primero y luego el nombre de un m�todo con par�metros:

```csharp
public interface Interface1
{
    void MethodExample();
}

public interface Interface2
{
    void MethodExample();
}

public class ExampleClass: Interface1, Interface2
{
    void Interface1.MethodExample()
    {
        Console.WriteLine("");
    }

    void Interface2.MethodExample()
    {
        Console.WriteLine("");
    }

}
```

Como podemos ver, no estamos usando un modificador de acceso en la implementaci�n del m�todo.

## Conclusi�n

En este art�culo, hemos aprendido:

- C�mo definir e implementar una interfaz
- C�mo hacer referencia a una clase a trav�s de la interfaz
- La forma de desacoplar nuestros objetos con interfaces e inyecci�n de dependencias
- Para implementar expl�citamente nuestras interfaces

<!--- reference style links --->
[github-shield]: https://img.shields.io/badge/-@fernandocalmet-%23181717?style=flat-square&logo=github
[github-url]: https://github.com/fernandocalmet
[kofi-shield]: https://img.shields.io/badge/-@fernandocalmet-%231DA1F2?style=flat-square&logo=kofi&logoColor=ff5f5f
[kofi-url]: https://ko-fi.com/fernandocalmet
[linkedin-shield]: https://img.shields.io/badge/-fernandocalmet-blue?style=flat-square&logo=Linkedin&logoColor=white&link=https://www.linkedin.com/in/fernandocalmet
[linkedin-url]: https://www.linkedin.com/in/fernandocalmet
[khanakat-shield]: https://img.shields.io/badge/khanakat.com-brightgreen?style=flat-square
[khanakat-url]: https://khanakat.com