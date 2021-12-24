# Condiciones en C # con instrucciones If-Else y Switch-Case

[![Github][github-shield]][github-url]
[![Kofi][kofi-shield]][kofi-url]
[![LinkedIn][linkedin-shield]][linkedin-url]
[![Khanakat][khanakat-shield]][khanakat-url]

## Condiciones b�sicas en `C#`

Si queremos ejecutar alguna expresi�n pero solo si se cumple alguna condici�n, entonces necesitamos usar declaraciones condicionales. Para crear una declaraci�n de este tipo, necesitamos usar `if` y `else` palabras clave:

```csharp
if (condition)
{
    < expression1 > ;
}
else
{
    < expression2 > ;
}
```

La condici�n es una expresi�n l�gica que puede dar como resultado verdadero o falso. Si es cierto `<expression1>`, se ejecutar�; de lo contrario, `<expression2>` se ejecutar�. Despu�s de cada expresi�n, debemos colocar el `;` signo.

Podemos ejecutar m�s expresiones si la condici�n es verdadera o falsa:

```csharp
if (condition)
{
    < expression1 > ;
    < expression2 > ;
}
else
{
    < expression3 > ;
    < expression4 > ;
}
```

Ejemplo 1: Cree una aplicaci�n que determine la mayor cantidad de dos entradas enteras:

```csharp
class Program
{
    static void Main(string[] args)
    {
        Console.WriteLine("Enter the first number: ");
        int first = Convert.ToInt32(Console.ReadLine());
    
        Console.WriteLine("Enter the second number: ");
        int second = Convert.ToInt32(Console.ReadLine());

        if(first > second)
        {
            Console.WriteLine($"The greater number is {first}");
        }
        else
        {
            Console.WriteLine($"The greater number is {second}");
        }

       Console.ReadKey();
    }
} 
```

El resultado:

```bash
Enter the first number:
92
Enter the second number:
36
The greater number is 92
```

No tenemos que usar solo palabras clave `if` y `else` en declaraciones condicionales, podemos agregar otra condici�n agregando la `else if` parte del bloque:

```csharp
if(condition1)
{
    < expression 1 > ;
}
else if(condition 2)
{
    < expression 2 > ;
}
else if(condition n)
{
    <expression n>
}
else
{
    < expression k > ;
}
```

Ejemplo 2: Cree una aplicaci�n que tome cualquier cadena y el color de la fuente (r para rojo, g para verde, o para otros) como entradas. Luego necesita imprimir esa cadena con el color seleccionado:

```csharp
class Program
{
    static void Main(string[] args)
    {
        Console.WriteLine("Enter your random string: ");
        string sentence = Console.ReadLine();

        Console.WriteLine("Choose your color: r for Red, g for Green, o for Other");
        char color = Convert.ToChar(Console.ReadLine());

        if(color == 'r')
        {
            Console.ForegroundColor = ConsoleColor.Red;
            Console.WriteLine(sentence);
        }
        else if(color == 'g')
        {
            Console.ForegroundColor = ConsoleColor.Green;
            Console.WriteLine(sentence);
        }
        else
        {
            Console.ForegroundColor = ConsoleColor.Blue;
            Console.WriteLine(sentence);
        }

        Console.ReadKey();
    }
}
```

```bash
Enter your random string:
This is my random string
Choose your color: r for Red, g for Green, o for Other g
This is my random string
```

## Condiciones anidadas en `C#`

En C #, podemos escribir una declaraci�n condicional dentro de una declaraci�n condicional si ese es uno de los requisitos de nuestro proyecto. Entonces, la sintaxis base se ve as�:

```csharp
if (condition)
{
    if (condition2)
    {
        < expression1 > ;
    }
    else
    {
        < expression2 > ;
    }
}
else
{
    < expression3 > ;
}
```

A pesar de que podemos crear declaraciones condicionales anidadas, no las recomendamos mucho, porque dar�a lugar a una baja legibilidad.

Ejemplo 3: Cree una aplicaci�n en la que el usuario ingrese un n�mero entre 1 y 100. Si el n�mero es menor que 50, nuestra aplicaci�n generar� una multiplicaci�n por 5. Pero si un n�mero es mayor que 50, la aplicaci�n de n�meros pares generar� una multiplicaci�n. por 2 y para un n�mero impar, la aplicaci�n generar� una multiplicaci�n por 3:

```csharp
class Program
{
    static void Main(string[] args)
    {
        Console.WriteLine("Enter your number: ");
        int number = Convert.ToInt32(Console.ReadLine());

        if (number > 50)
        {
            if(number % 2 == 0) //reminder in division with two for even numbers is always a zero.
            {
                Console.WriteLine(number * 2);
            }
            else
            {
                Console.WriteLine(number * 3);
            }
        }
        else
        {
            Console.WriteLine(number * 5);
        }

         Console.ReadKey();
    }
}
```

El resultado:

```bash
Enter your number:
68
136
```

## Declaraciones de casos conmutados

En una situaci�n en la que necesitamos m�s de una o dos condiciones para ejecutar alguna expresi�n, el uso de ramificaciones m�ltiples podr�a ser una ventaja. Para usar m�ltiples ramificaciones en C #, necesitamos usar `switch` y `case` palabras clave:

```csharp
switch (expression)
{
    case value1:
       <expression 1> ;
       break;
    case value2:
       <expression 2> ;
       break;
    default:
       < expression3>;
       break;
}
```

Ejemplo 4: Cree una aplicaci�n que acepte el n�mero del mes como entrada e imprima el n�mero de d�as de ese mes:

```csharp
static void Main(string[] args)
{
    Console.WriteLine("Enter the month number from 1 to 12");
    int month = Convert.ToInt32(Console.ReadLine());

    switch (month)
    {
        case 1: case 3: case 5:
        case 7: case 8:
        case 10: case 12:
           Console.WriteLine("Number of days is 31");
            break;
        case 4: case 6:
        case 9: case 11:
            Console.WriteLine("Number of days is 30");
            break;
        case 2:
            Console.WriteLine("Number of days is 28 or 29");
            break;
        default:
            Console.WriteLine("Your number is not between 1 and 12");
            break;
    }

    Console.ReadKey();
}
```

El resultado:

````bash
Enter the month number form 1 to 12
9
Number of days is 30
```

## Conclusi�n

Con este conocimiento, podemos crear estructuras condicionales en nuestro c�digo y tomar decisiones en funci�n de si las condiciones son verdaderas o falsas.

<!--- reference style links --->
[github-shield]: https://img.shields.io/badge/-@fernandocalmet-%23181717?style=flat-square&logo=github
[github-url]: https://github.com/fernandocalmet
[kofi-shield]: https://img.shields.io/badge/-@fernandocalmet-%231DA1F2?style=flat-square&logo=kofi&logoColor=ff5f5f
[kofi-url]: https://ko-fi.com/fernandocalmet
[linkedin-shield]: https://img.shields.io/badge/-fernandocalmet-blue?style=flat-square&logo=Linkedin&logoColor=white&link=https://www.linkedin.com/in/fernandocalmet
[linkedin-url]: https://www.linkedin.com/in/fernandocalmet
[khanakat-shield]: https://img.shields.io/badge/khanakat.com-brightgreen?style=flat-square
[khanakat-url]: https://khanakat.com