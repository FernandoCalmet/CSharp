# M�todos de `C#`

[![Github][github-shield]][github-url]
[![Kofi][kofi-shield]][kofi-url]
[![LinkedIn][linkedin-shield]][linkedin-url]
[![Khanakat][khanakat-shield]][khanakat-url]

## Firmas de m�todos

Podemos declarar nuestros m�todos especificando la firma del m�todo que consiste en el modificador de acceso (p�blico, privado�), el  nombre de un m�todo y los par�metros del m�todo . Si queremos que nuestro m�todo tenga una implementaci�n, debe tener dos llaves para especificar el cuerpo del m�todo. Colocamos nuestro c�digo entre esas llaves. Adem�s, tenemos que incluir un valor de retorno (void, int, double�) para que nuestro m�todo sea v�lido. El tipo de retorno no se aplica como parte de la firma del m�todo, pero no podemos crear un m�todo sin �l. Por lo tanto, se inyecta a s� mismo en una firma (o especificaci�n).

Un m�todo que devuelve un valor debe satisfacer dos condiciones. Primero, debe especificar un `return type` antes del nombre del m�todo. El segundo, debe tener una returndeclaraci�n dentro de su cuerpo (dentro de llaves). Por otro lado, si el m�todo no devuelve nada, void se usa la palabra clave en lugar de la palabra clave return. Si ese es el caso, un m�todo no necesita tener una declaraci�n de retorno dentro de su cuerpo:

![img01](/img/01.png)

En nuestro proyecto, podemos tener dos m�todos diferentes con el mismo nombre, pero no podemos tener dos m�todos diferentes con la misma firma del m�todo. Al menos una parte de la firma del m�todo debe ser diferente. Cuando tenemos dos o m�s m�todos con el mismo nombre pero diferentes firmas, eso se llama Sobrecarga de m�todos.

## Par�metros y argumentos

En el ejemplo anterior, hemos visto que nuestros m�todos aceptan solo un par�metro. Pero podemos crear un m�todo que acepte tantos par�metros como necesitemos:

```csharp
public void WriteAllNumbers(int a, int b, int c)
{
     Console.WriteLine($"{a} {b} {c}");
}
```

Es importante que cada par�metro tenga su propio tipo, nombre y que est�n separados por comas.

Cuando creamos un m�todo en la firma, creamos par�metros (imag�nelos como marcadores de posici�n para el valor del mismo tipo). Pero, cuando llamamos a ese m�todo, estamos pasando valores reales (argumentos) para esos par�metros:

```csharp
WriteAllNumbers(15, 16, 67);
```

Ejemplo 1: Cree una aplicaci�n que imprima la suma, resta y multiplicaci�n de dos entradas:

```csharp
class Program
{
    public static void Sum(int first, int second) //method needs to be static because we are calling it in a static Main method.
    {
        int result = first + second;
        Console.WriteLine($"Sum result: {result}");
    }

    public static void Subtract(int first, int second)
    {
        int result = first - second;
        Console.WriteLine($"Substraction result: {result}");
    }

    public static void Multiplication(int first, int second)
    {
        int result = first * second;
        Console.WriteLine($"Multiplication result: {result}");
    }

    static void Main(string[] args)
    {
        Console.WriteLine("Enter the first number: ");
        int firstArgument = Convert.ToInt32(Console.ReadLine());

        Console.WriteLine("Enter the second number: ");
        int secondArgument = Convert.ToInt32(Console.ReadLine());

        Sum(firstArgument, secondArgument);
        Subtract(firstArgument, secondArgument);
        Multiplication(firstArgument, secondArgument);

        Console.ReadKey();
    }
}
```

Una vez que ejecutemos nuestra aplicaci�n, veremos el resultado:

```bash
Enter the first number:
12
Enter the second number:
10
Sum result: 22
Substraction result: 2
Multiplication result: 120
```

## Par�metros opcionales

Un par�metro opcional tiene un valor predeterminado. El m�todo que tiene par�metros opcionales podr�a llamarse sin esos argumentos. Pero tambi�n podemos proporcion�rselos. Si proporcionamos los valores como argumentos para par�metros opcionales, los valores predeterminados se anular�n:

```csharp
public static void MethodWithOptParams(int first, int second = 10)
{
    Console.WriteLine(first + second);
}

MethodWithOptParams(20); //result is 30
MethodWithOptParams(20, 35); //result is 55
```

## Conclusi�n

El uso de m�todos es muy �til, no solo en C # sino en la programaci�n en general. Entonces, tener este conocimiento es una gran ventaja. No tenga miedo de usarlos mientras codifica, har�n que su c�digo sea m�s limpio, f�cil de mantener, legible y, sobre todo, reutilizable.

<!--- reference style links --->
[github-shield]: https://img.shields.io/badge/-@fernandocalmet-%23181717?style=flat-square&logo=github
[github-url]: https://github.com/fernandocalmet
[kofi-shield]: https://img.shields.io/badge/-@fernandocalmet-%231DA1F2?style=flat-square&logo=kofi&logoColor=ff5f5f
[kofi-url]: https://ko-fi.com/fernandocalmet
[linkedin-shield]: https://img.shields.io/badge/-fernandocalmet-blue?style=flat-square&logo=Linkedin&logoColor=white&link=https://www.linkedin.com/in/fernandocalmet
[linkedin-url]: https://www.linkedin.com/in/fernandocalmet
[khanakat-shield]: https://img.shields.io/badge/khanakat.com-brightgreen?style=flat-square
[khanakat-url]: https://khanakat.com