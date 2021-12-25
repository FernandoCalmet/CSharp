# Herencia

[![Github][github-shield]][github-url]
[![Kofi][kofi-shield]][kofi-url]
[![LinkedIn][linkedin-shield]][linkedin-url]
[![Khanakat][khanakat-shield]][khanakat-url]

## Usando herencia

Podemos definir la herencia entre dos clases usando la siguiente sintaxis:

```csharp
class DerivedClass: BaseClass
{
       
}

class DerivedSubClass: DerivedClass
{

}
```

Lo que esto significa es que `DerivedSubClass` hereda de `DerivedClass` y de `BaseClass` tambi�n, porque DerivedClasshereda de `BaseClass`. De esa manera, podemos compartir las caracter�sticas de la clase entre varias clases, aunque una clase solo puede heredar de una clase base .

Entonces, creemos una estructura de herencia b�sica:

```csharp
public class Writer
{
    public void Write()
    {
        Console.WriteLine("Writing to a file");
    }
}
public class XMLWriter: Writer
{
    public void FormatXMLFile()
    {
        Console.WriteLine("Formating XML file");
    }
}
public class JSONWriter: Writer
{
    public void FormatJSONFile()
    {
        Console.WriteLine("Formating JSON file");
    }
}
```

En este ejemplo, las clases `XMLWriter` y `JSONWriter` tienen sus propios m�todos, pero ambos comparten el m�todo `Write()` de la clase base `Writer`.

Entonces, si creamos un objeto de tipo `XMLWriter`, podremos acceder a su propio m�todo y al m�todo de la clase base:

```csharp
class Program
{
    static void Main(string[] args)
    {
        XMLWriter xmlWriter = new XMLWriter();
        xmlWriter.FormatXMLFile();
        xmlWriter.Write();
    }
}
```

Lo mismo ocurre con la clase `JSONWriter`.

## Llamar a constructores desde la clase base

Desde las clases derivadas podemos acceder al constructor de una clase base. Esto se usa con bastante frecuencia, debido a la inicializaci�n de algunas propiedades que se comparten entre clases derivadas. Podemos usar la basepalabra clave para ejecutar eso:

```csharp
public class Writer
{
    public string FileName { get; set; }

    public Writer(string fileName)
    {
        FileName = fileName;
    }

    public void Write()
    {
        Console.WriteLine("Writing to a file");
    }
}
public class XMLWriter: Writer
{
    public XMLWriter(string fileName)
        :base(fileName)
    {
    }

    public void FormatXMLFile()
    {
        Console.WriteLine("Formating XML file");
    }
}

public class JSONWriter: Writer
{
    public JSONWriter(string fileName)
        :base(fileName)
    {
    }

    public void FormatJSONFile()
    {
        Console.WriteLine("Formating JSON file");
    }
}
class Program
{
    static void Main(string[] args)
    {
        XMLWriter xmlWriter = new XMLWriter("xmlFileName");
        xmlWriter.FormatXMLFile();
        xmlWriter.Write();
        Console.WriteLine(xmlWriter.FileName);

        JSONWriter jsonWriter = new JSONWriter("jsonFileName");
        jsonWriter.FormatJSONFile();
        jsonWriter.Write();
        Console.WriteLine(jsonWriter.FileName);
    }
}
```

Como podemos ver, pasamos un valor de cadena a los constructores de la clase derivada y al usar la palabra clave `base`, estamos pasando ese valor de cadena al constructor de la clase base. All�, configuramos el valor de la propiedad `Name`.

## Acceso a clases

La jerarqu�a de herencia significa que nuestra `XMLWriter` (o `JSONWriter`) clase es un tipo especial de `Writer`, tiene todos los miembros no privados de Writer y caracter�sticas adicionales declaradas dentro de la clase de Writer XML (JSON). Pero existen algunas limitaciones para esta jerarqu�a.

Veamos el siguiente ejemplo:

