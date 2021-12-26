# Delegados

[![Github][github-shield]][github-url]
[![Kofi][kofi-shield]][kofi-url]
[![LinkedIn][linkedin-shield]][linkedin-url]
[![Khanakat][khanakat-shield]][khanakat-url]

## Sintaxis de delegado

Una sintaxis b�sica para crear un objeto delegado es:

```csharp
delegate Result_Type identifier([parameters]);
```

Hay tres pasos para definir y usar delegados:

- Declaraci�n de nuestro delegado
- Creaci�n de instancias, creaci�n del objeto del delegado
- Invocaci�n, donde llamamos a un m�todo referenciado

```csharp
//Declaration
public delegate void WriterDelegate(string text);
class Program
{
    public static void Write(string text)
    {
        Console.WriteLine(text);
    }

    static void Main(string[] args)
    {
        //Instantiation
        WriterDelegate writerDelegate = new WriterDelegate(Write);

        //Invocation
        writerDelegate("Some example text.");
    }
}
```

Es importante comprender que el tipo de retorno de un m�todo y el n�mero de par�metros deben coincidir con el tipo de retorno del delegado y el n�mero de par�metros. De lo contrario, obtendremos un error del compilador. Podemos ver en nuestro ejemplo que nuestro m�todo `Write` tiene un vac�o como tipo de retorno y solo un par�metro de cadena, as� como nuestro delegado.

Los delegados son muy �tiles para encapsular nuestros m�todos.

C # tiene los dos delegados integrados: `Func<T>` y `Action<T>`, son ampliamente utilizados, as� que hablemos m�s sobre ellos.

## Delegado Func <T>

Este delegado encapsula un m�todo que tiene hasta diecis�is par�metros y devuelve un valor del tipo especificado. Entonces, en otras palabras, usamos el delegado `Func` solo con un m�todo que tiene un tipo de retorno distinto de void.

Podemos instanciar el delegado `Func` con esta sintaxis:

```csharp
Func<Type1, Type2..., ReturnType> DelegateName = new Func<Type1, Type2..., ReturnType>(MethodName);
```

Podemos ver que el �ltimo par�metro entre corchetes es un tipo de retorno. Por supuesto, no tenemos que inicializar un objeto delegado como este, podemos hacerlo de otra manera:

```csharp
Func< Type1, Type2..., ReturnType> name = MethodName;
```

Veamos c�mo usar delegate `Func` con un ejemplo:

```csharp
class Program
{
    public static int Sum(int a, int b)
    {
        return a + b;
    }

    static void Main(string[] args)
    {
        Func<int, int, int> sumDelegate = Sum;
        Console.WriteLine(sumDelegate(10, 20));
    }
}
```

## Delegado Acci�n <T> 

Este delegado encapsula un m�todo que tiene hasta diecis�is par�metros y no devuelve ning�n resultado. Entonces podemos asignar a este delegado solo m�todos con el tipo de retorno void.

Podemos instanciar el objeto `Action` con esta sintaxis:

```csharp
Action<Type1, Type2...> DelegateName = new Action<Type1, Type2...>(MethodName);
```

O podemos usar otra forma:

```csharp
Action < Type1, Type2...> DelegateName = MethodName;
```

Veamos c�mo usar delegate `Action` con un ejemplo:

```csharp
public static void Write(string text)
{
    Console.WriteLine(text);
}

static void Main(string[] args)
{
    Action<string> writeDelegate = Write;
    writeDelegate("String parameter to write.");
}
```

## Ejemplo practico

En este ejemplo, vamos a crear una aplicaci�n que ejecuta uno de tres m�todos (Sumar, Restar, Multiplicar) basado en un solo par�metro proporcionado. B�sicamente, si enviamos `Sum` como par�metro, se ejecutar� el m�todo `Sum`, y as� sucesivamente. Primero, escribiremos este ejemplo sin delegados y luego refactorizaremos ese c�digo introduciendo delegados.

As� que comencemos con la primera parte:

```csharp
public enum Operation
{
    Sum,
    Subtract,
    Multiply
}

public class OperationManager
{
    private int _first;
    private int _second;
    public OperationManager(int first, int second)
    {
        _first = first;
        _second = second;
    }

    private int Sum()
    {
        return _first + _second;
    }

    private int Subtract()
    {
        return _first - _second;
    }

    private int Multiply()
    {
        return _first * _second;
    }

    public int Execute(Operation operation)
    {
        switch (operation)
        {
            case Operation.Sum:
                return Sum();
            case Operation.Subtract:
                return Subtract();
            case Operation.Multiply:
                return Multiply();
            default:
                return -1; //just to simulate
        }
    }
}

class Program
{
    static void Main(string[] args)
    {
        var opManager = new OperationManager(20, 10);
        var result = opManager.Execute(Operation.Sum);
        Console.WriteLine($"The result of the operation is {result}");

        Console.ReadKey();
    }
}
```

