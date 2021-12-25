# G�nericos

[![Github][github-shield]][github-url]
[![Kofi][kofi-shield]][kofi-url]
[![LinkedIn][linkedin-shield]][linkedin-url]
[![Khanakat][khanakat-shield]][khanakat-url]

## Tipo gen�rico T

Para crear una clase gen�rica, necesitamos proporcionar un tipo entre par�ntesis angulares:

```csharp
public class CollectionInitializer<T>
{
    ...
}
```

`T` en este ejemplo, act�a como un marcador de posici�n para un tipo con el que queremos trabajar. Necesitamos proporcionar ese tipo una vez que creemos una instancia de esta clase gen�rica. Veamos esto con un ejemplo simple:

```csharp
public class CollectionInitializer<T>
{
    private T[] collection;

    public CollectionInitializer(int collectionLength)
    {
        collection = new T[collectionLength];
    }

    public void AddElementsToCollection(params T[]elements)
    {
        for(int i=0; i<elements.Length; i++)
        {
            collection[i] = elements[i];
        }
    }

    public T[] RetrieveAllElements()
    {
        return collection;
    }

    public T RetreiveElementOnIndex(int index)
    {
        return collection[index];
    }
}
```

Y para usar esta clase gen�rica:

```csharp
class Program
{
    static void Main(string[] args)
    {
        CollectionInitializer<int> initializer = new CollectionInitializer<int>(5);

        initializer.AddElementsToCollection(5, 8, 12, 74, 13);
        int[] collection = initializer.RetrieveAllElements();
        int number = initializer.RetreiveElementOnIndex(3);

        foreach (int element in collection)
        {
            Console.WriteLine(element);
        }

        Console.WriteLine();
        Console.WriteLine($"Element on the selected index is: {number}");

        Console.ReadKey();
    }
}
```

Como podemos ver en nuestra clase `CollectionInitializer`, debemos proporcionar el tipo con el que queremos trabajar. Entonces, podemos simplemente llamar a los m�todos implementados dentro de nuestra clase gen�rica. Por supuesto, no implementamos controles de seguridad (si enviamos m�s elementos que la longitud de la matriz, etc.) solo por simplicidad. Ahora podemos ver el resultado:

```bash
5
8
12
74
13

Element on the selected index is: 74
```

Una clase gen�rica puede tener m�s de un par�metro de tipo:

```csharp
public class CollectionKeyValueInitializer<TKey, TValue>
```

## Restricciones con gen�ricos

A veces, queremos asegurarnos de que solo se puedan invocar ciertos tipos con nuestra clase gen�rica. Suele ser �til al trabajar con clases o interfaces. Podemos hacer eso usando la palabra clave where:

```csharp
public class CollectionInitializer<T> where T: Student
```

o podemos limitar nuestra clase gen�rica para trabajar solo con clases:

```csharp
public class CollectionInitializer<T> where T: class
```

Existen diferentes variaciones para estas restricciones, dependen de la situaci�n en la que estemos trabajando. Es importante saber que si restringimos nuestra clase gen�rica para trabajar solo con clases, obtendremos un error si proporcionamos el tipo de valor. Si queremos trabajar solo con tipos de valor, podemos restringir nuestra clase gen�rica de esta manera:

```csharp
public class CollectionInitializer<T> where T: struct
```

## M�todos gen�ricos

De la misma forma que podemos crear una clase gen�rica, podemos crear un m�todo gen�rico. Solo necesitamos establecer un par�metro de tipo entre par�ntesis angulares justo detr�s del nombre de un m�todo:

```csharp
public void ExampleMethod<T>(T param1, T param2)
{
    //Methods body
}
```

Debemos prestar atenci�n al identificador del par�metro de tipo si nuestro m�todo gen�rico existe dentro de una clase gen�rica. Si esa clase tiene un tipo T, entonces nuestro m�todo debe tener un tipo diferente (U, Y, R�). De lo contrario, el tipo T de un m�todo ocultar� el tipo T de una clase.

## Conclusi�n

En este art�culo, hemos aprendido:

- C�mo usar gen�ricos en C #
- C�mo implementar restricciones en nuestras clases gen�ricas
- La forma de crear m�todos gen�ricos

<!--- reference style links --->
[github-shield]: https://img.shields.io/badge/-@fernandocalmet-%23181717?style=flat-square&logo=github
[github-url]: https://github.com/fernandocalmet
[kofi-shield]: https://img.shields.io/badge/-@fernandocalmet-%231DA1F2?style=flat-square&logo=kofi&logoColor=ff5f5f
[kofi-url]: https://ko-fi.com/fernandocalmet
[linkedin-shield]: https://img.shields.io/badge/-fernandocalmet-blue?style=flat-square&logo=Linkedin&logoColor=white&link=https://www.linkedin.com/in/fernandocalmet
[linkedin-url]: https://www.linkedin.com/in/fernandocalmet
[khanakat-shield]: https://img.shields.io/badge/khanakat.com-brightgreen?style=flat-square
[khanakat-url]: https://khanakat.com