```csharp
XMLWriter xml = new XMLWriter("file.xml");
Writer writer = xml;
writer.Write(); //ok Write is part of the Writer class
writer.FormatXML(); //error FormatXML is not part of the Writer class
```

Esto significa que si nos referimos al objeto `XMLWriter` o `JSONWriter` con el objeto `Writer`, podemos acceder a los m�todos declarados dentro de la clase Writer.

Hay una limitaci�n m�s. No podemos asignar un objeto de rango superior a un objeto de rango inferior:

```csharp
Writer writer = new Writer("any name");
XMLWriter xml = writer; //error
```

Pero podemos resolver este problema usando la aspalabra clave " ":

```csharp
XMLWriter xml = new XMLWriter("any name");
Writer writer = xml; //writer points to xml

XMLWriter newWriter = writer as XMLWriter; //this is ok now because writer was xml
newWriter.FormatXMLFile();
```

## Declaraci�n de m�todos con la nueva palabra clave

En el proyecto del mundo real, a menudo necesitamos tener tantas funcionalidades diferentes, y eso generalmente conduce a la existencia de muchos m�todos, propiedades diferentes, etc. A veces es bastante dif�cil encontrar un nombre �nico y significativo para nuestros identificadores, especialmente si tenemos la jerarqu�a de herencia. Tarde o temprano vamos a intentar reutilizar un nombre que ya est� siendo utilizado por una de las clases en el nivel jer�rquico superior. Si se trata de eso (tenemos dos m�todos con el mismo nombre en la clase derivada y base) vamos a recibir una advertencia:

![img01](/img/01.png)

## Usando la nueva palabra clave

Un m�todo en una clase derivada oculta un m�todo en una clase base con la misma firma. Entonces, como puede ver en la imagen de arriba, nuestro m�todo SetNameexiste en la clase `XMLWriter` y la clase `Writer`. Dado que la clase `XMLWriter` hereda de la clase `Writer`, oculta una implementaci�n del SetNamem�todo de la clase `Writer`.

Aunque nuestro c�digo se compilar� y se ejecutar�, debemos tomar esta advertencia en serio. Puede suceder que otra clase herede de la clase `XMLWriter` e implemente el SetNamem�todo. El desarrollador puede esperar ejecutar el SetNamem�todo de la clase `Writer` (porque XMLWriterhereda de Writer) pero este no es un caso. El SetNamem�todo de la clase `Writer` est� oculto por el SetNamem�todo de la clase `XMLWriter`.

Si nos encontramos en este tipo de situaci�n, la mejor forma es cambiar las firmas del m�todo. Pero si estamos seguros de que queremos un comportamiento como este, podemos usar la palabra clave `new`. La newpalabra clave simplemente le dir� al compilador que estamos cien por ciento seguros de lo que estamos haciendo y que ya no queremos que aparezca un mensaje de advertencia:

```csharp
public class Writer
{
    public string FileName { get; set; }

    public Writer(string fileName)
    {
        FileName = fileName;
    }

    public void Write()
    {
        Console.WriteLine("Writing to a file");
    }

    public void SetName()
    {
        Console.WriteLine("Setting name in the base Writer class");
    }
}
 
public class XMLWriter: Writer
{
    public XMLWriter(string fileName)
        :base(fileName)
    {
    }

    public void FormatXMLFile()
    {
        Console.WriteLine("Formating XML file");
    }

    public new void SetName()
    {
        Console.WriteLine("Setting name in the XMLWriter class");
    }
}
```

Ahora ya no tenemos un mensaje de advertencia.

## Declarar m�todos con la palabra clave virtual

A veces, no queremos ocultar una implementaci�n de un m�todo de una clase base con la misma firma que un m�todo de una clase derivada. Lo que queremos es brindar una oportunidad para una implementaci�n diferente de un m�todo con la misma firma en una clase derivada. Entonces, queremos anular nuestro m�todo de una clase base con el m�todo dentro de una clase derivada.

