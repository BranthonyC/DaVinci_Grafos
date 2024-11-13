Here are some of the most important and frequently used commands in Neo4j's **Cypher query language**, which you’ll use to interact with the database.

### 1. **CREATE**: Add nodes and relationships
   - **Create a node**:
     ```cypher
     CREATE (n:Label {property: "value"})
     ```
     Example:
     ```cypher
     CREATE (p:Person {name: "Alice", age: 30})
     ```

   - **Create a relationship**:
     ```cypher
     MATCH (a:Person {name: "Alice"}), (b:Movie {title: "Inception"})
     CREATE (a)-[:LIKES]->(b)
     ```

### 2. **MATCH**: Retrieve data by pattern-matching
   - **Match nodes**:
     ```cypher
     MATCH (p:Person)
     RETURN p
     ```
   - **Match relationships**:
     ```cypher
     MATCH (p:Person)-[r:LIKES]->(m:Movie)
     RETURN p, r, m
     ```

### 3. **WHERE**: Filter results based on conditions
   - **Filter nodes or relationships**:
     ```cypher
     MATCH (p:Person)
     WHERE p.age > 25
     RETURN p
     ```

### 4. **RETURN**: Display results
   - **Return specific properties**:
     ```cypher
     MATCH (p:Person)
     RETURN p.name, p.age
     ```

### 5. **DELETE**: Remove nodes and relationships
   - **Delete a relationship**:
     ```cypher
     MATCH (p:Person)-[r:LIKES]->(m:Movie)
     DELETE r
     ```
   - **Delete a node** (only if it has no relationships):
     ```cypher
     MATCH (p:Person {name: "Alice"})
     DELETE p
     ```

### 6. **DETACH DELETE**: Remove nodes with their relationships
   ```cypher
   MATCH (p:Person {name: "Alice"})
   DETACH DELETE p
   ```

### 7. **SET**: Update or add properties
   - **Set a new property**:
     ```cypher
     MATCH (p:Person {name: "Alice"})
     SET p.age = 35
     ```
   - **Add a new label**:
     ```cypher
     MATCH (p:Person {name: "Alice"})
     SET p:Employee
     ```

### 8. **REMOVE**: Remove properties or labels
   - **Remove a property**:
     ```cypher
     MATCH (p:Person {name: "Alice"})
     REMOVE p.age
     ```
   - **Remove a label**:
     ```cypher
     MATCH (p:Person {name: "Alice"})
     REMOVE p:Employee
     ```

### 9. **MERGE**: Create a node or relationship only if it doesn’t already exist
   - **Merge a node**:
     ```cypher
     MERGE (p:Person {name: "Alice"})
     ```
   - **Merge a relationship**:
     ```cypher
     MATCH (a:Person {name: "Alice"}), (m:Movie {title: "Inception"})
     MERGE (a)-[:LIKES]->(m)
     ```

### 10. **WITH**: Chain multiple operations and pass results
   - **Use WITH for aggregation**:
     ```cypher
     MATCH (p:Person)-[:LIKES]->(m:Movie)
     WITH m, COUNT(p) AS likes
     RETURN m.title, likes
     ```

### 11. **ORDER BY**: Sort results
   ```cypher
   MATCH (p:Person)
   RETURN p.name, p.age
   ORDER BY p.age DESC
   ```

### 12. **LIMIT**: Restrict the number of results
   ```cypher
   MATCH (p:Person)
   RETURN p.name, p.age
   LIMIT 5
   ```

### 13. **UNWIND**: Expand a list into individual rows
   ```cypher
   UNWIND [1, 2, 3, 4] AS number
   RETURN number
   ```

### 14. **FOREACH**: Update data in loops
   ```cypher
   MATCH (p:Person {name: "Alice"})
   FOREACH (ignored IN range(1, 5) |
     CREATE (p)-[:FRIEND_OF]->(:Person {name: "Friend"})
   )
   ```

### 15. **CALL**: Execute a stored procedure or a subquery
   ```cypher
   CALL db.labels()
   ```

These commands cover the majority of operations you’ll need for creating, querying, updating, and managing your Neo4j database effectively!