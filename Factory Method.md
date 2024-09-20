Explicación: El patrón Factory Method permite crear objetos sin especificar la clase exacta del objeto que se creará. Esto es útil cuando quieres dejar que las subclases decidan qué tipo de objeto crear.

Ejemplo: Crear diferentes cartas del juego (Monstruos y Hechizos).


// Producto
public abstract class Carta
{
    public abstract string Nombre { get; }
    public abstract void Jugar();
}

// Producto Concreto
public class CartaMonstruo : Carta
{
    public override string Nombre => "Dragón Blanco de Ojos Azules";

    public override void Jugar()
    {
        Console.WriteLine($"{Nombre} ha sido invocado al campo.");
    }
}

// Producto Concreto
public class CartaHechizo : Carta
{
    public override string Nombre => "Olla de la Avaricia";

    public override void Jugar()
    {
        Console.WriteLine($"{Nombre} ha sido activada.");
    }
}

// Creador
public abstract class Jugador
{
    public abstract Carta CrearCarta();

    public void JugarCarta()
    {
        var carta = CrearCarta();
        carta.Jugar();
    }
}

// Creador Concreto
public class JugadorMonstruo : Jugador
{
    public override Carta CrearCarta()
    {
        return new CartaMonstruo();
    }
}

// Creador Concreto
public class JugadorHechizo : Jugador
{
    public override Carta CrearCarta()
    {
        return new CartaHechizo();
    }
}

// Uso
class Program
{
    static void Main(string[] args)
    {
        Jugador jugadorMonstruo = new JugadorMonstruo();
        jugadorMonstruo.JugarCarta(); // Invoca una carta de monstruo

        Jugador jugadorHechizo = new JugadorHechizo();
        jugadorHechizo.JugarCarta(); // Activa una carta de hechizo
    }
}
