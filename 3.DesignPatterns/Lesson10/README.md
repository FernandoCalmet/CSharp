# Patr�n de dise�o: Strategy

[![Github][github-shield]][github-url]
[![Kofi][kofi-shield]][kofi-url]
[![LinkedIn][linkedin-shield]][linkedin-url]
[![Khanakat][khanakat-shield]][khanakat-url]

## Estructura del patr�n de dise�o de estrategia

Como dijimos anteriormente, el patr�n de dise�o de la estrategia consiste en el objeto Contexto que mantiene la referencia hacia el objeto de la estrategia. Pero no es la �nica parte del rompecabezas. Para la implementaci�n completa, necesitamos el objeto Estrategia (interfaz) para definir una forma para que el objeto Contexto ejecute la estrategia y los objetos Estrategias concretas que implementa la interfaz Estrategia.

El patr�n de dise�o de estrategia es bastante com�n en el lenguaje C # debido a sus diversos usos para proporcionar el comportamiento cambiante de una clase sin modificarlo. Esto cumple con las reglas del Principio Abierto Cerrado , del que hablamos en uno de nuestros art�culos anteriores.

## Implementaci�n del patr�n de dise�o de la estrategia

Para implementar el patr�n de Estrategia, vamos a reutilizar un ejemplo de nuestro art�culo Principio Abierto Cerrado .

Entonces, la tarea principal es calcular el costo total de los salarios del desarrollador, pero para los diferentes niveles de desarrollador, el salario se calcula de manera diferente. Ahora, vamos a modificar ese ejemplo introduciendo el patr�n de dise�o de estrategia.

As� que comencemos con la enumeraci�n `DeveloperLevel` y un objeto simple `DeveloperReport` :

```csharp
public enum DeveloperLevel
{
    Senior,
    Junior
}
```

```csharp
public class DeveloperReport
{
    public int Id { get; set; }
    public string Name { get; set; }
    public DeveloperLevel Level { get; set; }
    public int WorkingHours { get; set; }
    public double HourlyRate { get; set; }

    public double CalculateSalary() => WorkingHours * HourlyRate; 
}
```

Para continuar, creemos la interfaz de estrategia llamada `ISalaryCalculator`:

```csharp
public interface ISalaryCalculator
{
    double CalculateTotalSalary(IEnumerable<DeveloperReport> reports);
}
```

Ahora lo que necesitamos son los objetos de estrategia concretos que aceptar�n todos los informes y calcular�n el salario total para los niveles de desarrollador requeridos:

```csharp
public class JuniorDevSalaryCalculator : ISalaryCalculator
{
    public double CalculateTotalSalary(IEnumerable<DeveloperReport> reports) => 
        reports
            .Where(r => r.Level == DeveloperLevel.Junior)
            .Select(r => r.CalculateSalary())
            .Sum();
}
```

```csharp
public class SeniorDevSalaryCalculator : ISalaryCalculator
{
    public double CalculateTotalSalary(IEnumerable<DeveloperReport> reports) =>
        reports
            .Where(r => r.Level == DeveloperLevel.Senior)
            .Select(r => r.CalculateSalary() * 1.2)
            .Sum();
}
```

Como podemos ver, para los desarrolladores senior, estamos agregando una bonificaci�n del 20% al salario. Adem�s, hemos separado nuestra l�gica de c�lculo para los diferentes niveles de desarrollador y facilitamos la adici�n de l�gica de c�lculo para los desarrolladores intermedios, por ejemplo. Todo lo que tendr�amos que hacer es agregar un objeto de estrategia adicional que implemente la interfaz `ISalaryCalculator`.

Una vez que tenemos los objetos de estrategia, necesitamos el objeto de contexto en nuestra implementaci�n:

```csharp
public class SalaryCalculator
{
    private ISalaryCalculator _calculator;

    public SalaryCalculator(ISalaryCalculator calculator)
    {
        _calculator = calculator;
    }

    public void SetCalculator(ISalaryCalculator calculator) => _calculator = calculator;

    public double Calculate(IEnumerable<DeveloperReport> reports) => _calculator.CalculateTotalSalary(reports);
}
```

