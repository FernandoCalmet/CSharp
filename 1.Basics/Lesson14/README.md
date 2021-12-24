# Matrices en `C#`

[![Github][github-shield]][github-url]
[![Kofi][kofi-shield]][kofi-url]
[![LinkedIn][linkedin-shield]][linkedin-url]
[![Khanakat][khanakat-shield]][khanakat-url]

## Declaraci�n e inicializaci�n de matrices

Para declarar una matriz, indicamos el tipo de esa matriz, luego los corchetes y finalmente el nombre de esa matriz:

```csharp
int[] numbers;
Pen[] pens;
```

Lo importante que debe saber es que no importa si almacenamos el tipo de referencia o los datos del tipo de valor dentro de una matriz, la matriz es siempre un tipo de datos de referencia.
Para inicializar nuestras matrices, necesitamos usar una palabra clave `new`, luego el tipo de datos y finalmente los corchetes con la capacidad de la matriz dentro:

```csharp
numbers = new int[5];
pens = new Pen[5];
```

En un primer ejemplo, almacenamos el tipo `int` (tipo de valor) dentro de la matriz de n�meros, reservando as� el espacio en nuestra memoria para cinco enteros. Pero en el segundo ejemplo, estamos reservando el espacio en nuestra memoria para cinco `Pen` tipos (tipos de referencia) por lo que no estamos almacenando sus valores sino sus referencias. Todos los `Pen` valores son nulos por ahora.
Hasta ahora, solo hemos asignado la memoria para nuestros valores, en realidad no agregamos esos valores en absoluto. Entonces, para finalizar el proceso de inicializaci�n, necesitamos agregar valores a nuestras matrices. La forma m�s com�n es declarar, asignar e inicializar una matriz en una l�nea de c�digo:

```csharp
int[] arrayExample = new int[5] { 4, 5, 7, 8, 3};
Pen[] penArrayExample = new Pen[3] { new Pen(Color.Red), new Pen(Color.Green), new Pen(Color.Blue) };
```

Tambi�n podemos usar los �ndices para completar una matriz:

```csharp
int[] numbers = new int[2];
numbers[0] = 5; numbers[1] = 7;
```

## Manipulaci�n de matrices

Para manipular con una matriz, podemos usar un bucle `for`. Con un bucle for estamos usando �ndices para acceder a cada elemento de una matriz:

```csharp
static void Main(string[] args)
{
    int[] numbers = new int[5] { 4, 5, 7, 8, 3};
           
    for(int i = 0; i < numbers.Length; i++)
    {
        Console.WriteLine(numbers[i]);
    }
}
```

Podemos hacer lo mismo pero con el bucle `foreach`. La diferencia entre estos dos enfoques se debe a que con el ciclo `for` estamos usando �ndices para acceder a elementos (variable i), pero con el ciclo `foreach` no estamos usando �ndices sino los valores reales:

```csharp
static void Main(string[] args)
{
    int[] numbers = new int[5] { 4, 5, 7, 8, 3};

    foreach(int i in numbers)
    {
        Console.WriteLine(i);
    }
}
```

## Ejemplos

Ejemplo 1: Cree una aplicaci�n en la que creamos una matriz de nelementos, completamos esa matriz con n�meros enteros aleatorios y finalmente imprimimos todos esos n�meros y su suma:

```csharp
class Program
{
    //array is a reference type so every action in this method will affect original array
    public static void PopulateArray(int[] numbers)
    {
        Random r = new Random();
        for(int i = 0; i < numbers.Length; i++)
        {
            numbers[i] = r.Next(1, 101);
            Console.WriteLine($"The {i+1}. element is {numbers[i]}");
        }
    }

    public static void CalculateSum(int[] numbers)
    {
        int sum = 0;
        foreach (int i in numbers)
        {
            sum += i;
        }

        Console.WriteLine($"The sum of all the elements is {sum}");
    }

     static void Main(string[] args)
    {
        Console.WriteLine("Enter an array capacity: ");
        int capacity = Convert.ToInt32(Console.ReadLine());

        int[] numbers = new int[capacity];

        PopulateArray(numbers);
        Console.WriteLine();
        CalculateSum(numbers);

        Console.ReadKey();
    }
}
```

## Matrices de par�metros

Una matriz params nos permite pasar un n�mero variable de argumentos a un m�todo. Para crear una matriz de params debemos especificar la palabra clave `params` cuando especificamos los par�metros para nuestro m�todo:

