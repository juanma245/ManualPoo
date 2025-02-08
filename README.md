# Manual de programación orientada a objetos.

## Introducción

¿Qué es la Programación orientada a objeto?
La Programación Orientada a Objetos (POO) es un paradigma de programación que organiza el software en torno a "objetos", que son instancias de "clases". Estos objetos contienen datos (atributos) y comportamientos (métodos) que operan sobre esos datos.

## Conceptos básicos de la programación orientada a objetos

### Clases y objetos

**Clase**: se puede definir como una plantilla la cual define los atributos y métodos que tiene un objeto, esto se puede entender como las propiedades y comportamientos del objeto, la obtención de estas propiedades y comportamientos se realiza mediante la abstracción, que es extraer las propiedades principales que debe cumplir un objeto.
**Objeto**: es una instancia o ejemplar de una clase, esa representa la entidad especifica, la cual sigue la plantilla definida en la clase.

Para ejemplificar estos dos conceptos podemos tomar como ejemplo la creación de una clase auto, abstrayendo las características principales podemos obtener que sus propiedades pueden ser, la marca, el color y la velocidad, y su comportamiento es acelerar, frenar y mostrar a qué velocidad se mueve, con este proceso se puede crear la clase o la plantilla que debe seguir cualquier objeto para ser un auto.

```java
// Definición de una clase
public class Coche {
    // Atributos (propiedades)
    String marca;
    String color;
    int velocidad;

    // Métodos (comportamientos)
    public void acelerar(int incremento) {
        velocidad += incremento;
    }

    public void frenar(int decremento) {
        velocidad -= decremento;
    }

    public void mostrarVelocidad() {
        System.out.println("Velocidad actual: " + velocidad + " km/h");
    }
}

// Creación de un objeto
public class Main {
    public static void main(String[] args) {
        Coche miCoche = new Coche(); // Instancia de la clase Coche
        miCoche.marca = "Toyota";
        miCoche.color = "Rojo";
        miCoche.acelerar(50);
        miCoche.mostrarVelocidad(); // Salida: Velocidad actual: 50 km/h
    }
}
```

Este es un ejemplo simple, el cual tiene un problema, y es que desde la función main se puede modificar libremente los atributos del objeto accediendo directamente a ellos, esto no es recomendable, solo el objeto debería ser capaz de modificar sus características, por lo cual se recomienda encapsular las pripeidades del objeto y permitir su acceso y modificación mediante el uso de métodos getters y setters.

### Encapsulamiento

El encapsulamiento es el proceso mediante el cual se protegen los datos de un objeto con el fin de restringir el acceso directo a ellos, usando modificadores de acceso y métodos getters(los cuales te permiten obtener los atributos) y setters(los cuales te permiten modificar los atributos), en java existen diferentes modificadores de acceso los cuales son private, public y protected, en este caso el mas importante y usado es el private, que hace que solo la clase pueda modificar el atributo directamente, es decir, fuera de esa clase el atributo es inaccesible sin un método getter o setter.

```java
public class CuentaBancaria {
    // Atributo privado
    private double saldo;

    // Método público para acceder al saldo (getter)
    public double getSaldo() {
        return saldo;
    }

    // Método público para modificar el saldo (setter)
    public void depositar(double cantidad) {
        if (cantidad > 0) {
            saldo += cantidad;
        }
    }
}
```

En el ejemplo se puede ver un uso del encapsulamiento, donde se crea la clase cuenta bancaria que cuenta con el atributo saldo, este atributo esta encapsulado con el modificador private, ya que de no ser así, no se podría controlar la forma en la que se modifica este atributo desde una clase externa, lo cual es peligroso para este ejemplo, para poder acceder al atributo se usa la función getSaldo(getter) el cual devuelve el saldo de la cuenta, y la función depositar(setter) la cual permite que la clase decida la forma en la que se modifica el saldo de la cuenta, teniendo mas control y seguridad sobre el atributo.

### Función constructora

En algunos casos se quiere que, al crear un objeto, el usuario ingrese unos datos iniciales, esto se realiza usando una función constructora, esta es una función que asigna valores a algunos atributos al momento de crear el objeto, esos pueden ser todos los atributos del objeto o solo algunos, Un constructor tiene el mismo nombre que la clase y no tiene un tipo de retorno explícito.

```java
// Definición de la clase Persona
public class Persona {
    // Atributos (propiedades)
    private String nombre;
    private int edad;

    // Constructor
    public Persona(String nombre, int edad) {
        this.nombre = nombre;
        this.edad = edad;
    }

    // Métodos (comportamientos)
    public void mostrarInformacion() {
        System.out.println("Nombre: " + nombre);
        System.out.println("Edad: " + edad);
    }

    // Método principal para probar la clase
    public static void main(String[] args) {
        // Creación de un objeto usando el constructor
        Persona persona1 = new Persona("Juan Pérez", 25);

        // Llamada a un método para mostrar la información
        persona1.mostrarInformacion();
    }
}
```

En el ejemplo se puede ver la creación de una clase persona, la cual cuenta con los atributos nombre y edad, la función constructora hace la función de inicializar los datos de la persona, ya que no se puede crear un objeto persona sin saber su edad o nombre, note que se usa la palabra reservada this, esta palabra hace referencia a la clase actual en la que se encuentra, esto para saber que el atributo que se esta modificando es el atributo de esa clase, y no el enviado en forma de parámetro de la función constructora, en la clase main, al memento de crear la instancia de la clase, se deben enviar los parámetros pedidos por la función constructora.

### Herencia

