# Patr�n de dise�o: Singleton

[![Github][github-shield]][github-url]
[![Kofi][kofi-shield]][kofi-url]
[![LinkedIn][linkedin-shield]][linkedin-url]
[![Khanakat][khanakat-shield]][khanakat-url]

## Proyecto inicial

Vamos a comenzar con una aplicaci�n de consola simple en la que vamos a leer todos los datos de un archivo (que consiste en ciudades con su poblaci�n) y luego usar esos datos. Entonces, para comenzar, creemos una �nica interfaz:

```csharp
public interface ISingletonContainer
{
    int GetPopulation(string name);
}
```

Despu�s de eso, tenemos que crear una clase para implementar la interfaz ISingletonContainer. Lo vamos a llamar `SingletonDataContainer`:

```csharp
public class SingletonDataContainer: ISingletonContainer
{
    private Dictionary<string, int> _capitals = new Dictionary<string, int>();

    public SingletonDataContainer()
    {
        Console.WriteLine("Initializing singleton object");

        var elements = File.ReadAllLines("capitals.txt");
        for (int i = 0; i < elements.Length; i+=2)
        {
            _capitals.Add(elements[i], int.Parse(elements[i + 1]));
        }
    }

    public int GetPopulation(string name)
    {
        return _capitals[name];
    }
}
```

Entonces, tenemos un diccionario en el que almacenamos los nombres de las may�sculas y su poblaci�n de nuestro archivo. Como podemos ver, estamos leyendo de un archivo en nuestro constructor. Y eso est� muy bien. Ahora estamos listos para usar esta clase en cualquier consumidor simplemente creando una instancia. Pero, �es esto realmente lo que tenemos que hacer, crear una instancia de la clase que lee de un archivo que nunca cambia (en este proyecto en particular. La poblaci�n de las ciudades cambia a diario). Por supuesto que no, por lo que obviamente usar un patr�n Singleton ser�a muy �til aqu�.

Entonces, implement�moslo.

## Implementaci�n Singleton

Para implementar el patr�n Singleton, cambiemos la clase `SingletonDataContainer`:

```csharp
public class SingletonDataContainer: ISingletonContainer
{
    private Dictionary<string, int> _capitals = new Dictionary<string, int>();

    private SingletonDataContainer()
    {
        Console.WriteLine("Initializing singleton object");

        var elements = File.ReadAllLines("capitals.txt");
        for (int i = 0; i < elements.Length; i+=2)
        {
            _capitals.Add(elements[i], int.Parse(elements[i + 1]));
        }
    }

    public int GetPopulation(string name)
    {
        return _capitals[name];
    }

    private static SingletonDataContainer instance = new SingletonDataContainer();

    public static SingletonDataContainer Instance => instance;
}
```

Entonces, lo que hemos hecho aqu� es ocultar nuestro constructor de las clases de consumidores haci�ndolo privado. Luego, hemos creado una �nica instancia de nuestra clase y la hemos expuesto a trav�s de la propiedad Instance.

En este punto, podemos llamar a la propiedad Instance tantas veces como queramos, pero nuestro objeto ser� instanciado solo una vez y compartido para cada otra llamada.

Comprobemos esa teor�a:

```csharp
class Program
{
    static void Main(string[] args)
    {
        var db = SingletonDataContainer.Instance;
        var db2 = SingletonDataContainer.Instance;
        var db3 = SingletonDataContainer.Instance;
        var db4 = SingletonDataContainer.Instance;
    }
}
```

Si iniciamos nuestra aplicaci�n, veremos esto:

```bash
Initializing singleton object
Press any key to continue . . .
```

Podemos ver que estamos llamando a nuestra instancia cuatro veces, pero se inicializa solo una vez, que es exactamente lo que queremos.

Pero nuestra implementaci�n no es la ideal. Construyamos nuestro objeto de forma perezosa.

## Implementaci�n de un singleton seguro para subprocesos

Modifiquemos nuestra clase para implementar un Singleton seguro para subprocesos usando el tipo `Lazy`:

```csharp
public class SingletonDataContainer : ISingletonContainer
{
    private Dictionary<string, int> _capitals = new Dictionary<string, int>();

    private SingletonDataContainer()
    {
        Console.WriteLine("Initializing singleton object");

        var elements = File.ReadAllLines("capitals.txt");
        for (int i = 0; i < elements.Length; i+=2)
        {
            _capitals.Add(elements[i], int.Parse(elements[i + 1]));
        }
    }

    public int GetPopulation(string name)
    {
        return _capitals[name];
    }

    private static Lazy<SingletonDataContainer> instance = new Lazy<SingletonDataContainer>(() => new SingletonDataContainer());

    public static SingletonDataContainer Instance => instance.Value;
}
```

En este momento, nuestra clase es completamente segura para subprocesos. Se carga de forma diferida, lo que significa que nuestra instancia se crear� solo cuando sea realmente necesaria. Incluso podemos verificar si nuestro objeto se crea con la propiedad `IsValueCreated` si es necesario.

Excelente, hemos terminado nuestra implementaci�n de Singleton.

Ahora podemos consumirlo por completo en nuestra clase de consumidor:

```csharp
class Program
{
    static void Main(string[] args)
    {
        var db = SingletonDataContainer.Instance;
        Console.WriteLine(db.GetPopulation("Washington, D.C."));
        var db2 = SingletonDataContainer.Instance;
        Console.WriteLine(db2.GetPopulation("London"));
    }
}
```

## Conclusi�n

Hemos visto que aunque el patr�n Singleton no es tan apreciado, puede ser �til en algunos casos. Por lo tanto, siempre depende de nosotros decidir si lo vamos a utilizar o no. La conclusi�n es que si necesitamos aplicar un patr�n Singleton en nuestro proyecto, esta es una buena manera de hacerlo.

<!--- reference style links --->
[github-shield]: https://img.shields.io/badge/-@fernandocalmet-%23181717?style=flat-square&logo=github
[github-url]: https://github.com/fernandocalmet
[kofi-shield]: https://img.shields.io/badge/-@fernandocalmet-%231DA1F2?style=flat-square&logo=kofi&logoColor=ff5f5f
[kofi-url]: https://ko-fi.com/fernandocalmet
[linkedin-shield]: https://img.shields.io/badge/-fernandocalmet-blue?style=flat-square&logo=Linkedin&logoColor=white&link=https://www.linkedin.com/in/fernandocalmet
[linkedin-url]: https://www.linkedin.com/in/fernandocalmet
[khanakat-shield]: https://img.shields.io/badge/khanakat.com-brightgreen?style=flat-square
[khanakat-url]: https://khanakat.com