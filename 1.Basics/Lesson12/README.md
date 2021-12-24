# Palabras clave de referencia y salida en `C#`

[![Github][github-shield]][github-url]
[![Kofi][kofi-shield]][kofi-url]
[![LinkedIn][linkedin-shield]][linkedin-url]
[![Khanakat][khanakat-shield]][khanakat-url]

## �Por qu� es importante el tipo de argumento aqu�?

Bueno, cuando pasamos el argumento de tipo int, double, decimal, etc. (tipos de valor b�sico), no pasamos el valor real sino su copia. Esto significa que nuestros valores originales no se cambian dentro de los m�todos, porque pasamos una nueva copia del valor original. Como resultado, todas las operaciones dentro de un m�todo se ejecutan sobre el valor de copia.

Podemos mostrar esto en un ejemplo:

```csharp
class Program
{
    public static void ChangeAndWrite(int number)
    {
        number = 10;
        Console.WriteLine($"Inside ChangeAndWrite method, number value is: {number}");
    }
    static void Main(string[] args)
    {
        int number = 5;
        Console.WriteLine($"Value of the number prior to ChangeAndWrite call is: {number}");

        ChangeAndWrite(number);
        Console.WriteLine($"Value of the number after the ChangeAndWrite call is: {number}");

        Console.ReadKey();
    }
}
```

Como podemos ver, el valor de la variable num�rica cambia solo dentro del m�todo `ChangeAndWrite`. Pero el valor original es el mismo que antes de llamar al m�todo `ChangeAndWrite`. Y nuevamente, esto se debe a que estamos pasando la copia exacta del valor original.

## Uso de palabras clave de referencia y de salida

Podemos cambiar este comportamiento predeterminado. Si queremos cambiar los valores originales dentro de nuestros m�todos, podemos hacerlo usando palabras clave `ref` y outdentro de la firma del m�todo y tambi�n dentro de la llamada al m�todo.

Podemos usar la palabra clave `ref` solo si la variable que usamos como argumento se inicializa antes de llamar a un m�todo. Al usar la outpalabra clave, no tenemos que inicializar una variable antes de llamar a un m�todo, pero debemos inicializarla dentro de un m�todo.

Entonces, simplifiquemos eso. Si queremos cambiar un valor existente de una variable dentro de un m�todo, usaremos la palabra clave `ref`. Pero, si queremos asignar un valor completamente nuevo a la variable dentro de un m�todo, usamos la palabra clave `out`.

# Ejemplo 1 para el tipo de valor

En el ejemplo anterior, vimos c�mo se comportan las variables de tipo de valor si no usamos las palabras clave ref o out. En este, veremos el comportamiento de las variables de tipo valor cuando usamos esas palabras clave:

```csharp
class Program
{
    public static void ChangeRef(ref int numberRef)
    {
        numberRef = 25;
        Console.WriteLine($"Inside the ChangeRef method the numberRef is {numberRef}");
    }

    public static void ChangeOut( out int numberOut)
    {
        numberOut = 60;
        Console.WriteLine($"Inside the ChangeOut method the numberOut is {numberOut}");
    }
    static void Main(string[] args)
    {
        int numberRef = 15;
 
        Console.WriteLine($"Before calling the ChangeRef method the numberRef is {numberRef}");
        ChangeRef(ref numberRef);
        Console.WriteLine($"After calling the ChangeRef method the numberRef is {numberRef}");

        Console.WriteLine();

        int numberOut;
        Console.WriteLine("Before calling the ChangeOut method the numberOut is unassigned");
        ChangeOut(out numberOut);
        Console.WriteLine($"After calling the ChangeOut method the numberOut is {numberOut}");

        Console.ReadKey();
    }
}
```

Todo esto est� bastante claro. Si usamos `ref` la palabra clave `out` o en la variable de tipo de valor, su valor original cambiar�. Pero la diferencia es que con la palabra clave `out` podemos usar variables no asignadas.

