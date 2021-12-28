# Patr�n de dise�o: Facade

[![Github][github-shield]][github-url]
[![Kofi][kofi-shield]][kofi-url]
[![LinkedIn][linkedin-shield]][linkedin-url]
[![Khanakat][khanakat-shield]][khanakat-url]

## �Qu� es un patr�n de fachada?

Como sugiere el nombre, representa una "fachada" para que el usuario final simplifique el uso de los subsistemas que est�n mal dise�ados y / o son demasiado complicados al ocultar sus detalles de implementaci�n. Tambi�n resulta �til cuando se trabaja con bibliotecas y API complejas.

Un patr�n de fachada est� representado por una interfaz de clase �nica que es simple, f�cil de leer y usar, sin el problema de cambiar los propios subsistemas. Sin embargo, debemos tener cuidado ya que limitar el uso de las funcionalidades del subsistema puede no ser suficiente para los usuarios avanzados.

## Ejemplo de patr�n de fachada

Como ejemplo para explicar mejor el patr�n de fachada, describiremos el flujo de trabajo de pedir comida en l�nea.

Digamos que tenemos una lista de restaurantes. Abrimos la p�gina del restaurante, buscamos el plato que nos gusta y lo a�adimos al carrito. Lo hacemos tantas veces como queramos y completamos el pedido. Cuando enviamos el pedido, recibimos una confirmaci�n del pedido junto con el precio del pedido.

Primero, creemos una clase llamada Orderque representar� el orden proveniente del Usuario:

```csharp
public class Order
{
    public string DishName { get; set; }
    public double DishPrice { get; set; }
    public string User { get; set; }
    public string ShippingAddress { get; set; }
    public double ShippingPrice { get; set; }

    public override string ToString()
    {
        return string.Format("User {0} ordered {1}. The full price is {2} dollars.",
            User, DishName, DishPrice + ShippingPrice);
    }
}
```

Adem�s, tenemos que crear dos clases m�s: un restaurante en l�nea y un servicio de env�o. La clase `OnlineRestaurant` proporciona m�todos para agregar pedidos al carrito:

```csharp
public class OnlineRestaurant
{
    private readonly List<Order> _cart;

    public OnlineRestaurant()
    {
        _cart = new List<Order>();
    }

    public void AddOrderToCart(Order order)
    {
        _cart.Add(order);
    }

    public void CompleteOrders()
    {
        Console.WriteLine("Orders completed. Dispatch in progress...");
    }
}
```

Por otro lado, la clase `ShippingService` acepta el pedido y lo env�a a la direcci�n almacenada en la propiedad `ShippingAddress` dentro de la clase `Order`. El `ShippingService` tambi�n calcula los gastos de env�o y se los muestra al usuario:

```csharp
public class ShippingService
{
    private Order _order;

    public void AcceptOrder(Order order)
    {
        _order = order;
    }

    public void CalculateShippingExpenses()
    {
        _order.ShippingPrice = 15.5;
    }

    public void ShipOrder()
    {
        Console.WriteLine(_order.ToString());
        Console.WriteLine("Order is being shipped to {0}...", _order.ShippingAddress);
    }
}
```

Al final, estamos incorporando toda la l�gica en la clase `Main` para representar el flujo de trabajo de pedir comida en l�nea:

```csharp
class Program
{
    static void Main(string[] args)
    {
        var restaurant = new OnlineRestaurant();
        var shippingService = new ShippingService();

        var chickenOrder = new Order() { DishName = "Chicken with rice", DishPrice = 20.0, User = "User1", ShippingAddress = "Random street 123" };
        var sushiOrder = new Order() { DishName = "Sushi", DishPrice = 52.0, User = "User2", ShippingAddress = "More random street 321" };

        restaurant.AddOrderToCart(chickenOrder);
        restaurant.AddOrderToCart(sushiOrder);
        restaurant.CompleteOrders();

        shippingService.AcceptOrder(chickenOrder);
        shippingService.CalculateShippingExpenses();
        shippingService.ShipOrder();

        shippingService.AcceptOrder(sushiOrder);
        shippingService.CalculateShippingExpenses();
        shippingService.ShipOrder();

        Console.ReadLine();
    }
}
```

El resultado de la implementaci�n actual de la `Main` clase es:

![img01](/img/01.png)

