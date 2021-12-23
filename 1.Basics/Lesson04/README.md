# Conversi�n de tipos en ``C#``

[![Github][github-shield]][github-url]
[![Kofi][kofi-shield]][kofi-url]
[![LinkedIn][linkedin-shield]][linkedin-url]
[![Khanakat][khanakat-shield]][khanakat-url]

## Conversi�n impl�cita en ``C#``

Se podr�an interpretar muchos datos diferentes utilizando diferentes tipos. Por ejemplo, el n�mero 74 se puede interpretar como un n�mero entero pero tambi�n como doble (74.0). Hay dos situaciones en las que se aplica la conversi�n impl�cita.

El primero es cuando calculamos una expresi�n. El compilador adapta autom�ticamente los tipos de datos que usamos en esa expresi�n:

```csharp
class Program
{
    static void Main(string[] args)
    {
        double b = 12.45;
        int x = 10;
        b = b + x;
    }
}
```

Aqu� la `b` variable es de tipo double y `x` es de tipo int. En la expresi�n `b + x`, el compilador convierte impl�citamente `x` de int a double y luego asigna un resultado al `b`.

La segunda situaci�n para la conversi�n es cuando el compilador almacena el resultado en una variable:

```csharp
class Program
{
    static void Main(string[] args)
    {
        int y = 20;
        int x = 10;
        double b;
        b = y / x;
    }
}
```

![img01](img/01.png)

En este ejemplo, vemos que ambos `x` y  `y` son del tipo int, pero el resultado es del tipo double.

Ahora, prestemos atenci�n a este ejemplo:

```csharp
int x = 21;
int y = 5

double b = x/y;
```

�Qu� piensas, qu� valor se almacena en la variable `b`?

La respuesta: "El resultado es 4,2" no es correcta. Por supuesto, ahora va la pregunta: "�Pero por qu�"?

El compilador calcula primero la expresi�n del lado derecho y solo luego convierte ese resultado en doble. Entonces, la expresi�n del lado derecho `x/y` consta de n�meros enteros, por lo que el resultado tambi�n es un n�mero entero, en este ejemplo, es 4 (el valor est� truncado). Despu�s de ese c�lculo, el compilador convierte el resultado en un doble y asigna el valor a la variable b:

```csharp
class Program
{
    static void Main(string[] args)
    {
        int y = 5;
        int x = 21;
        double b = x / y;
    }
}
```

![img02](img/02.png)

Podemos arreglar esto si queremos, usando la conversi�n expl�cita en cualquiera de las variables `x` o `y` en la expresi�n.

## Conversi�n expl�cita en ``C#``

Para la conversi�n expl�cita, necesitamos escribir c�digo adicional para convertir un tipo en otro. Tenemos dos formas diferentes, usando un operador de conversi�n o usando la Convertclase.

Veamos el siguiente ejemplo:

![img03](img/03.png)

El compilador se queja de una conversi�n no v�lida. Lo que nos falta aqu� es el operador de conversi�n, as� que us�moslo:

```csharp
class Program
{
    static void Main(string[] args)
    {
        int a;
        double b = 10.7;

        a = (int)b;
    }
}
```

![img04](img/04.png)

Al usar la `(int)` conversi�n de conversi�n, podemos transmitir de manera segura nuestros tipos de datos y el compilador lo aprueba. Pero lo que podemos ver es que nuestro resultado no es el que esperar�amos. Pero este es el resultado correcto. Es muy importante comprender que el operador de conversi�n puede reducir los datos cuando convertimos el tipo con el alcance de valor m�s grande a un tipo con el alcance de valor m�s peque�o. Como hicimos con la conversi�n de doble a int, por ejemplo.

Ahora podemos aplicar el operador de conversi�n en nuestro ejemplo de la parte Conversi�n impl�cita, para obtener el resultado correcto:

```csharp
class Program
{
    static void Main(string[] args)
    {
        int x = 21;
        int y = 5;

        double b = (double)x / y;
    }
}
```

El resultado ser� 4.2.

## Usando la clase Convert en ``C#``

Como dijimos, podemos usar la clase Convert con sus m�todos est�ticos, para convertir expl�citamente un tipo base a otro tipo base:

```csharp
class Program
{
    static void Main(string[] args)
    {
        int a = 15;
        string s = a; // this is not allowed

        int c = 15;
        string s1 = Convert.ToString(c); 
        //or
        string s2 = c.ToString();

    }
}
```

## Conclusi�n

Hemos aprendido sobre la conversi�n de tipos y c�mo se comporta la conversi�n impl�cita y expl�cita en C #.

<!--- reference style links --->
[github-shield]: https://img.shields.io/badge/-@fernandocalmet-%23181717?style=flat-square&logo=github
[github-url]: https://github.com/fernandocalmet
[kofi-shield]: https://img.shields.io/badge/-@fernandocalmet-%231DA1F2?style=flat-square&logo=kofi&logoColor=ff5f5f
[kofi-url]: https://ko-fi.com/fernandocalmet
[linkedin-shield]: https://img.shields.io/badge/-fernandocalmet-blue?style=flat-square&logo=Linkedin&logoColor=white&link=https://www.linkedin.com/in/fernandocalmet
[linkedin-url]: https://www.linkedin.com/in/fernandocalmet
[khanakat-shield]: https://img.shields.io/badge/khanakat.com-brightgreen?style=flat-square
[khanakat-url]: https://khanakat.com