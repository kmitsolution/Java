

# JPA-Hibernate
JPA is a specification and defines the way to manage relational database data using java objects. Hibernate is an implementation of JPA. It is an ORM tool to persist java objects into the relational databases.

## Example:- Create a Simple JPA Project with Hibernate using H2 Database
1. Create a project using <a href=https://start.spring.io/ > Spring Initializr </a>
2. Setup <b>Group</b> com.jpa.springboot , <b>Artifact</b> jpa-hibernate 
3. Add dependencies Spring Web, Spring Data JDBC, Spring Data JPA, H2 Database, Validation
4. Open the project in Eclipse.
5. To Connect with H2 add below lines in applicaiton.properties file
    ```
      spring.h2.console.enabled=true
      spring.datasource.url=jdbc:h2:mem:testdb
    ```
6. Open H2 Database using <a href=http://localhost:8080/h2-console>http://localhost:8080/h2-console</a>
7. Add schema.sql file and below table definition
```
create table Book
(
  id bigint not null,
  name varchar(30) not null,
  author varchar(255) not null,
  primary key(id)
);
```
8. Open H2 Database using <a href=http://localhost:8080/h2-console>http://localhost:8080/h2-console</a> . You will see the book table now in H2.
9. You can run the select/insert/update sql queries in the Query window of H2 console.
10. Let's do these sql operations using JPA
11. Add below class to 

```java
package com.jpa.springboot.jpahibernate.book.jdbc;

public class Book {
private int id;
private String name;
private String Author;
public Book(int id, String name, String author) {
	super();
	this.id = id;
	this.name = name;
	Author = author;
}
public int getId() {
	return id;
}
public String getName() {
	return name;
}

public String getAuthor() {
	return Author;
}



}

```

```java
package com.jpa.springboot.jpahibernate.book.jdbc;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.jdbc.core.JdbcTemplate;
import org.springframework.stereotype.Repository;

@Repository
public class BookJdbcRepository {

	@Autowired
	private JdbcTemplate springJdbcTemplate;
	private static String INSERT_QUERY="insert into book values(?,?,?);";
	private static String DELETE_QUERY="delete from book where id=?;";
	public void insert(Book book) {
		springJdbcTemplate.update(INSERT_QUERY,book.getId(),book.getName(),book.getAuthor());
	}
	public void delete(long id) {
		springJdbcTemplate.update(DELETE_QUERY,id);
	}
			
}




```

```java
package com.jpa.springboot.jpahibernate.book.jdbc;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.CommandLineRunner;
import org.springframework.stereotype.Component;

@Component
public class BookJdbcCommandLineRunner implements CommandLineRunner{

	@Autowired
	private BookJdbcRepository repoistory;
	@Override
	public void run(String... args) throws Exception {
		// TODO Auto-generated method stub= 
		Book book = new Book(1,"Azure","Book1");
		repoistory.insert(new Book(1,"Azure","Book1"));
		repoistory.insert(new Book(2,"Azure104","Book2"));
		repoistory.insert(new Book(3,"Azure400","Book3"));
		repoistory.delete(1);
	}

}


```
