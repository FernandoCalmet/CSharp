# Tipos an�nimos y que aceptan valores NULL

[![Github][github-shield]][github-url]
[![Kofi][kofi-shield]][kofi-url]
[![LinkedIn][linkedin-shield]][linkedin-url]
[![Khanakat][khanakat-shield]][khanakat-url]

## Clases an�nimas

Una clase an�nima es una clase que no tiene nombre. Esto suena extra�o, pero a veces una clase an�nima puede ser �til, especialmente cuando se usan expresiones de consulta.

Veamos qu� queremos decir con eso.

Podemos crear un objeto de la clase an�nima simplemente usando la palabra clave `new` delante de llaves:

```csharp
myAnonymousObj = new { Name = "John", Age = 32 };
```

Este objeto contiene dos propiedades el `Name` y el `Age`. El compilador asignar� impl�citamente los tipos a las propiedades en funci�n de los tipos de sus valores. Entonces, lo que esto significa b�sicamente es que la propiedad `Name` ser� del tipo cadena y la propiedad `Age` del tipo int.

Pero ahora, podemos preguntarnos, �de qu� tipo `myAnonymousObj` es? Y la respuesta es que no sabemos, cu�l es el objetivo de las clases an�nimas. Pero en C # esto no es un problema, podemos declarar nuestro objeto como una variable tipada impl�citamente usando la palabra clave `var`:

```csharp
var myAnonymousObj = new { Name = "nesto", Age = 32 };
```

La palabra clave var hace que el compilador cree una variable del mismo tipo que la expresi�n que usamos para inicializar ese objeto. Entonces, veamos un par de ejemplos de tipos conocidos:

```csharp
var number = 15; // the number is of type int
var word = "example"; //the word is of type string
var money = 987.32; //the money is of type double
```

Podemos acceder a las propiedades de nuestro objeto an�nimo de la misma manera que lo hicimos con los objetos regulares:

```csharp
Console.WriteLine($"The name of myAnonymousObject is {myAnonymousObj.Name}, the age is {myAnonymousObj.Age}");
```

## Tipos que aceptan valores NULL

El valor nulo es �til para inicializar tipos de referencia. Entonces, es l�gico que no podamos asignar el valor nulo al tipo de valor porque el nulo es en s� mismo una referencia.

Dicho esto, podemos ver que la siguiente declaraci�n arrojar� un error:

![img01](/img/01.png)

Sin embargo, C # nos proporciona un modificador que podemos usar para declarar un tipo de valor como un tipo de valor anulable. Podemos usar el ? signo para indicar que el tipo de valor es anulable:

```csharp
int? number = null;
```

Todav�a podemos asignar un valor entero a nuestro tipo de valor anulable:

```csharp
int? number = null;
int another = 200;

number = 345;
number = another;
```

Todo esto es v�lido. Pero si intentamos asignar la variable de un tipo int con un valor de nuestro tipo anulable, vamos a tener un problema:

```csharp
int? number = null;
int another = 200;

another = number; //this is the problem
```

Esto tiene sentido si consideramos que la variable `number` puede contener el nulo pero la variable `another` no puede contener nulo en absoluto.

## Propiedades de los tipos que aceptan valores NULL

Los tipos que aceptan valores NULL exponen algunas propiedades que pueden resultar �tiles mientras se trabaja en nuestros proyectos. La propiedad `HasValue` indica si un tipo que acepta valores NULL contiene un valor o es un valor nulo. La propiedad `Value` nos permite recuperar el valor del tipo que acepta valores NULL si no es nulo:

```csharp
int? number = null;
number = 234; //comment this line to print out the result from the else block

if(number.HasValue)
{
    Console.WriteLine(number.Value);
}
else
{
     Console.WriteLine("number is null");
}
```

## Conclusi�n

En este art�culo, hemos aprendido:

- C�mo usar clases an�nimas
- Cu�les son los tipos que aceptan valores NULL
- Acerca de las propiedades de los tipos que aceptan valores NULL

<!--- reference style links --->
[github-shield]: https://img.shields.io/badge/-@fernandocalmet-%23181717?style=flat-square&logo=github
[github-url]: https://github.com/fernandocalmet
[kofi-shield]: https://img.shields.io/badge/-@fernandocalmet-%231DA1F2?style=flat-square&logo=kofi&logoColor=ff5f5f
[kofi-url]: https://ko-fi.com/fernandocalmet
[linkedin-shield]: https://img.shields.io/badge/-fernandocalmet-blue?style=flat-square&logo=Linkedin&logoColor=white&link=https://www.linkedin.com/in/fernandocalmet
[linkedin-url]: https://www.linkedin.com/in/fernandocalmet
[khanakat-shield]: https://img.shields.io/badge/khanakat.com-brightgreen?style=flat-square
[khanakat-url]: https://khanakat.com