Un m�todo que se pretende anular se denomina m�todo virtual. Cuando hablamos de anular y ocultar, debemos ser claros con esos t�rminos. Ocultar significa que queremos ocultar completamente la implementaci�n de un m�todo de la clase base, pero la anulaci�n significa que queremos una implementaci�n diferente de un m�todo de una clase base.

Para crear un m�todo virtual usamos la `virtual` palabra clave:

```csharp
public class Writer
{
    public string FileName { get; set; }

    public Writer(string fileName)
    {
        FileName = fileName;
    }

    public void Write()
    {
        Console.WriteLine("Writing to a file");
    }

    public void SetName()
    {
        Console.WriteLine("Setting name in the base Writer class");
    }

    public virtual void CalculateFileSize()
    {
        Console.WriteLine("Calculating file size in a Writer class");
    }
}
```

## Declaraci�n de m�todos con la palabra clave de anulaci�n

Si declaramos un m�todo como `virtual` en nuestra clase base, podemos crear un m�todo en una clase derivada con la palabra clave `override` para declarar otra implementaci�n de ese m�todo:

```csharp
public class XMLWriter: Writer
{
    public XMLWriter(string fileName)
        :base(fileName)
    {
    }

    public void FormatXMLFile()
    {
        Console.WriteLine("Formating XML file");
    }

    public new void SetName()
    {
        Console.WriteLine("Setting name in the XMLWriter class");
    }

    public override void CalculateFileSize()
    {
        Console.WriteLine("Calculating file size in the XMLWriter class");
    }
}
```

Si queremos, podemos llamar a una implementaci�n original de ese m�todo en una clase derivada usando la `base` palabra clave:

```csharp
public class XMLWriter: Writer
{
    ...

    public override void CalculateFileSize()
    {
        base.CalculateFileSize();
        Console.WriteLine("Calculating file size in the XMLWriter class");
    }
}
```

Todas estas acciones de herencia y diferentes implementaciones de m�todos con las palabras clave mencionadas tienen su propio polimorfismo de nombre �nico.

## Reglas a seguir al trabajar con m�todos polim�rficos

Hay algunas reglas importantes que debemos seguir al declarar m�todos polim�rficos mediante el uso de las palabras clave virtual y override:

- No podemos declarar un m�todo virtual como privado. Su prop�sito es estar expuesto a una clase derivada, por lo que hacerlo privado no tiene sentido. Del mismo modo, los m�todos anulados no pueden ser privados porque una clase derivada no puede cambiar el nivel de protecci�n de un m�todo que hereda.
- Las firmas de los m�todos virtuales y anulados deben ser id�nticas
- Solo podemos anular un m�todo virtual. Si intentamos anular un m�todo que no tiene una palabra clave virtual, obtendremos un error
- Si no usamos la palabra clave override, no estamos reemplazando el m�todo, solo lo estamos ocultando. Si este es el comportamiento que queremos, debemos usar la nueva palabra clave
- Un m�todo anulado tambi�n es virtual, por lo que puede anularse en una clase derivada adicional


## Conclusi�n

En este art�culo, hemos aprendido:

- Que es la herencia y como se usa
- C�mo utilizar las palabras clave nuevas, virtuales y anuladas
- Reglas de polimorfismo en el lenguaje C #

<!--- reference style links --->
[github-shield]: https://img.shields.io/badge/-@fernandocalmet-%23181717?style=flat-square&logo=github
[github-url]: https://github.com/fernandocalmet
[kofi-shield]: https://img.shields.io/badge/-@fernandocalmet-%231DA1F2?style=flat-square&logo=kofi&logoColor=ff5f5f
[kofi-url]: https://ko-fi.com/fernandocalmet
[linkedin-shield]: https://img.shields.io/badge/-fernandocalmet-blue?style=flat-square&logo=Linkedin&logoColor=white&link=https://www.linkedin.com/in/fernandocalmet
[linkedin-url]: https://www.linkedin.com/in/fernandocalmet
[khanakat-shield]: https://img.shields.io/badge/khanakat.com-brightgreen?style=flat-square
[khanakat-url]: https://khanakat.com