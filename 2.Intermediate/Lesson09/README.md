# Clases abstractas

[![Github][github-shield]][github-url]
[![Kofi][kofi-shield]][kofi-url]
[![LinkedIn][linkedin-shield]][linkedin-url]
[![Khanakat][khanakat-shield]][khanakat-url]

## Crear clases abstractas

Para crear una clase abstracta, usamos la palabra clave `abstract`. El �nico prop�sito de la clase abstracta es heredarse y no se puede instanciar:

![img01](/img/01.png)

Una clase abstracta puede contener m�todos abstractos. Un m�todo abstracto no contiene implementaci�n, solo una definici�n con la palabra clave `abstract`:

```csharp
public abstract void Print(string text);
```

Para implementar un m�todo abstracto en la clase que deriva de una clase abstracta, necesitamos usar la palabra clave `override`:

```csharp
public override void Print()
{
    //method implementation
}
```

Como pudimos ver en una imagen anterior, una clase abstracta no tiene que tener ning�n miembro abstracto, pero lo m�s importante es que si una clase tiene al menos un miembro abstracto, esa clase debe ser una clase abstracta. De lo contrario, el compilador informar� un error:

![img02](/img/02.png)

## Clases Selladas

Si queremos evitar que se herede nuestra clase, necesitamos usar la palabra clave `sealed`. Si alguien intenta usar una clase sellada como clase base, el compilador arrojar� un error:

![img03](/img/03.png)

## Conclusi�n

En este art�culo, hemos aprendido:

- C�mo crear una clase abstracta
- C�mo usar miembros abstractos y c�mo implementarlos
- Qu� es una clase sellada y su prop�sito

<!--- reference style links --->
[github-shield]: https://img.shields.io/badge/-@fernandocalmet-%23181717?style=flat-square&logo=github
[github-url]: https://github.com/fernandocalmet
[kofi-shield]: https://img.shields.io/badge/-@fernandocalmet-%231DA1F2?style=flat-square&logo=kofi&logoColor=ff5f5f
[kofi-url]: https://ko-fi.com/fernandocalmet
[linkedin-shield]: https://img.shields.io/badge/-fernandocalmet-blue?style=flat-square&logo=Linkedin&logoColor=white&link=https://www.linkedin.com/in/fernandocalmet
[linkedin-url]: https://www.linkedin.com/in/fernandocalmet
[khanakat-shield]: https://img.shields.io/badge/khanakat.com-brightgreen?style=flat-square
[khanakat-url]: https://khanakat.com