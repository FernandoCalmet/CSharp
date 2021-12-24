# Trabajar con cadenas en `C#`: m�todos de cadena

[![Github][github-shield]][github-url]
[![Kofi][kofi-shield]][kofi-url]
[![LinkedIn][linkedin-shield]][linkedin-url]
[![Khanakat][khanakat-shield]][khanakat-url]

## M�todos de cadena Substring, IndexOf, LastIndexOf en `C#`

Substring (int startIndex) es el m�todo que devuelve parte de la cadena desde `startIndex` el final de la cadena.

Substring (int startIndex, int length) es el m�todo que devuelve parte de la cadena con una longitud definida de `startIndex`.

Veamos esto en la pr�ctica:

```csharp
class Program
{
    static void Main(string[] args)
    {
        string testString = "this is some string to use it for our example.";

        string partWithoutLength = testString.Substring(10);
        string partWithLength = testString.Substring(5, 10);

        Console.WriteLine(partWithoutLength);
        Console.WriteLine(partWithLength);

        Console.ReadKey();
    }
}
```

IndexOf () es el m�todo que devuelve la posici�n del valor entero de la primera aparici�n del car�cter, o una cadena en la cadena seleccionada. Si ese valor no existe, el m�todo devolver� -1.

Hay diferentes sobrecargas de este m�todo: `IndexOf(char value)`, `IndexOf(string value)`, `IndexOf(char value, int startIndex)`, `IndexOf(string value, int startIndex)` etc. Si utilizamos este m�todo con el startIndexpar�metro, no vamos a buscar desde el principio de la cadena, pero desde esa posici�n hasta el final:

```csharp
int charPosition = testString.IndexOf('i');
int stringPosition = testString.IndexOf("some");
int charPosWithStartIndex = testString.IndexOf('s', 10);
int stringPosWithStartIndex = testString.IndexOf("some", 10);
```

`LastIndexOf()` es el m�todo que devuelve la posici�n de la �ltima aparici�n de un car�cter o un valor de cadena. Este m�todo tiene las mismas sobrecargas que el `IndexOf` m�todo:

```csharp
int lastPosition = testString.LastIndexOf('o');
int stringLastPosition = testString.LastIndexOf("is");
```

## Contiene, comienza con, termina con

Contiene (valor de cadena) es el m�todo que devuelve verdadero si una cadena contiene el valor; de lo contrario, devolver� falso:

StartsWith (valor de cadena) es el m�todo que devuelve verdadero si una cadena comienza con el valor; de lo contrario, devuelve falso. A diferencia de este m�todo, el m�todo EndsWith (valor de cadena) devuelve verdadero si una cadena termina con el valor; de lo contrario, devuelve falso:

## Quitar, insertar

El m�todo `Remove(int startIndex)` elimina los caracteres de la cadena desde la `startIndex` posici�n hasta el final de la cadena y devuelve esa nueva cadena. Hay un m�todo sobrecargado `Remove(int startIndex, int count) que elimina un n�mero espec�fico de caracteres de la cadena desde la posici�n del �ndice inicial. Con el par�metro de conteo decidimos cu�ntos caracteres queremos eliminar:

```csharp
string loweredString = testString.Remove(10);
string loweredStringWithCount = testString.Remove(10, 9);
```

`Insert(int startIndex, string value)` es el m�todo que inserta el valor en la cadena desde la `startIndex` posici�n y devuelve una cadena modificada:

```csharp
string stringWithInsert = testString.Insert(13, "UPDATED ");
```

## ToLower, ToUpper

`ToLower()` devuelve una nueva cadena con todas las letras min�sculas:

```csharp
string upperCaseString = testString.ToUpper();
```

## Ejemplos de uso de m�todos de cadena en `C#`

Ejemplo 1: Cree una aplicaci�n que acepte el nombre y el apellido, separados por espacios, como entrada, y luego imprima el nombre en una fila y el apellido en otra fila:

```csharp
class Program
{
    static void Main(string[] args)
    {
        Console.WriteLine("Enter your full name, blank space separated");
        string fullName = Console.ReadLine();

        int blankPosition = fullName.IndexOf(' ');
        string name = fullName.Substring(0, blankPosition);
        string lastName = fullName.Substring(blankPosition + 1);

        Console.WriteLine(name);
        Console.WriteLine(lastName);

        Console.ReadKey();
    }
}
```

Ejemplo 2: Cree una aplicaci�n que acepte como entrada una oraci�n y elimine la primera y la �ltima palabra de esa oraci�n:

```csharp
class Program
{
    static void Main(string[] args)
    {
        Console.WriteLine("Enter your sentence: ");

        string sentence = Console.ReadLine();

        int firstBlankPosition = sentence.IndexOf(' ');
            
        string withoutFirstWord = sentence.Remove(0, firstBlankPosition + 1);

        int lastBlankPosition = withoutFirstWord.LastIndexOf(' ');

        string withoutFirstAndLast = withoutFirstWord.Remove(lastBlankPosition);

        Console.WriteLine(withoutFirstAndLast);

        Console.ReadKey();
    }
}
```

Este es el resultado:

```bash
Enter your sentence:
This is a new sentence with several words.
is a new sentence with several
```

## Conclusi�n

Hemos dominado el uso de los m�todos de cadena m�s utilizados en C #. Con la combinaci�n de estos m�todos, podemos crear soluciones poderosas para nuestras aplicaciones.

<!--- reference style links --->
[github-shield]: https://img.shields.io/badge/-@fernandocalmet-%23181717?style=flat-square&logo=github
[github-url]: https://github.com/fernandocalmet
[kofi-shield]: https://img.shields.io/badge/-@fernandocalmet-%231DA1F2?style=flat-square&logo=kofi&logoColor=ff5f5f
[kofi-url]: https://ko-fi.com/fernandocalmet
[linkedin-shield]: https://img.shields.io/badge/-fernandocalmet-blue?style=flat-square&logo=Linkedin&logoColor=white&link=https://www.linkedin.com/in/fernandocalmet
[linkedin-url]: https://www.linkedin.com/in/fernandocalmet
[khanakat-shield]: https://img.shields.io/badge/khanakat.com-brightgreen?style=flat-square
[khanakat-url]: https://khanakat.com