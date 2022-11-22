# Sesion Practica

## Pre-requisitos 

* Tener java instalado  y un jdk 17 o mayor.

* tener instalado el [IDE Eclipse](https://www.eclipse.org/downloads/) y en la instalacion seleccionar con "Eclipse IDE for java developers".

* Conexion a internet

![eclipse](/imagenes/eclipse.png)

## Creacion del proyecto 

Para esta sesion practica usaremos un proyecto del tipo Maven. Al momento de crearlo,la damos check a "create a simple proyect" y damos next. Ahora llenamos los campos "Group Id" y "Artifact Id" (Que sera el nombre de nuestro proyecto Maven, pueden poner el nombre que gusten mientras no ocupen palabras reservadas).

![maven](/imagenes/mavenCreate.png)

Al tener nuestro proyecto creado, vamos a hacerle una limpieza Maven e instalarle nuevamente las propiedades de Maven. Esto para evitar errores de copilacion por lo que es necesario tener una conexion a internet.< 

Para esto, solo damos click derecho -> Run As -> Maven Clean 

El proceso se mostrara a la izquirda inferior con una pequeña barra de progreso.

![clean](/imagenes/cleanMaven.png)

Y ahora hacemos casi el mismo proceso click derecho -> Run As -> Maven Install

Al final debe salirte el copilador con un "BUILD SUCCESS".

## Cambiar version de JRE

Abrimos el proyecto y en la carpeta "JRE System Library" y damos click derecho -> properties

y ahora buscamos la version 1.8 y le damos a "Apply & Close"

![jre](/imagenes/propiedadesjre.png)


## Dependencias / librerias a usar

Antes de crear cualquier archivo, ocupamos las librerias para correr hibernate y un driver para conectarnos a una base de datos. En este caso usaremos Mysql por lo tengo ocuparemos el Driver Mysql.

Para obtener las librerias en Maven, debemos dirigirnos al archivo "pom.xlm" en donde estan las propiedades del proyecto maven. El siquiente codigo es lo que debes de mirar.

``` xml

<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>hibernateJava</groupId> <!-- Nombre que pusieron -->
  <artifactId>hibernateJava</artifactId><!-- Nombre que pusieron -->
  <version>0.0.1-SNAPSHOT</version>
</project>

```

Entre </version> y </project> agregaremos las siguientes lineas de codigo.

``` xml

  <!-- https://mvnrepository.com/artifact/org.hibernate/hibernate-core -->
<dependencies>

	<dependency>
	<groupId>org.hibernate</groupId>
    <artifactId>hibernate-core</artifactId>
    <version>5.4.10.Final</version>
	</dependency>
	<!-- https://mvnrepository.com/artifact/com.mysql/mysql-connector-j -->
	<dependency>
    	<groupId>com.mysql</groupId>
    	<artifactId>mysql-connector-j</artifactId>
    	<version>8.0.31</version>
	</dependency>


</dependencies>

```

Por lo que terminaria algo parecido a esto:

``` xml

<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>hibernateJava</groupId> <!-- Nombre que pusieron -->
  <artifactId>hibernateJava</artifactId><!-- Nombre que pusieron -->
  <version>0.0.1-SNAPSHOT</version>


  <!-- https://mvnrepository.com/artifact/org.hibernate/hibernate-core -->
    <dependencies>

	    <dependency>
	    <groupId>org.hibernate</groupId>
        <artifactId>hibernate-core</artifactId>
        <version>5.4.10.Final</version>
	    </dependency>
	    <!-- https://mvnrepository.com/artifact/com.mysql/mysql-connector-j -->
	    <dependency>
    	<groupId>com.mysql</groupId>
    	<artifactId>mysql-connector-j</artifactId>
    	<version>8.0.31</version>
	    </dependency>

    </dependencies>
</project>

```

Lo guardamos y al momento se nos creara una carpeta nueva llamada "Maven Dependecies" donde se descargara automaticamente las librerias que ocupamos para usar Hibernate y el Driver de Mysql (la conexion que ocupamos para la base de datos).


## Archivo de configuracion 

Creamos un nuevo archivo como se muestra y lo llamamos hibernate.cfg.xml

![crearArchivo](/imagenes/crearArchivo.png)


Copia lo sigueinte y pegalo en el archivo recien creado.


``` xml

<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE hibernate-configuration PUBLIC "-//Hibernate/Hibernate Configuration DTD 3.0//EN" "http://www.hibernate.org/dtd/hibernate-configuration-3.0.dtd">
<hibernate-configuration>
    <session-factory>
    <property name="connection.driver_class">com.mysql.jdbc.Driver</property>
    <property name="connection.url">jdbc:mysql://localhost/hibernate1</property>
    <property name="connection.username">hibernate1</property>
    <property name="connection.password">hibernate1</property>
    <property name="dialect">org.hibernate.dialect.MySQLDialect</property>
    <property name="hibernate.show_sql">true</property>
    </session-factory>
</hibernate-configuration>

```

A continuacion te doy los datos de la base de datos que ocuparas acceder

Host: sql9.freesqldatabase.com
Database name: sql9579656
Database user: sql9579656
Database password: sJDimXFGP4
Port number: 3306

Asignamos los datos en sus respectivos valores y terminaremos con este archivo de configuracion de hibernate. (En la sesion se explica lo que hace cada propiedad).

## Creando Clase

Ahora en el mismo espacio de scr/main/java creamos una clase llamada "ingeniero" en tendra los atributos de id, nombre y Estado.


``` java

public class ingeniero {
	private int id;
	private String nombre;
	private String Estado;
	
	public ingeniero() {} // constructor vacio

}

```

Y agregamos los gets y sets al igual que un constructor completo. Por lo que la clase terminaria algo asi.

``` java

public class ingeniero {
	private int id;
	private String nombre;
	private String Estado;
	
	public ingeniero() {} // constructor vacio

	public ingeniero(int id, String nombre, String estado) {
		this.id = id;
		this.nombre = nombre;
		Estado = estado;
	}

	public int getId() {
		return id;
	}

	public void setId(int id) {
		this.id = id;
	}

	public String getNombre() {
		return nombre;
	}

	public void setNombre(String nombre) {
		this.nombre = nombre;
	}

	public String getEstado() {
		return Estado;
	}

	public void setEstado(String estado) {
		Estado = estado;
	}
	
	@Override
	public String toString() {
		return "ingeniero [id=" + id + ", nombre=" + nombre + ", Estado=" + Estado + "]";
	}
	

}

```

## Mapeado en Tabla 

Ahora bien, en un inicio de ocupa agregar una instruccion en el hibernate.cfg.xml para el mapeo de una clase a tabla, sin embargo, podemos usar anotaciones en nuestra clase que queremos que se identifique como tabla y tener una lectura aun mas clara de lo que identificamos como tabla.

En nuestra misma clase ingeniero, importaremos "javax.persistence.*" (el * para no repetir cada anotacion), y agregaremos las anotaciones @Entity , @Table y @Column en sus respectivos espacios, como se muestra a continuacion.

``` java
@Entity


@Table (name= "ingenieros") // El nombre de la tabla de la base de datos
public class ingeniero {
    @Column (name= "id") //nombre de la columna de la base de datos
	private int id;

    @Column (name= "nombre")
	private String nombre;

    @Column (name= "Estado")
	private String Estado;
	
	public ingeniero() {} // constructor vacio

    ....
}

```

## Generar Conexion 

Ahora creamos otra clase en el cual la llamaremos "Main" o "inicio", como gusten.

Dentro de nuestra clase main agregaremos el siguiente codigo que se ocupa para utilizar hibernate.

``` java
import org.hibernate.Session;
import org.hibernate.SessionFactory;
import org.hibernate.Transaction;
import org.hibernate.boot.registry.StandardServiceRegistryBuilder;
import org.hibernate.cfg.Configuration;


public class inicio {

	public static void main(String[] args) {
		
		Configuration confi = new Configuration().configure("hibernate.cfg.xml"); //Usamos la configuracion realizada en el archivo hibernate
		confi.addAnnotatedClass(player.class); //agregamos el mapeo de nuestra clase
		StandardServiceRegistryBuilder builder = new StandardServiceRegistryBuilder().applySettings(confi.getProperties()); //contruimos un servicio con lo que esta en la configuracion
		
		
		SessionFactory factory = confi.buildSessionFactory(builder.build()); //
		Session session = factory.openSession();
		Transaction trans = session.beginTransaction();

        //Proceso de CRUD que desee realizar 
        trans.commit();
		session.close();
	}

}

```

Por ultimo, especificamos que queremos realizar en el CRUD. En el cual, en vez de tener clases para separar la generacio de la conexion y donde se realiza el query. Se reducira en estas simples funciones.


``` java

	session.save(); // Create
	session.get(player.class, 03); // Read
	session.update(p1); // Update
	session.delete(p1); // Delete

```
Remplazando donde este el comentario "CRUD". : )
