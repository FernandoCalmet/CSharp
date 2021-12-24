# Clases y constructores

[![Github][github-shield]][github-url]
[![Kofi][kofi-shield]][kofi-url]
[![LinkedIn][linkedin-shield]][linkedin-url]
[![Khanakat][khanakat-shield]][khanakat-url]

## Agregar nuevos elementos en el Explorador de soluciones

Aunque podemos crear nuevas clases dentro del archivo `Program.cs`, es mucho mejor crear una nueva clase en un archivo separado. Para hacer eso, necesitamos hacer clic derecho en el nombre de nuestro proyecto, elegir Agregar y luego Nuevo elemento (Ctrl + Shift + A):

![img01](/img/01.png)

Luego, debemos elegir un archivo de clase y agregarle un nombre:

![img02](/img/02.png)

## Definici�n de clases y c�mo utilizarlas

En C #, para definir una clase, necesitamos usar la palabra clave `class`. La clase consta de miembros. Todos los miembros de la clase se definen en el cuerpo de la clase entre dos llaves:

```csharp
public class Student
{
    private string _name;
    private string _lastName;

    public string GetFullName()
    {
        return _name + ' ' + _lastName;
    }
 }
```

Vemos que el cuerpo contiene dos campos privados (las variables en el cuerpo de la clase se llaman campos) `_name` y `_lastName` un m�todo p�blico `GetFullName` (si no est� familiarizado con los modificadores de acceso: privado, p�blico, etc.).

Como sabemos por nuestros conceptos b�sicos de C # del m�dulo 1, la clase es un tipo de referencia, por lo que para inicializarla necesitamos usar la palabra clave `new`:

```csharp
class Program
{
    static void Main(string[] args)
    {
        Student student = new Student();
    }
}
```

Ahora el objeto `student` puede acceder a los miembros de la clase `Student`. Por ahora, solo tenemos un m�todo dentro de la clase `Student` y podemos llamarlo con la sintaxis `student.GetFullName()`. Esto devolver� una cadena vac�a, pero lo arreglaremos tan pronto como introduzcamos los constructores.

Es muy importante no confundir los t�rminos clase y objeto. La clase es una definici�n de tipo, pero un objeto es una instancia de ese tipo. Podemos tener varias instancias de objetos de la misma clase:

```csharp
Student student = new Student();
Student student10 = new Student();
Student student20 = new Student();
Student student30 = new Student();
```

## Constructores

Cuando usamos la palabra clave `new` para crear un objeto, CLR (Common Language Runtime) usa la definici�n de clase para construir ese objeto por nosotros llamando a un m�todo constructor.

El constructor es un m�todo especial que tiene el mismo nombre que la clase en la que est� definido, no devuelve ning�n valor (ni siquiera vac�o) y puede tomar par�metros. Se ejecuta autom�ticamente cuando creamos una instancia de una clase. Entonces, cada vez que usamos la palabra clave `new` para crear una instancia de una clase, estamos llamando a un constructor de esa clase.

Cada clase debe tener un constructor. Si no escribimos uno, el compilador genera uno autom�ticamente para nosotros. Este tipo de constructor se denomina constructor predeterminado . Un constructor predeterminado establecer� todos los datos dentro de una clase, a sus valores predeterminados (valores asignados si no los asignamos). Entonces, en nuestro ejemplo, los campos `_name` y `_lastName` tendr�n una cadena vac�a como valor al principio.

Tambi�n podemos escribir nuestro propio constructor predeterminado:

```csharp
public class Student
{
    private string _name;
    private string _lastName;

    public Student()
    {
        _name = string.Empty;
        _lastName = string.Empty;
    }

    public string GetFullName()
    {
        return _name + ' ' + _lastName;
    }
}
```

## Sobrecarga del constructor

Nuestras clases no est�n restringidas a tener un solo m�todo constructor. Podemos crear m�s de ellos en una sola clase:

```csharp
public class Student
{
    private string _name;
    private string _lastName;

    public Student()
    {
        _name = string.Empty;
        _lastName = string.Empty;
    }

    public Student(string name, string lastName)
    {
        _name = name;
        _lastName = lastName;
    }

    public string GetFullName()
    {
        return _name + ' ' + _lastName;
    }
}
```

Ahora tenemos dos opciones para instanciar nuestra clase, la primera con los valores predeterminados (que no tenemos que escribir) y la sobrecargada, que nos da la posibilidad de establecer los valores de nuestros campos:

```csharp
class Program
{
    static void Main(string[] args)
    {
        Student student = new Student(); //default constructor

        Student student1 = new Student("John", "Doe");//overloaded constructor
        Console.WriteLine(student1.GetFullName());
    }
}
```

Hay una cosa importante a tener en cuenta. Si creamos nuestro propio constructor para una clase, el compilador no crear� uno predeterminado para nosotros. Entonces, si queremos tener uno predeterminado y el sobrecargado, debemos crear ambos.

## Clases parciales

En un proyecto del mundo real, nuestra clase puede ser bastante grande con tantas l�neas de c�digo. Ese tipo de clases podr�an volverse menos legibles y dif�ciles de mantener. Para evitar eso, podemos usar clases parciales. Las clases parciales tienen a�n m�s ventajas porque varios desarrolladores pueden trabajar en la misma clase al mismo tiempo. Adem�s, tambi�n podemos crear un m�todo parcial dentro de esas clases.

Una clase parcial no es m�s que una parte de una sola clase. Para definir clases parciales, necesitamos usar la palabra clave `partial` en cada archivo:

```csharp
partial class Student
{
    private string _name;
    private string _lastName;

    public Student()
    {
        _name = string.Empty;
        _lastName = string.Empty;
    }
}

partial class Student
{
    public Student(string name, string lastName)
    {
        _name = name;
        _lastName = lastName;
    }

    public string GetFullName()
    {
        return _name + ' ' + _lastName;
    }
}
```

## Conclusi�n

En este art�culo, hemos aprendido:

- Que son las clases y como usarlas
- C�mo usar constructores y c�mo sobrecargarlos
- C�mo usar clases parciales y por qu� son �tiles

<!--- reference style links --->
[github-shield]: https://img.shields.io/badge/-@fernandocalmet-%23181717?style=flat-square&logo=github
[github-url]: https://github.com/fernandocalmet
[kofi-shield]: https://img.shields.io/badge/-@fernandocalmet-%231DA1F2?style=flat-square&logo=kofi&logoColor=ff5f5f
[kofi-url]: https://ko-fi.com/fernandocalmet
[linkedin-shield]: https://img.shields.io/badge/-fernandocalmet-blue?style=flat-square&logo=Linkedin&logoColor=white&link=https://www.linkedin.com/in/fernandocalmet
[linkedin-url]: https://www.linkedin.com/in/fernandocalmet
[khanakat-shield]: https://img.shields.io/badge/khanakat.com-brightgreen?style=flat-square
[khanakat-url]: https://khanakat.com