# Intro
Hibernate is an ORM that implements JPA (Java Persistence API).
`SessionFactory` and `Session` are two important concepts. `SessionFactory` creates Sessions which is responsible for managing the configuration settings, database connections and caching.
# Basic Example
```xml title:hibernate.cfg.xml
<!DOCTYPE hibernate-configuration PUBLIC

        "-//Hibernate/Hibernate Configuration DTD 3.0//EN"

        "http://www.hibernate.org/dtd/hibernate-configuration-3.0.dtd">
<hibernate-configuration>
    <session-factory>
        <!-- JDBC Database connection settings -->
        <property name="connection.driver_class">oracle.jdbc.OracleDriver</property>
        <property name="connection.url">jdbc:oracle:thin:@//localhost:1521/orclpdb</property>
        <property name="connection.username">hr</property>
        <property name="connection.password">hr</property>
        <property name="show_sql">true</property>
        <property name="hbm2ddl.auto">update</property>
		<property name="current_session_context_class">thread</property>
    </session-factory>

</hibernate-configuration>
```
```java title:Main.java
import org.hibernate.SessionFactory
import org.hibernate.cfg.Configuration

public class Main{

	public static void Main(String[] args){
		Configuration configuration = new Configuration()
									.configure("hibernate.cfg.xml")
									.addAnnotatedClass(Player.class);
		SessionFactory sessionFactory = configuration.buildSessionFactory();
		Session session = sessionFactory.getCurrentSession();
		session.beginTransaction();
		session.close();
		sessionFactory.close();
		
	}
}
```
```java title:Player.java
package model; 
import javax.persistence.Entity;
import javax.persistence.Id;
@Entity(name = "Players") 
public class Player{
	@Id
	@GeneratedValue(strategy = GenerationType.IDENTITY)
	@Column(name = "id_example")
	int id; 
	
	String name;
	int level; 
}
```
---
## Values for hbm2ddl.auto

| Value       | Action                                           |
| ----------- | ------------------------------------------------ |
| validate    | Validates schema against mappings                |
| update      | Updates the schema to match mappings             |
| create      | Drops and recreates schema on startup<br>        |
| create-drop | Creates schema on startup, drops on shutdown     |
| none        | No action is taken on the schema<br>hbm2ddl.auto |
## Relationships
JPA links related entities using join column on the "one" side and join table on the "many" side.

>[!note] Mapping Relationships Between Classes
>E.g: When using `@OneToOne(mappedBy = "")`, the class in which this is written, there will be no join column in the corresponding generated table.

>[!warning] OneToOne Relationship
>You MUST enforce the unique constraint to ensure the OneToOne relationship is functioning as expected by writing `@JoinColumn(unique = true)`.

>[!info] Default Behavior of `@OneToMany` 
>The `@OneToMany` will behave as a `@ManyToMany` relationship, if the `mappedBy` attribute is not set. However if it's set, no extra table will be created. 

>[!info] Default Behavior of `@ManyToMany` 
>The `@ManyToMany` will create two join tables, since it tries to insert a join column in each table but as that's not possible on the "many" side it creates a join table place of the join column.

### Cascading 

| Cascade Operation      | Description                                                                                                                                                                                                                                                                                                                                             |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **PERSIST** _(save)_   | If the parent entity is persisted, then all its related entities will also be persisted.                                                                                                                                                                                                                                                                |
| **MERGE** _(update)_   | If the parent entity is merged, then all its related entities will also be merged.                                                                                                                                                                                                                                                                      |
| **DETACH**             | If the parent entity is detached, then all its related entities will also be detached.<br><br>In JPA, *detach* refers to the process of removing an entity from the persistence context. Once an entity is detached, it becomes unmanaged, meaning JPA will no longer track changes to that entity, and those changes won't be automatically persisted. |
| **REFRESH** _(select)_ | If the parent entity is refreshed, then all its related entities will also be refreshed.                                                                                                                                                                                                                                                                |
| **REMOVE** _(delete)_  | If the parent entity is removed, then all its related entities will also be removed.                                                                                                                                                                                                                                                                    |
| **ALL**                | All the above cascade operations can be applied to the entities related to the parent entity.                                                                                                                                                                                                                                                           |
### Fetching
There are two types of fetching strategies _LAZY_ & _EAGER_. Lazy does not perform join operation until the child entity is accessed while eager performs the join operation once the the parent is fetched.

#### Default JPA Fetching Behavior

| Relationship | fetchType |
| ------------ | --------- |
| OneToOne     | EAGER     |
| ManyToOne    | EAGER     |
| OneToMany    | LAZY      |
| ManyToMany   | LAZY      |


### example
Here in this example `Person` is referred to as the parent entity.
```java title:Person.java
@Entity
public class Person {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private int id;
    private String name;
    private int age;
    @OneToOne(cascade = CascadeType.MERGE)
    private Passport passport;
```
## ETC

> [!warning] Hibernate Requires Default Constructor In Entity Classes
> For hibernate to be able to return an object it requires the default constructor as well as setter methods.
### Hibernate Annotations
- `@Entity` to designate a class as a model for a database table
- `@Id` to designate the primary key attribute.
- `@GeneratedValue(strategy = "GenerationType.AUTO")` to designate how keys are generated.
- `@Column()` to change column name or add unique or null constraints.
- `@OneToOne(mappedBy = "")`
- `@JoinColumn()`
- `@JoinTable(name = "", joinColumns = @JoinColumn(), inverseJoinColumns = @JoinColumn() )`


