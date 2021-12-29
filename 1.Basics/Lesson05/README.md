# Estructuras lineales en `C#` con entradas e impresi�n de resultados de salida

[![Github][github-shield]][github-url]
[![Kofi][kofi-shield]][kofi-url]
[![LinkedIn][linkedin-shield]][linkedin-url]
[![Khanakat][khanakat-shield]][khanakat-url]

## Imprimir la suma de dos valores enteros mediante estructuras lineales en `C#`

Ejemplo 1: Cree una aplicaci�n que imprima la suma de dos valores enteros que el usuario ingresa en la ventana de la consola.

Creemos una nueva aplicaci�n de consola y as�gnele un nombre `SumGenerator`. Luego, escriba este c�digo dentro del m�todo `Main`:

```csharp
namespace SumGenerator
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Write the first integer:");
            int first = Convert.ToInt32(Console.ReadLine());

            Console.WriteLine("Write the second integer:");
            int second = Convert.ToInt32(Console.ReadLine());

            int result = first + second;
            Console.WriteLine($"The result is {result}");

            Console.ReadKey();
        }
    }
}
```

Con la declaraci�n `Console.WriteLine()`, mostramos el mensaje en la ventana de la consola y pasamos a la siguiente l�nea. La declaraci�n `Console.ReadLine()` leer� nuestra entrada, pero es de tipo cadena y lo que necesitamos es un tipo int. Entonces, necesitamos convertirlo con la declaraci�n `Convert.ToInt32()`. Finalmente, calculamos la suma y la imprimimos. La declaraci�n `Console.ReadKey()` est� aqu� solo para mantener abierta la ventana de nuestra consola.

Presionemos F5 para iniciar nuestra aplicaci�n e ingresemos dos n�meros enteros:

```bash
Write the first integer:
5
Write the second integer:
The result is 33
```

## Uso de entradas (nombre y apellido) e impresi�n del nombre completo con estructuras lineales en `C#`

Ejemplo 2: Escriba una aplicaci�n que para dos entradas proporcionadas (nombre y apellido), imprima el nombre completo en un formato: nombre <espacio> apellido.

Creemos una nueva aplicaci�n de consola y escribamos el c�digo:

```csharp
namespace FullNameGenerator
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("What is your first name:");
            string name = Console.ReadLine();

            Console.WriteLine("What is your last name:");
            string lastName = Console.ReadLine();

            string fullName = name + " " + lastName;
            Console.WriteLine($"Your full name is: {fullName}");

            Console.ReadKey();
        }
    }
}
```

Eso es. Si ejecutamos nuestro proyecto presionando F5, veremos el resultado con el nombre y apellido, separados por espacios.

## Conclusi�n

Ahora sabemos c�mo manipular las entradas en nuestras aplicaciones y c�mo mostrar el resultado en la ventana de la consola. Adem�s, hemos utilizado la conversi�n de datos de `string` a `int` para poder sumar las entradas de un usuario.

<!--- reference style links --->
[github-shield]: https://img.shields.io/badge/-@fernandocalmet-%23181717?style=flat-square&logo=github
[github-url]: https://github.com/fernandocalmet
[kofi-shield]: https://img.shields.io/badge/-@fernandocalmet-%231DA1F2?style=flat-square&logo=kofi&logoColor=ff5f5f
[kofi-url]: https://ko-fi.com/fernandocalmet
[linkedin-shield]: https://img.shields.io/badge/-fernandocalmet-blue?style=flat-square&logo=Linkedin&logoColor=white&link=https://www.linkedin.com/in/fernandocalmet
[linkedin-url]: https://www.linkedin.com/in/fernandocalmet
[khanakat-shield]: https://img.shields.io/badge/khanakat.com-brightgreen?style=flat-square
[khanakat-url]: https://khanakat.com