Si iniciamos esta aplicaci�n, obtendremos la respuesta correcta para cualquier operaci�n que enviemos al m�todo `Execute`. Pero este c�digo podr�a ser mucho mejor y m�s f�cil de leer sin expresi�n `switch-case`. Si vamos a tener m�s de diez operaciones (por ejemplo), este bloque `switch` tambi�n ser�a muy feo de leer y mantener.

Entonces, cambiemos nuestro c�digo para que sea legible, mantenible y m�s orientado a objetos. Presentamos una nueva clase `ExecutionManager`:

```csharp
public class ExecutionManager
{
    public Dictionary<Operation, Func<int>> FuncExecute { get; set; }
    private Func<int> _sum;
    private Func<int> _subtract;
    private Func<int> _multiply;

    public ExecutionManager()
    {
        FuncExecute = new Dictionary<Operation, Func<int>>(3);
    }

    public void PopulateFunctions(Func<int> Sum, Func<int> Subtract, Func<int> Multiply)
    {
        _sum = Sum;
        _subtract = Subtract;
        _multiply = Multiply;
    }

    public void PrepareExecution()
    {
        FuncExecute.Add(Operation.Sum, _sum);
        FuncExecute.Add(Operation.Subtract, _subtract);
        FuncExecute.Add(Operation.Multiply, _multiply);
    }
}
```

Aqu�, creamos un diccionario que contendr� todas las operaciones y todas las referencias hacia nuestros m�todos (delegados Func). Ahora podemos inyectar esta clase en la clase `OperationManager` y cambiar el m�todo `Execute`:

```csharp
public class OperationManager
{
    private int _first;
    private int _second;
    private readonly ExecutionManager _executionManager;

    public OperationManager(int first, int second, ExecutionManager executionManager)
    {
        _first = first;
        _second = second;
        _executionManager = executionManager;
        _executionManager.PopulateFunctions(Sum, Subtract, Multiply);
        _executionManager.PrepareExecution();
    }

    private int Sum()
    {
        return _first + _second;
    }

    private int Subtract()
    {
        return _first - _second;
    }

    private int Multiply()
    {
        return _first * _second;
    }

    public int Execute(Operation operation)
    {
        return _executionManager.FuncExecute.ContainsKey(operation) ?
            _executionManager.FuncExecute[operation]() :
            -1;
    }
}
```

Ahora, estamos configurando todo en el constructor de la clase `OperationManager` y ejecutando nuestra acci�n en el m�todo `Execute` si contiene la operaci�n requerida. A primera vista, podemos ver cu�nto mejor es este c�digo.

Finalmente, necesitamos cambiar la clase `Program`:

```csharp
class Program
{
    static void Main(string[] args)
    {
        var executionManager = new ExecutionManager();
        var opManager = new OperationManager(20, 10, executionManager);
        var result = opManager.Execute(Operation.Sum);
        Console.WriteLine($"The result of the operation is {result}");

        Console.ReadKey();
    }
}
```

## Conclusi�n

En este art�culo, hemos aprendido:

- C�mo crear una instancia de un delegado
- La forma de utilizar los delegados de Func y Action
- C�mo escribir un c�digo mejor usando delegados

<!--- reference style links --->
[github-shield]: https://img.shields.io/badge/-@fernandocalmet-%23181717?style=flat-square&logo=github
[github-url]: https://github.com/fernandocalmet
[kofi-shield]: https://img.shields.io/badge/-@fernandocalmet-%231DA1F2?style=flat-square&logo=kofi&logoColor=ff5f5f
[kofi-url]: https://ko-fi.com/fernandocalmet
[linkedin-shield]: https://img.shields.io/badge/-fernandocalmet-blue?style=flat-square&logo=Linkedin&logoColor=white&link=https://www.linkedin.com/in/fernandocalmet
[linkedin-url]: https://www.linkedin.com/in/fernandocalmet
[khanakat-shield]: https://img.shields.io/badge/khanakat.com-brightgreen?style=flat-square
[khanakat-url]: https://khanakat.com