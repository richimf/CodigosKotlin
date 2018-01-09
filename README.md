# DESIGN PATTERNS #

### CATEGORIAS ###

* CREATIONAL: Como crear objetos.
	- Builder, Dependency Injection, Singleton

* STRUCTURAL: Como componer objetos.
	- Adapter, Facade

* BEHAVIORAL: Como coordinar interacciones entre objetos.
	-Command, Observer, Model View Controller, Model View ViewModel, Clean Architecture

### CREATIONAL ###
#### BUILDER ####
Cuando queremos crear un objeto y poco a poco lo vamos haciendo mas complejo.
Gracias a esto, podriamos crear muchos objetos con diferentes caracteristicas, evitando crear muchos constructores en una clase.
Generalmente tiene esta estructura:

>Podemos ver que se usa "un punto" y una "funcion()""
```java
AlertDialog.Builder(this)
  .setTitle("My title")
  .setMessage("A message")
  .show()
```

>Ejemplo de como se crea una clase usando Pattern Builder:
```java
public static class MyClassBuilder {

	private MyClassBuilder mb;

		//Constructor
		public MyClassBuilder(){
			mb = new MyClassBuilder();
		}

		//Example of method using Pattern Builder
		public MyClassBuilder setColor(Color color){
			mb.color = color;
			return this; // <---
		}

		//etc...
}
```

#### DEPENDENCY INJECTION ####
La inyección de dependencias tiene que proveerte de cualquier objeto que se necesite cuando hagas una instancia de un nuevo objeto.
El nuevo objeto no necesita construir o perzonalizar los objetos.
En Android, aveces necesitamos acceder a los mismos objetos complejos desde varios lugares en la App. Se pueden inyectar estos objetos dentro de los Activities o Fragments y acceder a ellos.

>Una Inyección de Dependencias es una tecnica para inicializar una variable en lugar de explicitamente crear un servicio objeto, como se muestra:
```java
// An example without dependency injection
public class Client {
    // Internal reference to the service used by this client
    private ExampleService service;

    // Constructor
    Client() {
        // Specify a specific implementation in the constructor instead of using dependency injection
        service = new ExampleService();
    }

    // Method within this client that uses the services
    public String greet() {
        return "Hello " + service.getName();
    }
}
```

>Ahora utilizando Inyección de Dependencias:
```java
// Service setter interface.
public interface ServiceSetter {
    public void setService(Service service);
}

// Client class
public class Client implements ServiceSetter {
    // Internal reference to the service used by this client.
    private Service service;

    // Set the service that this client is to use.
    @Override
    public void setService(Service service) {
        this.service = service;
    }
}

//MAIN CLASS
public class Injector {
    public static void main(String[] args) {
        // Build the dependencies first
        Service service = new ExampleService();

        // Inject the service, constructor style
        Client client = new Client(service);

        // Use the objects
        System.out.println(client.greet());
    }	
}
```
Ver [Dragger](https://google.github.io/dagger/android.html) para Android: 