La herencia te permite crear una clase la cual parte de una clase ya existente, eso quiere decir que la clase hija o subclase, hereda todos los atributos y métodos de la clase padre o superclase, esto también hace que herede la función constructora, por lo cual es necesario llamar a la función constructora del padre, para poder inicializar al hijo, esto se hace de una manera simple, con la palabra reservada super la cual llama a la función constructora del padre, dentro de la función constructora del hijo, teniendo esto en cuenta es importante que al crear a la función constructora del hijo, se pidan también los atributos necesarios para llamar a la función constructora del padre.

```java
// Clase base (superclase)
public class Vehiculo {
    // Atributos privados (encapsulamiento)
    private String marca;
    private int año;

    // Constructor de la clase base
    public Vehiculo(String marca, int año) {
        this.marca = marca;
        this.año = año;
    }

    // Métodos getters (para acceder a los atributos privados)
    public String getMarca() {
        return marca;
    }

    public int getAño() {
        return año;
    }

    // Método para mostrar información del vehículo
    public void mostrarInformacion() {
        System.out.println("Marca: " + marca);
        System.out.println("Año: " + año);
    }
}

// Subclase (hereda de Vehiculo)
public class Coche extends Vehiculo {
    // Atributo privado adicional
    private int numPuertas;

    // Constructor de la subclase
    public Coche(String marca, int año, int numPuertas) {
        // Llamada al constructor de la clase base (superclase)
        super(marca, año);
        this.numPuertas = numPuertas;
    }

    // Método getter para el atributo adicional
    public int getNumPuertas() {
        return numPuertas;
    }

    // Sobrescritura del método mostrarInformacion
    @Override
    public void mostrarInformacion() {
        super.mostrarInformacion(); // Llama al método de la superclase
        System.out.println("Número de puertas: " + numPuertas);
    }
}

// Clase principal para probar la herencia
public class Main {
    public static void main(String[] args) {
        // Creación de un objeto de la subclase Coche
        Coche miCoche = new Coche("Toyota", 2020, 4);

        // Uso de métodos heredados y propios
        miCoche.mostrarInformacion();
    }
}
```

En el ejemplo se puede ver la creación de una clase llamada vehículo, la cual cuanta con los atributos marca y año, su clase constructora y sus métodos getter y setter, se muestra la creación de una clase coche la cual hereda esos atributos de la clase vehículo, esto se realiza con la palabra reservada extends la cual le dice a java, que la clase coche hereda de la clase vehículo, se puede ver que la clase coche tiene un atributo propio el cual es el numero de puertas, y se ve como en la función constructora se usa el super, para llamar al constructor de vehículo, en la clase main se puede ver que al crear una clase coche, esta puede usar los métodos de la clase vehículo, esto gracias a la herencia.

### Polimorfismo

Permite que objetos de diferentes laces respondan al mismo mensaje de manera diferente, es decir, que los mismos métodos respondan de manera diferente al ser llamados, eso se hace usando herencia, y la sobreescritura de métodos, es decir, que un hijo, sobrescriba la función definida por el padre, para poder hacer eso, se debe escribir @override, justo antes de la función que se desea sobrescribir, esto para que java sepa que esa es una sobreescritura y pueda adaptarse a eso, se pueden usar interfaces para conseguir este resultado.

```java
// Superclase
public class Animal {
    public void hacerSonido() {
        System.out.println("Sonido genérico de animal.");
    }
}

// Subclase
public class Perro extends Animal {
    @Override
    public void hacerSonido() {
        System.out.println("Guau guau!");
    }
}

// Subclase
public class Gato extends Animal {
    @Override
    public void hacerSonido() {
        System.out.println("Miau!");
    }
}

// Uso del polimorfismo
public class Main {
    public static void main(String[] args) {
        Animal miAnimal = new Perro();
        miAnimal.hacerSonido(); // Salida: Guau guau!

        miAnimal = new Gato();
        miAnimal.hacerSonido(); // Salida: Miau!
    }
}
```

En el ejemplo se puede ver la creación de tres clases, la clase animal, y las clases gato y perro las cuales heredan de la clase animal, vemos que la clase animal tiene el método hacerSonido definido, sin embargo, un perro y un gato no hacen el mismo sonido, por lo que necesitan sobrescribir la función, se puede ver como se usa la etiqueta @override para indicar que es una sobreescritura.

### Clases abstractas

Es una clase la cual permite definir métodos sin implementación, es decir, es decir las clases hijas que hereden de una clase abstracta esta obligada a implementar la funcionalidad de la función para crear una función abstracta se debe crear la clase con la palabra reservada abstract.

```java
// Clase abstracta
public abstract class Figura {
    public abstract double calcularArea();
}

// Subclase
public class Circulo extends Figura {
    double radio;

    public Circulo(double radio) {
        this.radio = radio;
    }

    @Override
    public double calcularArea() {
        return Math.PI * radio * radio;
    }
}

// Uso de la abstracción
public class Main {
    public static void main(String[] args) {
        Figura miFigura = new Circulo(5);
        System.out.println("Área del círculo: " + miFigura.calcularArea());
    }
}
```

En el ejemplo se puede ver como se crea la clase figura, la cual tiene un método que calcula el área, sin embargo, no todas las figuras calculan su área de la misma manera por lo cual es conveniente en este caso hacer abstracta esa clase, para que las clases hijas implementen su propia forma de calcular su área, luego se crea la clase circulo la cual hereda de figura, por lo cual necesita implementar la función calcular Área, esto lo hace sobrescribiendo la función, y así como se puede hacer con el circulo, se puede usar la clase abstracta para que todas las figuras implementen su forma de calcular el área.