## Ejemplo 2 para el tipo de referencia

Hemos aprendido que el tipo de referencia no almacena su valor dentro de su propia ubicaci�n de memoria. Almacena la direcci�n hacia la ubicaci�n de la memoria donde se almacena el valor. Por lo tanto, cuando enviamos un argumento como tipo de referencia al m�todo y cambiamos ese par�metro, se cambia el valor original. Esto se debe a que no estamos enviando la copia del valor sino la copia de la direcci�n que apunta al valor original. Esto es lo mismo que cuando usamos la palabra clave ref con los tipos de valor.

A�n as�, podemos usar la palabra clave ref con los tipos de referencia si queremos crear un nuevo objeto con la misma direcci�n.

Veamos todo esto en un ejemplo:

```csharp
class Program
{
    public static void ChangeColor(Pen pen)
    {
        pen.Color = Color.Green;
        Console.WriteLine($"Inside the ChangeColor method the color is {pen.Color}");
    }

    public static void CreateNewObjectWithoutRef(Pen pen)
    {
        pen = new Pen(Color.Red);
        Console.WriteLine($"Inside the CreateNewObjectWithoutRef method the color of new pen object is {pen.Color}");
    }

    public static void CreateNewObjectWithRef(ref Pen pen)
    {
        pen = new Pen(Color.Yellow);
        Console.WriteLine($"Inside the CreateNewObjectWithRef method the color of new pen object is {pen.Color}");
    }

    static void Main(string[] args)
    {
        Pen pen = new Pen(Color.Blue);

        Console.WriteLine($"Before ChangeColor method: {pen.Color}");
        ChangeColor(pen);
        Console.WriteLine($"After the ChangeColor method: {pen.Color}");

        Console.WriteLine();

        Console.WriteLine($"Before CreateNewObjectWithoutRef method: {pen.Color}");
        CreateNewObjectWithoutRef(pen);
        Console.WriteLine($"After CreateNewObjectWithoutRef method: {pen.Color}");

        Console.WriteLine();

        Console.WriteLine($"Before CreateNewObjectWithRef method: {pen.Color}");
        CreateNewObjectWithRef(ref pen);
        Console.WriteLine($"After CreateNewObjectWithRef method: {pen.Color}");

        Console.ReadKey();
    }
}
```

En el primer m�todo, no usamos la palabra clave ref. El valor se cambia porque pasamos la copia de la direcci�n en la que se almacena el valor original. En el segundo m�todo, el valor original permanece igual. Eso es porque creamos un nuevo objeto dentro del m�todo, por lo que se asigna la nueva direcci�n de memoria. Pero en el tercer m�todo, usamos la palabra clave `ref` y el valor original cambia. �Por qu�? Porque con la refpalabra clave estamos copiando la misma direcci�n a un nuevo objeto.

## Conclusi�n

Ahora sabemos c�mo usar palabras clave ref y out con los tipos de valor y referencia. Esta es una caracter�stica bastante �til en C #, por lo que saber c�mo trabajar con esas palabras clave es una ventaja para los desarrolladores.

<!--- reference style links --->
[github-shield]: https://img.shields.io/badge/-@fernandocalmet-%23181717?style=flat-square&logo=github
[github-url]: https://github.com/fernandocalmet
[kofi-shield]: https://img.shields.io/badge/-@fernandocalmet-%231DA1F2?style=flat-square&logo=kofi&logoColor=ff5f5f
[kofi-url]: https://ko-fi.com/fernandocalmet
[linkedin-shield]: https://img.shields.io/badge/-fernandocalmet-blue?style=flat-square&logo=Linkedin&logoColor=white&link=https://www.linkedin.com/in/fernandocalmet
[linkedin-url]: https://www.linkedin.com/in/fernandocalmet
[khanakat-shield]: https://img.shields.io/badge/khanakat.com-brightgreen?style=flat-square
[khanakat-url]: https://khanakat.com