## Project: **Neo4j Movie Social Network**

### Objective
Students will create a mini social network using Neo4j where users (people) can connect as friends and share movie recommendations. The goal is to practice creating and managing nodes and relationships, querying the database, and analyzing connections.

### Step-by-Step Guide

#### 1. **Set Up the Database**

   - **Goal**: Set up the Neo4j database and understand how to create basic nodes and relationships.

   - **Steps**:
      1. Create a new database in Neo4j (using Neo4j Desktop or Neo4j Aura).
      2. Familiarize yourself with the Neo4j Browser interface.

#### 2. **Create Nodes for People and Movies**

   - **Goal**: Learn how to create nodes and set properties.

   - **Tasks**:
      - **People**: Create nodes for each person, with properties like `name`, `age`, and `location`.
         ```cypher
         CREATE (alice:Person {name: 'Alice', age: 24, location: 'New York'})
         CREATE (bob:Person {name: 'Bob', age: 30, location: 'Chicago'})
         CREATE (carol:Person {name: 'Carol', age: 28, location: 'Los Angeles'})
         ```
      - **Movies**: Create nodes for a few movies, with properties like `title`, `year`, and `genres` (as an array).
         ```cypher
         CREATE (inception:Movie {title: 'Inception', year: 2010, genres: ['Sci-Fi', 'Thriller']})
         CREATE (matrix:Movie {title: 'The Matrix', year: 1999, genres: ['Sci-Fi', 'Action']})
         ```

#### 3. **Create Relationships**

   - **Goal**: Understand how to create relationships between nodes.

   - **Tasks**:
      - **Friendships**: Establish friendship relationships between people.
         ```cypher
         MATCH (a:Person {name: 'Alice'}), (b:Person {name: 'Bob'})
         CREATE (a)-[:FRIENDS_WITH {since: '2023'}]->(b)
         ```
      - **Movie Recommendations**: Create "recommended" relationships from each person to their favorite movies.
         ```cypher
         MATCH (p:Person {name: 'Alice'}), (m:Movie {title: 'Inception'})
         CREATE (p)-[:RECOMMENDS]->(m)
         ```

#### 4. **Query the Data**

   - **Goal**: Practice retrieving data using Cypher queries.

   - **Tasks**:
      - Find all people and return their names, ages, and locations.
         ```cypher
         MATCH (p:Person)
         RETURN p.name, p.age, p.location
         ```
      - List all movies recommended by a specific person.
         ```cypher
         MATCH (p:Person {name: 'Alice'})-[:RECOMMENDS]->(m:Movie)
         RETURN m.title, m.year
         ```
      - Retrieve friends of a specific person.
         ```cypher
         MATCH (p:Person {name: 'Alice'})-[:FRIENDS_WITH]-(friend:Person)
         RETURN friend.name, friend.age
         ```

#### 5. **Update and Delete Data**

   - **Goal**: Learn how to modify or delete properties and relationships.

   - **Tasks**:
      - **Add Properties**: Add a new property `email` to each person.
         ```cypher
         MATCH (p:Person {name: 'Alice'})
         SET p.email = 'alice@example.com'
         RETURN p
         ```
      - **Delete a Relationship**: Remove a friendship or recommendation.
         ```cypher
         MATCH (a:Person {name: 'Alice'})-[r:FRIENDS_WITH]-(b:Person {name: 'Bob'})
         DELETE r
         ```

#### 6. **Aggregation and Advanced Queries**

   - **Goal**: Learn to perform aggregation and more complex querying.

   - **Tasks**:
      - Find the count of friends for each person.
         ```cypher
         MATCH (p:Person)-[:FRIENDS_WITH]-(friend:Person)
         RETURN p.name, count(friend) AS friends_count
         ```
      - List the most recommended movies.
         ```cypher
         MATCH (p:Person)-[:RECOMMENDS]->(m:Movie)
         RETURN m.title, count(p) AS recommendation_count
         ORDER BY recommendation_count DESC
         ```

#### 7. **Extra Challenges (Optional)**

   - **Path Finding**: Find the shortest path between two people.
      ```cypher
      MATCH path = shortestPath(
        (p1:Person {name: 'Alice'})-[:FRIENDS_WITH*]-(p2:Person {name: 'Carol'})
      )
      RETURN path
      ```
   - **Genre Matching**: Find all movies of a specific genre that are recommended by a user's friends.
      ```cypher
      MATCH (p:Person {name: 'Alice'})-[:FRIENDS_WITH]->(friend)-[:RECOMMENDS]->(m:Movie)
      WHERE 'Sci-Fi' IN m.genres
      RETURN friend.name, m.title
      ```

---

## Practical Exercises

1. **Create Additional People**: Add more nodes representing people with properties like `name`, `age`, and `interests`.
2. **Add Movie Recommendations**: Link people with movies they recommend.
3. **Find Friend Recommendations**: Query movies recommended by the friends of a specific person.
4. **Add Advanced Filters**: Create a query to list movies released after a certain year, filtered by genre.
5. **Aggregation Challenge**: Count the total number of movies recommended by each person.

### Final Report and Presentation

1. **Report**: Each student should summarize their project, including screenshots of their Cypher queries and results.
2. **Presentation**: Each student can present a 5-minute overview of their database, sharing insights from their queries and any interesting findings.

This project allows students to practice fundamental Cypher skills and explore Neo4j's capabilities. Good luck, and have fun experimenting!