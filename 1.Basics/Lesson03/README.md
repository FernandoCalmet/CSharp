# Operadores en ``C#``

[![Github][github-shield]][github-url]
[![Kofi][kofi-shield]][kofi-url]
[![LinkedIn][linkedin-shield]][linkedin-url]
[![Khanakat][khanakat-shield]][khanakat-url]

## Tipo de operadores en ``C#``

Los operadores m�s utilizados en C# son:

![img01](img/01.png)

## Operadores aritm�ticos en ``C#``

Los operadores aritm�ticos se definen para todos los tipos de datos num�ricos. Los operadores +, -, *, / representan las operaciones aritm�ticas binarias b�sicas (suma, resta, multiplicaci�n y divisi�n). El porcentaje de operador es el resto despu�s de la divisi�n.

Lo importante a tener en cuenta es que el operador + se comporta de manera diferente con los tipos de n�meros y cadenas. Con los n�meros, el resultado de la expresi�n 5 + 5 es 10. Pero con las cadenas, el resultado de la expresi�n "5" + "5" es "55". Entonces, con el tipo de n�mero, es un operador de suma, pero con el tipo de cadena, es un operador de concatenaci�n.

## Operadores relacionales en ``C#``

Todos los operadores relacionales devuelven un resultado verdadero o falso. Se utilizan para comparar expresiones o variables de ambos lados del operador relacional. Estos operadores tienen una prioridad menor que los aritm�ticos. Entonces, en el siguiente ejemplo: x*a-8*b>y+5*z;el lado izquierdo del operador mayor que se ha calculado primero, luego el lado derecho y luego se comparan.

Para las variables de tipo valor y las cadenas, el ==operador (igualdad) devolver� verdadero solo si son iguales; de lo contrario, devolver� falso. Pero si las variables son tipos de referencia, el ==operador devolver� verdadero solo si esas dos variables apuntan a la misma ubicaci�n de memoria; de lo contrario, devolver� falso.

Veamos esto a trav�s de un ejemplo:

```csharp
class Program
{
    static void Main(string[] args)
    {
        int a = 15;
        int b = 15;

        string s1 = "This is a string";
        string s2 = "This is a string";

        Student student1 = new Student("John", 25);
        Student student2 = new Student("John", 25);
    }
}
```

Si colocamos un punto de interrupci�n en nuestro c�digo e inspeccionamos el resultado usando la ventana Ver:

![img02](img/02.png)

Vemos eso `a` y `b` son iguales al igual que los `s1` y `s2`. Pero los `student1` y `student2` no son iguales porque apuntan a diferentes ubicaciones de memoria. Pero si creamos otra variable de tipo `Student` y le asignamos el valor de student1 variable, el `==` operador devolver� verdadero:

```csharp
Student student1 = new Student("John", 25);
Student student2 = new Student("John", 25);

Student student3 = student1;
```

![img03](img/03.png)

## Operadores logicos

Los operadores l�gicos `&&` (y) y `||` (o) sirven para conectar valores l�gicos. La expresi�n `<expression1>&&<expression2>` es verdadera solo si ambas expresiones son verdaderas. La expresi�n `<expression1>||<expression2>` es falsa solo si ambas expresiones son falsas; de lo contrario, es verdadera.

El `!` operador (negaci�n) niega el valor l�gico al que se aplica. Tiene la m�xima prioridad de todos los operadores mencionados. Por lo tanto, la expresi�n `!logicalValue` ser� falsa solo si logicValue es verdadero y viceversa.

Veamos esto con un ejemplo:

```csharp
class Program
{
    static void Main(string[] args)
    {
        int a = 14;
        int b = 30;
        int c = 20;

        if(a < b && a < c)
        {
            Console.WriteLine($"min number is {a}");
        }

        if(a < b || a < c)
        {
            Console.WriteLine("The a variable is smaller then b or c");
        }

        if(!(a > b))
        {
            Console.WriteLine("a is less than b");
        }
    }
}
```

## Operadores de incremento y decremento

En el lenguaje C #, podemos usar operadores que aumentan y disminuyen el valor de la variable en 1. Esos operadores son `++` y `--`, y son muy �tiles en muchos casos. Entonces, la mejor forma de escribir este c�digo:

```csharp
static void Main(string[] args)
{
     int a = 15;
     a = a + 1; //now it is 16
}
```

Ser�a:

```csharp
static void Main(string[] args)
{
    int a = 15;
    a++; //now it is 16
}
```

Lo mismo se aplica al `--` operador.

Estos dos operadores tienen la notaci�n de prefijo: `--variable`, `++variable` y las notaciones de sufijo: `variable--`, `variable++`. Aunque ambas notaciones cambiar�n el valor en 1, el resultado ser� diferente. Esto es m�s f�cil de explicar con un ejemplo:

```csharp
class Program
{
    static void Main(string[] args)
    {
        int a = 15;
        int b = --a;

        int c = 20;
        int d = c--;
    }
}
```

![img04](img/04.png)

Lo que podemos notar es que la notaci�n de prefijo disminuye el valor de la `a` variable primero y luego asigna ese valor a la `b` variable. Pero la expresi�n con notaci�n de sufijo es diferente. El valor de la `c` variable se asigna `d` primero a la variable y luego se reduce en 1.

Lo mismo se aplica al operador de incremento:

```csharp
class Program
{
    static void Main(string[] args)
    {
        int a = 15;
        int b = ++a;

        int c = 20;
        int d = c++;
    }
}
```

![img05](img/05.png)

## Conclusi�n

Excelente. Ahora tenemos m�s conocimiento sobre los operadores en C#.

<!--- reference style links --->
[github-shield]: https://img.shields.io/badge/-@fernandocalmet-%23181717?style=flat-square&logo=github
[github-url]: https://github.com/fernandocalmet
[kofi-shield]: https://img.shields.io/badge/-@fernandocalmet-%231DA1F2?style=flat-square&logo=kofi&logoColor=ff5f5f
[kofi-url]: https://ko-fi.com/fernandocalmet
[linkedin-shield]: https://img.shields.io/badge/-fernandocalmet-blue?style=flat-square&logo=Linkedin&logoColor=white&link=https://www.linkedin.com/in/fernandocalmet
[linkedin-url]: https://www.linkedin.com/in/fernandocalmet
[khanakat-shield]: https://img.shields.io/badge/khanakat.com-brightgreen?style=flat-square
[khanakat-url]: https://khanakat.com