```csharp
public static void TestMethod(params int[] numbers)
{
    //method body    
}
```

El efecto de la palabra clave `params` es que nos permite enviar cualquier n�mero de argumentos al par�metro del m�todo sin crear una matriz:

```csharp
static void Main(string[] args)
{
   TestMethod(1, 2, 3);
}
```

Aunque una matriz de params es muy �til, todav�a tenemos algunas limitaciones al trabajar con ellos:

- No podemos usar la palabra clave params para trabajar con matrices bidimensionales
- La sobrecarga de m�todos no es posible �nicamente con la palabra clave params
- No podemos especificar palabras clave ref o out con matrices params
- Una matriz de params tiene que ser el �ltimo par�metro de nuestro m�todo
- Un m�todo que no es params siempre tiene prioridad sobre los m�todos params

Ejemplo 2: Cree una aplicaci�n que imprima el m�nimo de todos los n�meros enviados al m�todo PrintMin:

```csharp
class Program
{
    public static void PrintMin(params int[] numbers)
    {
        int min = numbers[0];
        for(int i=1; i < numbers.Length; i++)
        {
            if(min > numbers[i])
            {
                min = numbers[i];
            }
        }

        Console.WriteLine(min);
    }
    static void Main(string[] args)
    {
        PrintMin(49, 58, 12, 98, 47, 13);

        Console.ReadKey();
    }
}
```

## Matriz multidimensional

Sabemos c�mo utilizar matrices unidimensionales, pero C # tambi�n admite matrices multidimensionales. En esta secci�n, hablaremos de matrices bidimensionales. �Por qu� se llaman bidimensionales?

Bueno, porque tienen dos dimensiones, filas y columnas. Para crear una matriz "2d", usamos la siguiente sintaxis:

```csharp
int[,] numbersMultiDim = new int[3, 2] { { 1, 5 }, { 3, 8 }, { 6, 1 } };
```

Con esta sintaxis, creamos una matriz bidimensional con tres filas y dos columnas. Entonces, en una presentaci�n gr�fica deber�a verse as�:

![img01](/img/01.png)

Para acceder a cualquier n�mero de esta matriz podemos utilizar la sintaxis con el nombre de la matriz y la posici�n del n�mero entre corchetes. Proporcionamos posici�n mediante �ndices. Entonces, la primera fila tiene el �ndice 0 y la �ltima tiene el �ndice (n�mero de filas - 1). Lo mismo ocurre con las columnas:

```csharp
int number = numbersMultiDim[2, 1]; // value 1    => third row on index 2 and second column on index 1
```

Para iterar a trav�s de todos los datos, podemos usar el ciclo for:

```csharp
for(int i = 0; i < numbersMultiDim.GetLength(0); i++)
{
      for(int j = 0; j < numbersMultiDim.GetLength(1); j++)
      {
          Console.WriteLine(numbersMultiDim[i,j]);
      }
}
```

Como puede ver, estamos usando dos bucles para iterar a trav�s de una matriz bidimensional. El primero es iterar a trav�s de todas las filas y el segundo a trav�s de todas las columnas de la fila actual.
Usamos matrices multidimensionales cuando tenemos que presentar nuestros datos en forma multidimensional. Espec�ficamente, utilizamos matrices bidimensionales para trabajar con los datos en forma de tabla con las filas y columnas.

## Conclusi�n

Gran trabajo. Contamos con todos los conocimientos necesarios para trabajar con arrays y utilizarlos en nuestro proceso de desarrollo.

<!--- reference style links --->
[github-shield]: https://img.shields.io/badge/-@fernandocalmet-%23181717?style=flat-square&logo=github
[github-url]: https://github.com/fernandocalmet
[kofi-shield]: https://img.shields.io/badge/-@fernandocalmet-%231DA1F2?style=flat-square&logo=kofi&logoColor=ff5f5f
[kofi-url]: https://ko-fi.com/fernandocalmet
[linkedin-shield]: https://img.shields.io/badge/-fernandocalmet-blue?style=flat-square&logo=Linkedin&logoColor=white&link=https://www.linkedin.com/in/fernandocalmet
[linkedin-url]: https://www.linkedin.com/in/fernandocalmet
[khanakat-shield]: https://img.shields.io/badge/khanakat.com-brightgreen?style=flat-square
[khanakat-url]: https://khanakat.com