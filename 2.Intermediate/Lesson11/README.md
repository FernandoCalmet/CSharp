# Cola, pila, tabla hash

[![Github][github-shield]][github-url]
[![Kofi][kofi-shield]][kofi-url]
[![LinkedIn][linkedin-shield]][linkedin-url]
[![Khanakat][khanakat-shield]][khanakat-url]

## Colecci�n de cola

La colecci�n `queue` representa una colecci�n de objetos primero en entrar, primero en salir. Esto significa que podemos colocar nuestros objetos en una colecci�n de cola en un orden determinado y eliminar esos objetos en el mismo orden. Entonces, el primer objeto que entra es el primer objeto que sale.

Para crear una instancia de objeto de una colecci�n `queue`, podemos usar dos declaraciones diferentes.

Usando el espacio de nombres `System.Collection.Generic`:

```csharp
Queue<int> intCollection = new Queue<int>();
```

Y al usar el espacio de nombres `System.Collection`:

```csharp
Queue queueCollection = new Queue();
```

Si declaramos un objeto proporcionando un tipo (en nuestro ejemplo, un int), podemos almacenar solo n�meros enteros en su interior. Por otro lado, si usamos el segundo ejemplo podemos almacenar diferentes tipos de datos en una colecci�n porque almacena objetos.

## Los m�todos y propiedades m�s comunes

El Enqueuem�todo agrega un elemento dentro de una colecci�n:

```csharp
Queue queueCollection = new Queue();
queueCollection.Enqueue(54);
queueCollection.Enqueue("John");
queueCollection.Enqueue(54.10);

foreach (var item in queueCollection)
{
      Console.WriteLine(item);
}
```

Cuando queremos eliminar un elemento al principio de la colecci�n y devolverlo, vamos a utilizar el m�todo `Dequeue`:

```csharp
Queue queueCollection1 = new Queue();
queueCollection1.Enqueue(54);
queueCollection1.Enqueue("John");
queueCollection1.Enqueue(54.10);

int number = Convert.ToInt32(queueCollection1.Dequeue());
Console.WriteLine($"Removed element is: {number}");
Console.WriteLine();

foreach (var item in queueCollection1)
{
    Console.WriteLine(item);
}
```

El m�todo `Peek` devuelve el elemento al principio de la colecci�n pero no lo elimina:

```csharp
Queue queueCollection2 = new Queue();
queueCollection2.Enqueue(54);
queueCollection2.Enqueue("John");
queueCollection2.Enqueue(54.10);
            
int peekNumber = Convert.ToInt32(queueCollection2.Peek());
Console.WriteLine($"Returned element is: {number}");
Console.WriteLine();

foreach (var item in queueCollection2)
{
    Console.WriteLine(item);
}
```

El m�todo `Clear` elimina todos los elementos de una colecci�n.

Si queremos comprobar cu�ntos elementos tenemos dentro de una colecci�n, podemos usar la propiedad `Count`:

```csharp
queueCollection2.Clear();
Console.WriteLine(queueCollection2.Count);
```

## Colecci�n Stack

Una colecci�n `stack`representa una colecci�n simple de �ltimo en entrar, primero en salir. Significa que un elemento que entre primero en una colecci�n saldr� en �ltimo lugar.

Al igual que con una colecci�n `Queue`, podemos usar los espacios de nombres `System.Collection` y `System.Collection.Generic`:

```csharp
Stack stack = new Stack();
Stack<int> stackInt = new Stack<int>();
```

## Propiedades y m�todos relacionados

El m�todo `Push` inserta un objeto en la parte superior de la colecci�n:

```csharp
Stack stack1 = new Stack();
stack1.Push(328);
stack1.Push("Fifty Five");
stack1.Push(124.87);

foreach (var item in stackCollection1)
{
    Console.WriteLine(item);
}
```

`Pop` elimina el elemento que se incluy� en �ltimo lugar en una colecci�n y lo devuelve:

```csharp
Stack stackCollection2 = new Stack();
stackCollection2.Push(328);
stackCollection2.Push("Fifty Five");
stackCollection2.Push(124.87);

double number = Convert.ToDouble(stackCollection2.Pop());
Console.WriteLine($"Element removed from a collection is: {number}");

foreach (var item in stackCollection2)
{
    Console.WriteLine(item);
}
```

`Peek` devuelve un objeto listo para salir de la colecci�n, pero no lo elimina:

