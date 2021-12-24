# Archivos, StreamWriter y StreamReader en `C#`

[![Github][github-shield]][github-url]
[![Kofi][kofi-shield]][kofi-url]
[![LinkedIn][linkedin-shield]][linkedin-url]
[![Khanakat][khanakat-shield]][khanakat-url]

## Creaci�n de objetos para StreamWriter y StreamReader

Para crear objetos para las clases `StreamReader` y `StreamWriter`, necesitamos usar la inicializaci�n est�ndar para los tipos de datos de referencia. Podemos ejecutar esta inicializaci�n de varias formas, pero la m�s com�n es solo proporcionando una direcci�n al archivo:

```csharp
StreamReader readerRelativePath = new StreamReader("test.txt");
StreamReader readerAbsolutePath = new StreamReader("C:\\MyProject\\test.txt");
StreamWriter writerRelativePath = new StreamWriter("test.txt");
StreamWriter writerAbsolutePath = new StreamWriter("C:\\MyProject\\test.txt");
```

Como podemos ver en el c�digo anterior, podemos proporcionar la ruta relativa o absoluta a nuestro archivo. Si proporcionamos una ruta relativa (solo un nombre y una extensi�n), Visual Studio colocar� un archivo dentro de la carpeta projectName / bin / debug.

## M�todos StreamReader

StreamReader contiene muchos m�todos diferentes para trabajar con archivos, pero vamos a mencionar algunos de ellos.

El m�todo `Read()` devolver� el siguiente signo como un n�mero entero o -1 si llegamos al final del archivo. Podemos usar conversi�n expl�cita (conversi�n) para convertir ese entero en un tipo `char`:

```csharp
static void Main(string[] args)
{
    StreamReader sr = new StreamReader("test.txt");

    int x;
    char ch;

    x = sr.Read();
            
    while(x != -1)
    {
        ch = (char)x;
        //do stuff here
        x = sr.Read();
    }
}
```

El m�todo `ReadLine()` devolver� una l�nea completa como una cadena. Si llegamos al final del archivo, devolver� nulo:

```csharp
static void Main(string[] args)
{
    StreamReader sr = new StreamReader("test.txt");

    string line = sr.ReadLine();

    while(line != null)
    {
        //some coding
        line = sr.ReadLine();
    }
}
```

El m�todo `ReadToEnd()` devuelve un archivo completo en una cadena. Si no hay nada m�s para leer, devolver� una cadena vac�a.

El m�todo `Peek()` comprueba el siguiente car�cter del archivo o, si no encuentra nada, devolver� -1:

```csharp
static void Main(string[] args)
{
    StreamReader sr = new StreamReader("test.txt");
    string line;

    while(sr.Peek() != -1)
    {
        line = sr.ReadLine();
        //some coding
    }
}
```

## M�todos StreamWriter

Los dos m�todos m�s importantes para la clase StreamWriter son `Write()` y `WriteLine()`. Con el m�todo `Write()` escribimos una l�nea dentro de un archivo pero sin pasar a otra l�nea despu�s. Pero con el m�todo `WriteLine()`  escribimos una l�nea dentro de un archivo y pasamos a otra l�nea.

Es muy importante llamar al m�todo `Close()`, una vez que hayamos terminado con el uso de objetos de lectura o escritura.

Ejemplo 1: Cree una aplicaci�n que escriba cinco n�meros aleatorios del 1 al 100 en un archivo llamado numbers.txt. Luego leer� todos los n�meros de ese archivo, los imprimir� e imprimir� el n�mero m�ximo:

```csharp
class Program
{
    public static void WriteToFile(string path)
    {
        StreamWriter sw = new StreamWriter(path);
        Random r = new Random(); //class to generate random numbers
        for(int i = 1; i <= 5; i++)
        {
            sw.WriteLine(r.Next(1,101));
        }

        sw.Close();
    }

    public static void PrintNumbersAndMax(string path)
    {
        StreamReader sr = new StreamReader(path);
        string line = sr.ReadLine();
        Console.WriteLine(line);
        int max = Convert.ToInt32(line);

        while ((line = sr.ReadLine()) != null)
        {
            Console.WriteLine(line);

            int temp = Convert.ToInt32(line);
            if(temp > max)
            {
                max = temp;
            }
        }
     
        sr.Close();

        Console.WriteLine($"Max number is: {max}");
    }

    static void Main(string[] args)
    {
        WriteToFile("numbers.txt");

        PrintNumbersAndMax("numbers.txt");

        Console.ReadLine();
   }
}
```

Como podemos ver, tenemos que usar el m�todo `Close` para cerrar nuestro lector y escritor. Pero hay una forma a�n mejor de hacer esto. Usando el bloque` using`.

## Usando Block

El bloque `using` ayuda a gestionar nuestros recursos. Especifica un alcance en el que usamos nuestro recurso, y una vez que dejamos ese alcance, el recurso ser� administrado.

Para usar el bloque `using` necesitamos especificar la palabra clave `using`, crear recursos entre par�ntesis y declarar el alcance del usingbloque con las llaves:

```csharp
using (Resource creation)
{

}
```

Entonces, podemos reescribir uno de nuestros m�todos del ejemplo anterior:

```csharp
public static void PrintNumbersAndMax(string path)
{
    using (StreamReader sr = new StreamReader(path))
    {
        string line = sr.ReadLine();
        Console.WriteLine(line);
        int max = Convert.ToInt32(line);

        while ((line = sr.ReadLine()) != null)
        {
            Console.WriteLine(line);

            int temp = Convert.ToInt32(line);
            if (temp > max)
            {
                 max = temp;
            }
        }

        Console.WriteLine($"Max number is: {max}");
    }
}
```

En este ejemplo, no estamos usando el m�todo `Close` porque tan pronto como la ejecuci�n abandone el cuerpo de la declaraci�n `using` , el `StreamReaderobjeto` ser� administrado.

## Conclusi�n

Aqu� vamos. En este momento, tenemos un buen conocimiento para manipular archivos de C #.

<!--- reference style links --->
[github-shield]: https://img.shields.io/badge/-@fernandocalmet-%23181717?style=flat-square&logo=github
[github-url]: https://github.com/fernandocalmet
[kofi-shield]: https://img.shields.io/badge/-@fernandocalmet-%231DA1F2?style=flat-square&logo=kofi&logoColor=ff5f5f
[kofi-url]: https://ko-fi.com/fernandocalmet
[linkedin-shield]: https://img.shields.io/badge/-fernandocalmet-blue?style=flat-square&logo=Linkedin&logoColor=white&link=https://www.linkedin.com/in/fernandocalmet
[linkedin-url]: https://www.linkedin.com/in/fernandocalmet
[khanakat-shield]: https://img.shields.io/badge/khanakat.com-brightgreen?style=flat-square
[khanakat-url]: https://khanakat.com