# Patr�n de dise�o: Adapter

[![Github][github-shield]][github-url]
[![Kofi][kofi-shield]][kofi-url]
[![LinkedIn][linkedin-shield]][linkedin-url]
[![Khanakat][khanakat-shield]][khanakat-url]

## Proyecto inicial

Imaginemos que tenemos una funcionalidad en la que convertimos la lista de fabricantes de autom�viles a formato JSON y la escribimos en la pantalla. Pero en lugar de una lista, se nos ha proporcionado una API que nos proporciona todos los fabricantes en formato XML.

Digamos que no podemos modificar la funcionalidad de la API existente (debido a las restricciones t�cnicas, como ser importados a nuestro proyecto desde otra soluci�n que no debemos modificar o como un paquete NuGet), por lo que tenemos que encontrar una forma de evitarlo.

Y la forma correcta de hacerlo es implementar el patr�n Adaptador para resolver este problema.

Comencemos con la creaci�n del modelo `Manufacturer` y un ejemplo simple de convertidor de objeto a XML:

```csharp
public class Manufacturer
{
    public string Name { get; set; }
    public string City { get; set; }
    public int Year { get; set; }
}
```

```csharp
public static class ManufacturerDataProvider
{
    public List<Manufacturer> GetData() =>
       new List<Manufacturer>
       {
            new Manufacturer { City = "Italy", Name = "Alfa Romeo", Year = 2016 },
            new Manufacturer { City = "UK", Name = "Aston Martin", Year = 2018 },
            new Manufacturer { City = "USA", Name = "Dodge", Year = 2017 },
            new Manufacturer { City = "Japan", Name = "Subaru", Year = 2016 },
            new Manufacturer { City = "Germany", Name = "BMW", Year = 2015 }
       };
}
```

```csharp
public class XmlConverter
{
    public XDocument GetXML()
    {
        var xDocument = new XDocument();
        var xElement = new XElement("Manufacturers");
        var xAttributes = ManufacturerDataProvider.GetData()
            .Select(m => new XElement("Manufacturer", 
                                new XAttribute("City", m.City),
                                new XAttribute("Name", m.Name),
                                new XAttribute("Year", m.Year)));

        xElement.Add(xAttributes);
        xDocument.Add(xElement);

        Console.WriteLine(xDocument);

        return xDocument;
    }
}
```

Como podemos ver, este es un c�digo bastante sencillo. Estamos recopilando datos del fabricante, creando un elemento de fabricantes ra�z y todos los subelementos de fabricante con sus atributos.

Despu�s de eso, estamos imprimiendo los resultados en la ventana de la consola para mostrar c�mo se ve el XML final.

As� es como `xDocument` deber�a verse:

![img01](/img/01.png)

Ahora implementemos una clase `JsonConverter`:

```csharp
public class JsonConverter
{
    private IEnumerable<Manufacturer> _manufacturers;

    public JsonConverter(IEnumerable<Manufacturer> manufacturers)
    {
        _manufacturers = manufacturers;
    }

    public void ConvertToJson()
    {
        var jsonManufacturers = JsonConvert.SerializeObject(_manufacturers, Formatting.Indented);

        Console.WriteLine("\nPrinting JSON list\n");
        Console.WriteLine(jsonManufacturers);
    }
} 
```

Este c�digo es a�n m�s simple porque solo serializamos nuestra lista de fabricantes en formato JSON.

Por supuesto, para que la serializaci�n funcione, necesitamos instalar la biblioteca `Newtonsoft.Json`, as� que no olvide hacerlo.

Excelente, tenemos nuestra funcionalidad JSON y la interfaz XML proporcionada. Pero ahora, necesitamos resolver un problema real. C�mo combinar esas dos interfaces para lograr nuestra tarea, que es convertir a los fabricantes de formato XML a JSON.

## Implementaci�n del adaptador

Como podemos ver, no hay forma de pasar un xDocumenta la clase `JsonConverter` y no deber�a haber uno, por lo que necesitamos crear la clase de adaptador que har� que estas dos interfaces funcionen juntas.

Para ello, vamos a empezar con la interfaz `IXmlToJson` para definir el comportamiento de nuestra clase adaptadora:

```csharp
public interface IXmlToJson
{
    void ConvertXmlToJson();
}
```

Luego, continuemos con la clase `XmlToJsonAdapter` que va a implementar la interfaz `IXmlToJson`:

```csharp
public class XmlToJsonAdapter : IXmlToJson
{
    private readonly XmlConverter _xmlConverter;

    public XmlToJsonAdapter(XmlConverter xmlConverter)
    {
        _xmlConverter = xmlConverter;
    }

    public void ConvertXmlToJson()
    {
        var manufacturers = _xmlConverter.GetXML()
                .Element("Manufacturers")
                .Elements("Manufacturer")
                .Select(m => new Manufacturer
                             {
                                City = m.Attribute("City").Value,
                                Name = m.Attribute("Name").Value,
                                Year = Convert.ToInt32(m.Attribute("Year").Value)
                             });

        new JsonConverter(manufacturers)
            .ConvertToJson();
    }
}
```

Excelente. Hemos creado nuestra clase de adaptador que convierte el objeto de documento Xml en la lista de fabricantes y proporciona esa lista a la clase `JsonConverter`.

Entonces, como puede ver, hemos habilitado la colaboraci�n entre dos interfaces completamente diferentes con solo introducir una clase de adaptador en nuestro proyecto.

Ahora, podemos hacer una llamada a esta clase de adaptador desde nuestra clase de cliente:

```csharp
class Program
{
   static void Main(string[] args)
    {
        var xmlConverter = new XmlConverter();
        var adapter = new XmlToJsonAdapter(xmlConverter);
        adapter.ConvertXmlToJson();
    }
}
```

Una vez que iniciemos nuestra aplicaci�n, veremos el siguiente resultado:

![img01](/img/01.png)

## Cu�ndo usar el adaptador

Debemos usar la clase Adapter siempre que queramos trabajar con la clase existente pero su interfaz no es compatible con el resto de nuestro c�digo. B�sicamente, el patr�n Adaptador es una capa intermedia que sirve como traductor entre el c�digo implementado en nuestro proyecto y alguna clase de terceros o cualquier otra clase con una interfaz diferente.

Adem�s, deber�amos usar el Adaptador cuando queramos reutilizar clases existentes de nuestro proyecto pero carecen de una funcionalidad com�n. Al usar el patr�n Adaptador en este caso, no necesitamos extender cada clase por separado y crear un c�digo redundante.

## Conclusi�n

El patr�n Adapter es bastante com�n en el mundo de C # y se usa bastante cuando tenemos que adaptar algunas clases existentes a una nueva interfaz. Puede aumentar la complejidad de un c�digo agregando clases adicionales (adaptadores) pero vale la pena un esfuerzo seguro.

<!--- reference style links --->
[github-shield]: https://img.shields.io/badge/-@fernandocalmet-%23181717?style=flat-square&logo=github
[github-url]: https://github.com/fernandocalmet
[kofi-shield]: https://img.shields.io/badge/-@fernandocalmet-%231DA1F2?style=flat-square&logo=kofi&logoColor=ff5f5f
[kofi-url]: https://ko-fi.com/fernandocalmet
[linkedin-shield]: https://img.shields.io/badge/-fernandocalmet-blue?style=flat-square&logo=Linkedin&logoColor=white&link=https://www.linkedin.com/in/fernandocalmet
[linkedin-url]: https://www.linkedin.com/in/fernandocalmet
[khanakat-shield]: https://img.shields.io/badge/khanakat.com-brightgreen?style=flat-square
[khanakat-url]: https://khanakat.com