Nota: Asumimos que los pedidos vienen del exterior y por eso los creamos dentro de la Mainclase. Esto es opcional, por supuesto, para sistemas m�s complicados, esto tambi�n ser�a parte de alg�n servicio.

Ahora, para aquellos de ustedes que se preguntan:

"�Por qu� est� mal esto?"

Sigue leyendo.

Al observar la clase `Main` y todos los pasos que hemos implementado, podemos ver una gran cantidad de c�digo en una sola clase. Dado que tendemos a hacer las cosas m�s f�ciles de leer y menos complicadas, tenemos que hacer algunos ajustes.

Y ah� es donde interviene el patr�n de fachada.

## Implementaci�n del patr�n de fachada

Uno de los objetivos del Patr�n de fachada es ocultar los detalles de implementaci�n, lo que indica que tener todo en la Mainclase no funciona. Es demasiada informaci�n innecesaria, por lo tanto, nos gustar�a m�s en otro lugar.

Dicho esto, vamos a crear otra clase llamada `Facade`. La clase `Facade` actuar� como un "middleware" entre el Usuario y la complejidad del sistema sin cambiar la l�gica empresarial:

```csharp
public class Facade
{
    private readonly OnlineRestaurant _restaurant;
    private readonly ShippingService _shippingService;

    public Facade(OnlineRestaurant restaurant, ShippingService shippingService)
    {
        _restaurant = restaurant;
        _shippingService = shippingService;
    }

    public void OrderFood(List<Order> orders)
    {
        foreach (var order in orders)
        {
            _restaurant.AddOrderToCart(order);
        }

        _restaurant.CompleteOrders();

        foreach (var order in orders)
        {
            _shippingService.AcceptOrder(order);
            _shippingService.CalculateShippingExpenses();
            _shippingService.ShipOrder();
        }
    }
}
```

Como hemos movido la l�gica de implementaci�n a la clase `Facade`, podemos simplificar la clase `Main`:

```csharp
class Program
{
    static void Main(string[] args)
    {
        var restaurant = new OnlineRestaurant();
        var shippingService = new ShippingService();

        var facade = new Facade(restaurant, shippingService);

        var chickenOrder = new Order() { DishName = "Chicken with rice", DishPrice = 20.0, User = "User1", ShippingAddress = "Random street 123" };
        var sushiOrder = new Order() { DishName = "Sushi", DishPrice = 52.0, User = "User2", ShippingAddress = "More random street 321" };

        facade.OrderFood(new List<Order>() { chickenOrder, sushiOrder });

        Console.ReadLine();
    }
}
```

Cuando ejecutamos el c�digo, podemos ver el resultado exacto:

![img02](/img/02.png)

Esto significa que hemos liberado con �xito al usuario de la presi�n innecesaria de conocer todos los pasos necesarios para que llegue la comida.

Nota: en este ejemplo, pasamos el `OnlineRestaurant` y el `ShippingService` al Facade, asumiendo que ya est�n creados. Sin embargo, tambi�n se pueden crear instancias dentro de `Facade` en s� mismo.

## Conclusi�n

Entonces, hemos visto c�mo el patr�n de fachada puede ayudarnos a facilitar la vida del cliente. Ahora, estamos listos para adoptar las complejas implementaciones tal como est�n. Y por �ltimo, pero no menos importante, en determinadas situaciones, el uso de este patr�n requiere precauci�n. Puede limitar las capacidades del usuario para hacer uso de todo el potencial de la aplicaci�n o biblioteca que estamos tratando de simplificar.

<!--- reference style links --->
[github-shield]: https://img.shields.io/badge/-@fernandocalmet-%23181717?style=flat-square&logo=github
[github-url]: https://github.com/fernandocalmet
[kofi-shield]: https://img.shields.io/badge/-@fernandocalmet-%231DA1F2?style=flat-square&logo=kofi&logoColor=ff5f5f
[kofi-url]: https://ko-fi.com/fernandocalmet
[linkedin-shield]: https://img.shields.io/badge/-fernandocalmet-blue?style=flat-square&logo=Linkedin&logoColor=white&link=https://www.linkedin.com/in/fernandocalmet
[linkedin-url]: https://www.linkedin.com/in/fernandocalmet
[khanakat-shield]: https://img.shields.io/badge/khanakat.com-brightgreen?style=flat-square
[khanakat-url]: https://khanakat.com