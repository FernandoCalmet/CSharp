# Lista gen�rica y diccionario

[![Github][github-shield]][github-url]
[![Kofi][kofi-shield]][kofi-url]
[![LinkedIn][linkedin-shield]][linkedin-url]
[![Khanakat][khanakat-shield]][khanakat-url]

## Lista <T>

Una `List<T>` representa una colecci�n de objetos fuertemente tipados a los que se puede acceder por �ndice.

Para crear una instancia `List<T>`, necesitamos proporcionar un tipo entre los corchetes angulares:

```csharp
List<int> numberList = new List<int>();
List<Student> students = new List<Student>();
```

Tiene dos constructores m�s que podemos usar para inicializar un objeto List. Con el primero, podemos configurar la capacidad inicial:

```csharp
List<int> numbers = new List<int>(2);
```

Con el segundo, podemos completar nuestra lista con la colecci�n `IEnumerable`:

```csharp
int[] nums = new int[5] { 1, 2, 3, 4, 5 };
List<int> numbers = new List<int>(nums);
```

Para acceder a cualquier elemento podemos especificar su posici�n de �ndice:

```csharp
int number = numbers[1];
```

## M�todos y propiedades

El m�todo `Add` agrega el elemento dentro de una lista:

```csharp
List<int> numbers = new List<int>();
numbers.Add(34);
numbers.Add(58);
numbers.Add(69);

foreach (int number in numbers)
{
    Console.WriteLine(number);
}
```

`AddRange` agrega los elementos de la colecci�n especificada al final de una lista:

```csharp
List<int> numbers = new List<int>();
numbers.Add(34);
numbers.Add(58);
numbers.Add(69);

int[] nums = new int[] { 1, 22, 44 };

numbers.AddRange(nums);

foreach (int number in numbers)
{
     Console.WriteLine(number);
}
```

`Contains` determina si un elemento existe en la lista:

```csharp
if(numbers.Contains(34))
{
     Console.WriteLine("The number 34 exists in a list");
}
```

El m�todo `IndexOf` devuelve la posici�n de un elemento como un n�mero entero. Si no se pudo encontrar un elemento, este m�todo devuelve -1:

```csharp
int index;
if((index = numbers.IndexOf(58)) != -1)
{
    Console.WriteLine($"The number 58 is on the index: {index}");
}
```

`LastIndexOf` es similar a un m�todo anterior, excepto que devuelve una �ltima aparici�n del elemento.

El m�todo `CopyTo` copia toda la colecci�n en una matriz compatible, comenzando desde el principio de esa matriz:

```csharp
int[] copyArray = new int[6];

numbers.CopyTo(copyArray);

foreach (int copyNumber in copyArray)
{
     Console.WriteLine(copyNumber);
}
```

El m�todo `Remove` elimina la primera aparici�n de un elemento espec�fico de la lista:

```csharp
numbers.Remove(69);
```

El m�todo `Clear` borra todos los elementos de una lista:

```csharp
numbers.Clear();
```

Podemos verificar cu�ntos elementos tiene una lista usando la propiedad `Count`:

```csharp
Console.WriteLine(numbers.Count);
```

## Diccionario

`Dictionary` representa una colecci�n de claves y valores. Para instanciar un objeto podemos usar la siguiente sintaxis:

```csharp
Dictionary<KeyType, ValueType> Name = new Dictionary<KeyType, ValueType>();
```

`KeyType` representa un tipo de nuestra clave en una colecci�n. `ValueType` representa el valor asignado a la clave. Entonces, podemos extraer nuestro valor de una colecci�n usando la clave dentro de los corchetes:

```csharp
DictionaryName[key];
```

Dictionary tiene varios constructores que podemos usar para crear instancias de objetos:

```csharp
Dictionary<string, int> dictExample = new Dictionary<string, int>();

Dictionary<string, int> dictExample1 = new Dictionary<string, int>(5); //to set initial size

Dictionary<string, int> dictExample2 = new Dictionary<string, int>(dictExample1); //accepts all the elements from created Key-Value collection
```

## M�todos y propiedades

El m�todo `Add` agrega el par clave-valor dentro de una colecci�n:

```csharp
Dictionary<string, int> dictExample = new Dictionary<string, int>();

dictExample.Add("First", 100);
dictExample.Add("Second", 200);
dictExample.Add("Third", 300);

foreach (var item in dictExample)
{
     Console.WriteLine(dictExample[item.Key]);
}
```

`Remove` elimina el par clave-valor de una colecci�n en funci�n de la clave especificada:

```csharp
dictExample.Remove("Second");
foreach (var item in dictExample)
{
     Console.WriteLine(dictExample[item.Key]);
}
```

`ContainsKey` determina si una colecci�n contiene una clave espec�fica.

`ContainsValue` determina si una colecci�n contiene un valor espec�fico:

```csharp
if(dictExample.ContainsKey("First"))
{
     Console.WriteLine("It contains key");
}

if(dictExample.ContainsValue(300))
{
      Console.WriteLine("It contains value");
}
```

El m�todo `Clear` elimina todos los pares clave-valor de una colecci�n:

```csharp
dictExample.Clear();
```

Si queremos contar todos nuestros elementos dentro de una colecci�n, podemos usar la propiedad `Count`. Si queremos obtener una colecci�n de contener `Keys` o contener `Values` de un diccionario, podemos usar las propiedades `Keys` y `Values`:

```csharp
Console.WriteLine(dictExample.Count);

foreach (var key in dictExample.Keys)
{
     Console.WriteLine(key);
}

foreach (var value in dictExample.Values)
{
     Console.WriteLine(value);
}
```

## Conclusi�n

En este art�culo, hemos aprendido:

- Para usar la colecci�n List <T> con sus m�todos
- Para usar un diccionario con sus m�todos y propiedades

<!--- reference style links --->
[github-shield]: https://img.shields.io/badge/-@fernandocalmet-%23181717?style=flat-square&logo=github
[github-url]: https://github.com/fernandocalmet
[kofi-shield]: https://img.shields.io/badge/-@fernandocalmet-%231DA1F2?style=flat-square&logo=kofi&logoColor=ff5f5f
[kofi-url]: https://ko-fi.com/fernandocalmet
[linkedin-shield]: https://img.shields.io/badge/-fernandocalmet-blue?style=flat-square&logo=Linkedin&logoColor=white&link=https://www.linkedin.com/in/fernandocalmet
[linkedin-url]: https://www.linkedin.com/in/fernandocalmet
[khanakat-shield]: https://img.shields.io/badge/khanakat.com-brightgreen?style=flat-square
[khanakat-url]: https://khanakat.com