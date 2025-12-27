# DATA MODELS AND QUERY LANGUAGES

Data models shape not only how software is built, but also how developers think about the problems they are solving. Most applications are composed of multiple layers of data models, where each layer represents the one above it while hiding lower-level complexity. Different data models—such as relational, document, and graph models—come with different assumptions, strengths, and limitations. Choosing the right data model is critical, because it determines what an application can do efficiently and what becomes difficult or impossible.

## Relational Model Versus Document Model

The relational model, introduced by Edgar Codd in 1970, organizes data into tables of rows and columns and became the dominant data model by the mid-1980s. Originally designed for business data processing, relational databases proved highly flexible and scalable as computing evolved. Despite many competing data models over the years, relational databases have remained widely used for decades and continue to power a large portion of modern web applications.

### The Object-Relational Mismatch

Most modern applications are written in object-oriented languages, which creates an **object-relational mismatch** when storing data in relational tables. ORMs like ActiveRecord and Hibernate help, but differences remain. For data structures like résumés or profiles, **JSON representations** reduce this mismatch by keeping all related data in a single document, preserving one-to-many relationships as an explicit tree structure. This simplifies queries and improves data locality compared to traditional multi-table relational schemas.

### Query Languages for Data

SQL is a **declarative query language**, unlike imperative database code used in IMS or CODASYL. Declarative queries specify **what data to retrieve and how to transform it**, not **how to execute the query**. This allows the database to optimize access paths, reorder operations, and parallelize execution automatically. Imperative queries are harder to optimize or parallelize because they specify **exact steps and order**. SQL’s declarative nature makes it concise, flexible, and efficient, especially for modern multi-core and distributed systems.

### MapReduce Querying

**MapReduce** is a programming model for distributed, bulk data processing. In MongoDB, `map` emits key-value pairs for each document, and `reduce` aggregates values by key. Unlike declarative SQL, MapReduce uses JavaScript functions and is lower-level. Pure function restrictions allow distributed and fault-tolerant execution. For convenience, MongoDB later introduced the **Aggregation Pipeline**, a declarative, JSON-based query language similar to SQL, making queries simpler and more optimizable.

## Graph-Like Data Models

When many-to-many relationships are common, **graph models** are more natural than relational or document models. A graph consists of **vertices (nodes)** and **edges (relationships)**. Examples include social networks, the web graph, and transportation networks. Graphs can store both homogeneous and heterogeneous objects, enabling complex queries and algorithms like shortest path and PageRank. Social networks like Facebook use a single graph with multiple vertex and edge types to model users, locations, events, and interactions.

### Property Graphs

In the Property Graph model, each vertex has a unique ID, incoming and outgoing edges, and a set of key-value properties. Each edge connects two vertices, has a label, and its own properties. Graphs can be stored relationally with a table for vertices and a table for edges, with indexes for efficient traversal. This model allows flexible many-to-many relationships, supports heterogeneous data, and is highly evolvable—new features and data types can be added easily without redesigning the entire schema.

### The Cypher Query Language

**Cypher** is a declarative query language for property graphs (Neo4j). Vertices and edges can be created with symbolic names, and relationships are expressed using arrow notation. Queries, such as finding people born in the US but living in Europe, use patterns to match vertices and edges. Cypher hides execution details from the developer, letting the query optimizer decide the most efficient way to traverse the graph. This makes querying complex graph relationships easier and more efficient, similar to SQL for relational data.

### Graph Queries in SQL

Graph data **can be stored in relational tables**, but querying it with SQL is more cumbersome. Recursive relationships (variable-length paths) require **recursive CTEs (WITH RECURSIVE)**. For example, finding people born in the US and living in Europe can be done in 4 lines in Cypher, but takes 29 lines in SQL. This illustrates that **different data models are optimized for different use cases**, and choosing the right model is crucial for your application.