En este objeto de contexto, proporcionamos la inicializaci�n del objeto de estrategia con el constructor en un tiempo de compilaci�n o con el m�todo `SetCalculator` en el tiempo de ejecuci�n de la aplicaci�n. Adem�s, el m�todo `Calculate` simplemente ejecuta la funcionalidad del objeto de estrategia.

Entonces, para conectar todos los puntos, modifiquemos la clase `Program.cs`:

```csharp
class Program
{
    static void Main(string[] args)
    {
        var reports = new List<DeveloperReport>
        {
            new DeveloperReport {Id = 1, Name = "Dev1", Level = DeveloperLevel.Senior, HourlyRate = 30.5, WorkingHours = 160 },
            new DeveloperReport { Id = 2, Name = "Dev2", Level = DeveloperLevel.Junior, HourlyRate = 20, WorkingHours = 120 },
            new DeveloperReport { Id = 3, Name = "Dev3", Level = DeveloperLevel.Senior, HourlyRate = 32.5, WorkingHours = 130 },
            new DeveloperReport { Id = 4, Name = "Dev4", Level = DeveloperLevel.Junior, HourlyRate = 24.5, WorkingHours = 140 }
        };

        var calculatorContext = new SalaryCalculator(new JuniorDevSalaryCalculator());
        var juniorTotal = calculatorContext.Calculate(reports);
        Console.WriteLine($"Total amount for junior salaries is: {juniorTotal}");

        calculatorContext.SetCalculator(new SeniorDevSalaryCalculator());
        var seniorTotal = calculatorContext.Calculate(reports);
        Console.WriteLine($"Total amount for senior salaries is: {seniorTotal}");

        Console.WriteLine($"Total cost for all the salaries is: {juniorTotal+seniorTotal}");
    }
}
```

Este deber�a ser nuestro resultado:

![img01](/img/01.png)

## �Cu�ndo deber�amos utilizar el patr�n de dise�o de la estrategia?

Debemos usar este patr�n siempre que tengamos diferentes variaciones para alguna funcionalidad en un objeto y queramos cambiar de una variaci�n a otra en un tiempo de ejecuci�n. Adem�s, si tenemos clases similares en nuestro proyecto que solo difieren en c�mo ejecutan alg�n comportamiento, el patr�n de estrategia deber�a ser la elecci�n correcta para nosotros.

Deber�amos considerar la posibilidad de introducir este patr�n en situaciones en las que una sola clase tiene m�ltiples condiciones sobre diferentes variaciones de la misma funcionalidad. Eso es porque el patr�n de estrategia nos permite extraer esas variaciones en clases separadas (estrategias concretas). Luego, podemos invocarlos en la clase de contexto.

## Conclusi�n

Como puede ver, implementar el patr�n de dise�o de la estrategia no es dif�cil ni complejo en absoluto.

Hace que nuestro c�digo sea m�s legible y m�s f�cil de mantener. S�, requiere la implementaci�n de clases adicionales en el proyecto, pero ese es el precio que vale la pena pagar.

Entonces, hemos aprendido:

- �Cu�l es el patr�n de dise�o de la estrategia?
- C�mo implementarlo en C #
- Y cuando usarlo

<!--- reference style links --->
[github-shield]: https://img.shields.io/badge/-@fernandocalmet-%23181717?style=flat-square&logo=github
[github-url]: https://github.com/fernandocalmet
[kofi-shield]: https://img.shields.io/badge/-@fernandocalmet-%231DA1F2?style=flat-square&logo=kofi&logoColor=ff5f5f
[kofi-url]: https://ko-fi.com/fernandocalmet
[linkedin-shield]: https://img.shields.io/badge/-fernandocalmet-blue?style=flat-square&logo=Linkedin&logoColor=white&link=https://www.linkedin.com/in/fernandocalmet
[linkedin-url]: https://www.linkedin.com/in/fernandocalmet
[khanakat-shield]: https://img.shields.io/badge/khanakat.com-brightgreen?style=flat-square
[khanakat-url]: https://khanakat.com