# Bucles while, for y Do-While en `C#`

[![Github][github-shield]][github-url]
[![Kofi][kofi-shield]][kofi-url]
[![LinkedIn][linkedin-shield]][linkedin-url]
[![Khanakat][khanakat-shield]][khanakat-url]

## Bucle While

Mientras que el bucle es un bucle con una condici�n previa. Esto significa que primero estamos verificando una condici�n y luego, si una condici�n devuelve verdadera, ejecutamos nuestra expresi�n:

```csharp
while(condition)
{
   < expression > ;
}
```

Ejemplo 1: Cree una aplicaci�n que calcule la suma de todos los n�meros desde n hasta m (entradas de un usuario):

```csharp
class Program
{
    static void Main(string[] args)
    {
        Console.WriteLine("Enter the integer n number:");
        int n = Convert.ToInt32(Console.ReadLine());

        Console.WriteLine("Enter the integer m number");
        int m = Convert.ToInt32(Console.ReadLine());

        int sum = 0;

        while(n <= m)
        {
            sum += n;
            n++;
        }

        Console.WriteLine($"Sum from n to m is {sum}");
        Console.ReadKey();
    }
}
```

El resultado:

```bash
Enter the integer n number:
5
Enter the integer m number
25
Sum from n to m is 315
```

Entonces, expliquemos el c�digo de arriba.

Debido a que calculamos la suma de todos los n�meros desde �n� hasta �m�, necesitamos tener una variable para almacenar ese valor. Debe inicializarse con un cero al principio. Sin eso, nuestra aplicaci�n no podr� compilarse debido a que la variable de suma no est� asignada.

En un bucle while, vamos a trav�s de todos los n�meros de `n` a `m` y la adici�n de cada n�mero de la variable suma. Estamos usando esta expresi�n: `sum += n`;que es m�s corta para `sum = sum + n`;

Finalmente, necesitamos incrementar la nvariable en 1. Sin eso, tendr�amos un ciclo infinito porque el valor de la nvariable siempre ser�a menor que el valor de la `m` variable.

Deber�amos usar bucles while cuando el n�mero de iteraciones es incierto. Esto significa que podr�amos repetir la iteraci�n hasta que se cumpla alguna condici�n, pero no estamos seguros de cu�ntas iteraciones necesitar�amos para alcanzar el cumplimiento de la condici�n.

## Bucle For

For loop es otro ciclo con una condici�n previa. Usamos la siguiente sintaxis para escribirlo en C #:

```csharp
for (initialization; condition; progression;)
{
    <loop body > ;
}
```

Usamos la inicializaci�n al comienzo del ciclo y sirve para inicializar la variable con un valor. La condici�n se utiliza para determinar cu�ndo se completa el ciclo. La progresi�n es una parte en la que incrementamos o disminuimos nuestra variable inicializada en la parte de inicializaci�n. El cuerpo consta de todas las expresiones que necesitamos ejecutar siempre que la condici�n sea verdadera.

Es importante saber que el orden de ejecuci�n es: Inicializaci�n, Condici�n, Cuerpo del bucle, Progresi�n.

Ejemplo 1: Cree una aplicaci�n que calcule la suma de todos los n�meros desde n hasta m (entradas de un usuario):

```csharp
class Program
{
    static void Main(string[] args)
    {
        Console.WriteLine("Enter the integer n number:");
        int n = Convert.ToInt32(Console.ReadLine());

        Console.WriteLine("Enter the integer m number");
        int m = Convert.ToInt32(Console.ReadLine());

        int sum = 0;

        for(int i = n; i <= m; i++)
        {
            sum += i;
        }

        Console.WriteLine($"Sum from n to m is {sum}");

        Console.ReadKey();

    }
}
```

El resultado:

```bash
Enter the integer n number:
98
Enter the integer m number:
327
Sum from n to m is 48875
```

Ejemplo 2: Cree una aplicaci�n que imprima todos los n�meros enteros de n a 1:

```csharp
class Program
{
    static void Main(string[] args)
    {
        Console.WriteLine("Enter number n that is greater than 1: ");
        int n = Convert.ToInt32(Console.ReadLine());

        for (int i = n; i >= 1; i--)
        {
            Console.WriteLine(i);
        }

        Console.ReadKey();
    }
}
```

Resultado:

```bash
Enter number n that is greater than 1:
10
10
9
8
7
6
5
4
3
2
1
```

Deber�amos usar bucles for cuando sepamos cu�ntas iteraciones vamos a tener. Esto significa que si iteramos a trav�s de todos los elementos dentro de una colecci�n o tenemos un punto final para las iteraciones.

## Bucle Do While

El ciclo do-while es un ciclo con poscondici�n. Lo que esto significa es que el cuerpo del bucle se ejecuta primero y la condici�n se verifica despu�s. Eso es totalmente opuesto a los ejemplos de bucle anteriores.

Inspeccionemos la implementaci�n de este ciclo:

```csharp
do
{
    < expression > ;
} while (condition);
```

Ahora practiquemos un poco.

Ejemplo 1: Cree una aplicaci�n que calcule la suma de todos los n�meros desde n hasta m (entradas de un usuario):

```csharp
class Program
{
    static void Main(string[] args)
    {
        Console.WriteLine("Enter the integer n number:");
        int n = Convert.ToInt32(Console.ReadLine());

        Console.WriteLine("Enter the integer m number");
        int m = Convert.ToInt32(Console.ReadLine());

        int sum = 0;

        do
        {
            sum += n;
            n++;
        } while (n <= m);

        Console.WriteLine($"The sum from n to m is {sum}");
        Console.ReadKey();
    }
}
```

```bash
Enter the integer n number:
24
Enter the integer m number:
38
The sum from n to m is 465
```

Ejemplo 2: Cree una aplicaci�n que imprima la suma de todos los n�meros pares an:

```csharp
class Program
{
    static void Main(string[] args)
    {
        Console.WriteLine("Enter the upper border number n: ");
        int n = Convert.ToInt32(Console.ReadLine());

        int sum = 2;
        int startingNumber = 4;

        do
        {
            sum += startingNumber;
            startingNumber += 2;
        }while (startingNumber <= n);

        Console.WriteLine($"Sum of all the even numbers to n is {sum}");
        Console.ReadKey();
    }
}
```

```bash
Enter the upper border number n:
10
Sum of all the even numbers to n is 30
```

## Conclusi�n

Ahora podemos implementar iteraciones en combinaci�n con todo lo que hemos aprendido de los art�culos anteriores, haciendo as� nuestra aplicaci�n m�s poderosa.

<!--- reference style links --->
[github-shield]: https://img.shields.io/badge/-@fernandocalmet-%23181717?style=flat-square&logo=github
[github-url]: https://github.com/fernandocalmet
[kofi-shield]: https://img.shields.io/badge/-@fernandocalmet-%231DA1F2?style=flat-square&logo=kofi&logoColor=ff5f5f
[kofi-url]: https://ko-fi.com/fernandocalmet
[linkedin-shield]: https://img.shields.io/badge/-fernandocalmet-blue?style=flat-square&logo=Linkedin&logoColor=white&link=https://www.linkedin.com/in/fernandocalmet
[linkedin-url]: https://www.linkedin.com/in/fernandocalmet
[khanakat-shield]: https://img.shields.io/badge/khanakat.com-brightgreen?style=flat-square
[khanakat-url]: https://khanakat.com