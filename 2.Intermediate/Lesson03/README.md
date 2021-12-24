# Miembros est�ticos, constantes y m�todos de extensi�n

[![Github][github-shield]][github-url]
[![Kofi][kofi-shield]][kofi-url]
[![LinkedIn][linkedin-shield]][linkedin-url]
[![Khanakat][khanakat-shield]][khanakat-url]

## Acerca de los m�todos est�ticos

Cuando definimos un m�todo en una clase, pertenece a esa clase y todas las instancias de esa clase podr�n acceder a �l. Una clase puede tener muchos de estos m�todos. Pero hay algunos m�todos que son independientes de la instancia de clase espec�fica. Ese tipo de m�todos se denominan "m�todos est�ticos". Entonces, los m�todos est�ticos son los m�todos que no pertenecen a una instancia de una clase, pueden interactuar solo con otros elementos est�ticos y tienen la palabra clave est�tica en la descripci�n del m�todo.

Tomemos el m�todo `Sqrt()`, por ejemplo. Este m�todo calcula la ra�z cuadrada de un n�mero, y no tenemos que instanciar la clase `Math` (a la que pertenece el Sqrt) porque este m�todo es un m�todo est�tico:

```csharp
int number = 4;
Console.WriteLine(Math.Sqrt(number));
```

Entonces, �por qu� el m�todo `Sqrt` es un m�todo est�tico y no no-est�tico?

Bueno, `Sqrt` acepta solo un argumento y es suficiente para hacer su trabajo. Proporcionamos un n�mero de argumento y el m�todo devuelve una ra�z cuadrada de ese n�mero. No mencionamos la clase `Math` en absoluto. Eso es porque no tenemos que hacerlo. La clase `Math` no proporciona ning�n apoyo al m�todo `Sqrt` para que haga su trabajo. Solo proporciona un espacio para que resida el m�todo `Sqrt`.

Cuando tenemos un caso como este, suele ser una buena soluci�n crear un m�todo como uno est�tico.

## Trabajar con un m�todo est�tico

Para llamar a un m�todo est�tico, como dijimos, no necesitamos una instancia de una clase. Podemos llamarlo con la siguiente sintaxis: `ClassName.MethodName(arguments�);`

Entonces, cuando queremos usar el m�todo `Sqrt` o cualquier otro m�todo de la clase `Math`, podemos llamarlo as�: `Math.Sqrt(16);`

## Creaci�n de un campo mediante la palabra clave constante

Si prefijamos nuestro campo con la palabra clave const, podemos declarar dicho campo donde su valor nunca puede cambiar. La palabra clave `const` es la abreviatura de constante. Un miembro constante se define en tiempo de compilaci�n y no se puede modificar en tiempo de ejecuci�n.

Podemos crear una variable constante de la siguiente manera: `AccessModifier const Type Name = Value;`

![img01](/img/01.png)

## Clase est�tica

En C #, junto a los m�todos est�ticos, tambi�n podemos declarar clases est�ticas. La clase est�tica puede contener solo los miembros est�ticos. Su prop�sito es actuar como titular de los m�todos y campos de utilidad. No tiene sentido crear instancias de este tipo de clases utilizando la palabra clave `new`. Adem�s, no podemos hacer eso en absoluto. Pero podemos crear un constructor predeterminado siempre que sea est�tico. Cualquier otro tipo de constructor es ilegal:

```csharp
public static class TestClass
{
    private static int number;

    static TestClass()
    {
        number = 54;
    }
 }
```

## Acerca de los m�todos de extensi�n y c�mo usarlos

Supongamos que queremos agregar una nueva caracter�stica al tipo `string`, por ejemplo, la funcionalidad `FirstLetterUpperCase` que siempre hace que la primera letra de una cadena est� en may�sculas. Podemos escribir un m�todo normal para ese prop�sito:

```csharp
public static string FirstLetterUpperCase(string word)
{
     char letter = Char.ToUpper(word[0]);
     string remaining = word.Substring(1);

     return letter + remaining;
}

static void Main(string[] args)
{
     string word = "football";
     string newWord = FirstLetterUpperCase(word);
}
```

Pero, como podemos ver, necesitamos enviar una palabra como par�metro cada vez y aceptar el valor devuelto cada vez tambi�n. Este no es el enfoque equivocado, pero podemos hacerlo a�n mejor. Ah� es donde entran los m�todos de extensi�n.

Un m�todo de extensi�n nos permite extender un tipo existente con m�todos est�ticos adicionales. Debemos crear ese tipo de m�todos dentro de una clase est�tica y tienen el primer par�metro prefijado con la palabra clave `this`.

Pero, �por qu� tenemos que colocar un prefijo delante del primer par�metro?

Porque ese par�metro es un indicador que le dice al compilador qu� tipo extendemos.

As� que aqu� est� el ejemplo anterior pero con el m�todo de extensi�n:

```csharp
public static class StringExtensions
{
    public static string FirstLetterUpperCase(this string word)
    {
        char letter = Char.ToUpper(word[0]);
        string remaining = word.Substring(1);

        return letter + remaining;
    }
}

class Program
{
    static void Main(string[] args)
    {
        string word = "football"
                      .FirstLetterUpperCase();

        Console.WriteLine(word);
        Console.ReadKey();
    }
}
```

## Conclusi�n

Hemos terminado con los miembros est�ticos y ahora tenemos una gran herramienta en nuestra caja de herramientas que podemos usar mientras desarrollamos nuestras aplicaciones C #.

En este art�culo, hemos aprendido:

- C�mo usar clases est�ticas
- La forma de usar m�todos est�ticos.
- C�mo crear m�todos de extensi�n
- Acerca de las palabras clave const y la creaci�n de constantes

<!--- reference style links --->
[github-shield]: https://img.shields.io/badge/-@fernandocalmet-%23181717?style=flat-square&logo=github
[github-url]: https://github.com/fernandocalmet
[kofi-shield]: https://img.shields.io/badge/-@fernandocalmet-%231DA1F2?style=flat-square&logo=kofi&logoColor=ff5f5f
[kofi-url]: https://ko-fi.com/fernandocalmet
[linkedin-shield]: https://img.shields.io/badge/-fernandocalmet-blue?style=flat-square&logo=Linkedin&logoColor=white&link=https://www.linkedin.com/in/fernandocalmet
[linkedin-url]: https://www.linkedin.com/in/fernandocalmet
[khanakat-shield]: https://img.shields.io/badge/khanakat.com-brightgreen?style=flat-square
[khanakat-url]: https://khanakat.com