```csharp
Stack stackCollection3 = new Stack();
stackCollection3.Push(328);
stackCollection3.Push("Fifty Five");
stackCollection3.Push(124.87);

double number1 = Convert.ToDouble(stackCollection3.Peek());
Console.WriteLine($"Element returned from a collection is: {number}");

foreach (var item in stackCollection3)
{
    Console.WriteLine(item);
}
```

Para eliminar todos los objetos de una colecci�n, usamos el m�todo `Clear`.

Si queremos contar el n�mero de elementos, usamos la propiedad `Count`:

```csharp
stackCollection3.Clear();
Console.WriteLine(stackCollection3.Count);
```

## Hash Table

Hashtable representa una colecci�n de un par clave-valor que se organiza en funci�n del c�digo hash de la clave. De manera diferente, de las colecciones de cola y pila, podemos instanciar un objeto de tabla hash usando el �nico sespacio de nombres `System.Collection` :

```csharp
Hashtable hashTable = new Hashtable();
```

El constructor de Hashtable tiene quince constructores sobrecargados.

## M�todos comunes en la colecci�n Hashtable

El m�todo `Add` agrega un elemento con la clave y el valor especificados a la colecci�n:

```csharp
Hashtable hashTable = new Hashtable();
hashTable.Add(Element.First, 174);
hashTable.Add(Element.Second, "Sixty");
hashTable.Add(Element.Third, 124.24);
foreach (var key in hashTable.Keys)
{
    Console.WriteLine($"Key: {key}, value: {hashTable[key]}");
}
```

El m�todo `Remove` elimina el elemento con la clave especificada de una colecci�n:

```csharp
Hashtable hashTable1 = new Hashtable();
hashTable1.Add(Element.First, 174);
hashTable1.Add(Element.Second, "Sixty");
hashTable1.Add(Element.Third, 124.24);

hashTable1.Remove(Element.Second);

foreach (var key in hashTable1.Keys)
{
    Console.WriteLine($"Key: {key}, value: {hashTable[key]}");
}
```

`ContainsKey` determina si una colecci�n contiene una clave espec�fica:

```csharp
if (hashTable.ContainsKey(Element.Second))
{
      Console.WriteLine($"Collection contains key: {Element.Second} and its value is {hashTable[Element.Second]}");
}
```

El m�todo `ContainsValue` determina si una colecci�n contiene un valor espec�fico.

`Clear` elimina todos los elementos de una colecci�n:

```csharp
hashTable.Clear();
```

## Propiedades comunes en la colecci�n Hashtable

La propiedad `Count` cuenta el n�mero de elementos dentro de una colecci�n:

```csharp
Console.WriteLine(hashTable.Count);
```

La propiedad `Keys` devuelve todas las claves de una colecci�n y la propiedad `Value` devuelve todos los valores de una colecci�n:

```csharp
Hashtable hashTable2 = new Hashtable();
hashTable2.Add(Element.First, 174);
hashTable2.Add(Element.Second, "Sixty");
hashTable2.Add(Element.Third, 124.24);

var keys = hashTable2.Keys;
foreach (var key in keys)
{
     Console.WriteLine(key);
}
Console.WriteLine();

var values = hashTable2.Values;
foreach (var value in values)
{
     Console.WriteLine(value);
}
```

## Conclusi�n

En este art�culo, hemos aprendido:

- Para usar la colecci�n Queue con sus m�todos
- Para usar la colecci�n Stack con sus m�todos
- C�mo utilizar la colecci�n Hashtable con sus m�todos

<!--- reference style links --->
[github-shield]: https://img.shields.io/badge/-@fernandocalmet-%23181717?style=flat-square&logo=github
[github-url]: https://github.com/fernandocalmet
[kofi-shield]: https://img.shields.io/badge/-@fernandocalmet-%231DA1F2?style=flat-square&logo=kofi&logoColor=ff5f5f
[kofi-url]: https://ko-fi.com/fernandocalmet
[linkedin-shield]: https://img.shields.io/badge/-fernandocalmet-blue?style=flat-square&logo=Linkedin&logoColor=white&link=https://www.linkedin.com/in/fernandocalmet
[linkedin-url]: https://www.linkedin.com/in/fernandocalmet
[khanakat-shield]: https://img.shields.io/badge/khanakat.com-brightgreen?style=flat-square
[khanakat-url]: https://khanakat.com