# simple-sql-generator
This project is my version of a simple SQL query generator using Java Reflection API, from the original tutorial on [PluralSight](https://www.pluralsight.com/courses/java-fundamentals-reflection-api-method-handles): 
**Java 8 Fundamentals: The Java Reflection API Method Handles.**
The main purpose of the project is to generate CRUD query with defined models or entities.

The Java Reflection API is a powerful tool that allows developers to inspect and manipulate classes, methods, fields, and other elements of the Java programming language at runtime. It provides a way to access and modify the behavior of classes and objects dynamically, which can be useful for various purposes such as debugging, testing, and building frameworks.

In this use case, I use Reflection API to generate SQL queries for CRUD operations based on the structure of the entity classes. All the work is done in the `SimpleCrudQueryBuilder` class, which takes an entity class as input and generates the corresponding SQL queries for CRUD operations.

CRUD stands for:
- **C**reate   = Insert for the SQL
- **R**etrieve = Select for the SQL
- **U**pdate   = Update for the SQL
- **D**elete   = Delete for the SQL

```java
class SimpleCrudQueryBuilderTest {

    private static final String EXPECTED_SELECT_BY_ID_QUERY = "SELECT id,firstname,lastname,telephone,email,gender,address FROM client WHERE id=?";
    private static final String EXPECTED_SELECT_QUERY = "SELECT id,firstname,lastname,telephone,email,gender,address FROM client";
    private static final String EXPECTED_INSERT_QUERY = "INSERT INTO client VALUES id=?,firstname=?,lastname=?,telephone=?,email=?,gender=?,address=?";
    private static final String EXPECTED_UPDATE_QUERY = "UPDATE client SET firstname=?,lastname=?,telephone=?,email=?,gender=?,address=? WHERE id=?";
    private static final String EXPECTED_DELETE_QUERY = "DELETE FROM client WHERE id=?";

    private SimpleCrudQueryBuilder<Client> queryBuilder;

    @BeforeEach
    public void setUp() {
        queryBuilder = new SimpleCrudQueryBuilder<>(Client.class);
    }

    @Test
    void testBuildFindByIdQuery() {
        assertEquals(EXPECTED_SELECT_BY_ID_QUERY, queryBuilder.buildFindByIdQuery());
    }

    @Test
    void testBuildFindAllQuery() {
        assertEquals(EXPECTED_SELECT_QUERY, queryBuilder.buildFindAllQuery());
    }

    @Test
    void testBuildInsertQuery() {
        assertEquals(EXPECTED_INSERT_QUERY, queryBuilder.buildInsertQuery());
    }

    @Test
    void testBuildUpdateQuery() {
        assertEquals(EXPECTED_UPDATE_QUERY, queryBuilder.buildUpdateQuery());
    }

    @Test
    void testBuildDeleteQuery() {
        assertEquals(EXPECTED_DELETE_QUERY, queryBuilder.buildDeleteQuery());
    }
}
```

Here is what it looks like.
- The entity here is: `Client`