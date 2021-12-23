# Tipos de datos, declaraciones y definiciones de variables en ``C#``

[![Github][github-shield]][github-url]
[![Kofi][kofi-shield]][kofi-url]
[![LinkedIn][linkedin-shield]][linkedin-url]
[![Khanakat][khanakat-shield]][khanakat-url]

En C #, los diferentes tipos de datos se registran de forma diferente. Adem�s, tambi�n se les permite ejecutar diferentes acciones sobre ellos. Para diferentes tipos de datos, se reserva una cierta cantidad de espacio de memoria en nuestras computadoras.

Con cada tipo de datos definimos:

- C�mo registrar datos en la memoria
- Los posibles valores para esos datos
- Posibles acciones sobre los datos

## Registro de tipo de datos en ``C#``

os tipos de datos que representan n�meros enteros se expresan con un cierto n�mero de bits. Para n�meros sin signo, el rango es de 0 a 2^N -1, y el rango de n�meros con signo es de -2^N-1 a 2^N-1 -1. Entonces, si el tipo de datos tiene un tama�o de 8 bits como el tipo de datos sbyte, podemos representar su rango as�: de -2^7 a 2^7 -1 => de -128 a 127.

La siguiente tabla contiene diferentes tipos de datos que representan los n�meros enteros:

![img01](img/01.png)

La letra ``u`` delante del tipo significa que el tipo no puede contener n�meros negativos, no est� firmado.

Los tipos mencionados anteriormente son los tipos de n�meros enteros. Pero en C #, tenemos los tipos de n�meros con punto flotante.

Tambi�n podemos presentarlos en una tabla:

![img02](img/02.png)

En C #, tenemos dos tipos de datos b�sicos m�s:

![img03](img/03.png)

Para usar el tipo de caracteres en nuestro c�digo, debemos colocarlo entre comillas simples: 'a' o 'A' o '3' ...

Otro tipo que a menudo se presenta como tipo de datos b�sico es el tipo de cadena . Pero la cadena no es un tipo de valor, es un tipo de referencia. Para usar una cadena en nuestro c�digo, debemos colocar el valor entre comillas dobles: "Este es el tipo de cadena" o "3452" ...

Entonces, sabemos que tenemos los tipos de valor y los tipos de referencia, y es hora de hablar m�s sobre ellos y las variables tambi�n.

## Variables en ``C#``

Variable es un nombre de una ubicaci�n de memoria en la que la aplicaci�n almacena valores.

Deber�amos crear nuestras variables con los siguientes ejemplos:

- nombre del estudiante
- sujeto
- work_day ...

Los ejemplos incorrectos ser�an

- nombre del estudiante
- jornada laboral
- 1 lugar

Debemos mencionar que C # es un lenguaje que distingue entre may�sculas y min�sculas, por lo que el nombre del alumno no es el mismo que el nombre del alumno .

El lenguaje C # tiene su propio conjunto de palabras reservadas, las llamadas palabras clave. No podemos usarlos como nombre para nuestras variables. Para obtener la lista de palabras clave, puede visitar la lista de palabras clave .

Pero si por alguna raz�n queremos nombrar nuestra variable con una palabra clave, para evitar choques, podemos usar el @signo delante del nombre:

```csharp
int @int; //valid
string @return; //valid
decimal decimal; //not valid
```

### Palabras clave contextuales

Las palabras clave contextuales son las que podemos usar para los nombres de las variables pero sin usar el signo @ al frente:

``add alias ascending async await by descending dynamic equals from get global group in`` 
``into join``
``let nameof on orderby partial remove select set unmanaged value var when where yield``

### Tipos de valor y referencia

En C #, tenemos variables divididas en dos categor�as: tipo de valor y tipo de referencia . La diferencia es que las variables de tipo de valor almacenan sus valores dentro de sus propias ubicaciones de memoria, pero la ubicaci�n de memoria para las variables de tipo de referencia contiene solo la direcci�n de la ubicaci�n de memoria din�mica donde se almacena el valor.

Veamos c�mo se comportan los tipos de valor en un ejemplo gr�fico:

![img04](img/04.png)

Hagamos lo mismo para los tipos de referencia:

![img05](img/05.png)

## Declaraciones y expresiones de variable en C #

Debemos declarar nuestras variables de la siguiente manera:

``<data type> <variable name> ;  or <data type> <variable name>, <variable name> ... ;``

Entonces, algunos ejemplos ser�an:

```csharp
class Program
{
    static void Main(string[] args)
    {
        int age;
        double temperature, change;
        Student student;
    }
}
```

Solo con la declaraci�n, no podemos asignar un valor a una variable de tipo de valor. Para hacer eso, necesitamos usar expresiones adem�s:

``<data type> <variable name> = <expression> ;``

Nuevamente, veamos esto con un ejemplo:

```csharp
class Program
{
    static void Main(string[] args)
    {
        int x = 5;
        int y = 145 + x;
        char p = 'p';
        p = 'A';
    }
}
```

Para agregar valor a la variable de tipo de referencia, necesitamos usar la  newpalabra clave en la parte de la expresi�n (la cadena es una excepci�n a esta regla):

```csharp
class Program
{
    static void Main(string[] args)
    {
        Student student = new Student("John", 25);
    }
}
```

Nos gustar�a mencionar que no recomendamos llamar a las variables con nombres "x" o "y" ... Hemos utilizado esos nombres solo por simplicidad. Es una mejor idea dar nombres significativos a nuestras variables.

## Conclusi�n

Ahora hemos aprendido c�mo declarar nuestras variables y tambi�n c�mo asignarles valores.

<!--- reference style links --->
[github-shield]: https://img.shields.io/badge/-@fernandocalmet-%23181717?style=flat-square&logo=github
[github-url]: https://github.com/fernandocalmet
[kofi-shield]: https://img.shields.io/badge/-@fernandocalmet-%231DA1F2?style=flat-square&logo=kofi&logoColor=ff5f5f
[kofi-url]: https://ko-fi.com/fernandocalmet
[linkedin-shield]: https://img.shields.io/badge/-fernandocalmet-blue?style=flat-square&logo=Linkedin&logoColor=white&link=https://www.linkedin.com/in/fernandocalmet
[linkedin-url]: https://www.linkedin.com/in/fernandocalmet
[khanakat-shield]: https://img.shields.io/badge/khanakat.com-brightgreen?style=flat-square
[khanakat-url]: https://khanakat.com