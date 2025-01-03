# Data Models and Query Languages

## Data Models
There are two main types of data models:
- **Relational Model**: data is organized into relationships between tables where each relation is an unordered collection of tuples (rows in SQL).
- **Document Model (NoSQL)**: data is organized into documents with nested fields where data is considered self-contained in each document and relationhips between documents are rare.
- **Property Graph Model (NoSQL)**: data is organized into vertices and edges where anything is potentially related to everything.

## Relational Model
Relational databases were designed to handle **transaction processing**, such as entering a banking transaction., and batch processing, such as calculating the monthly payroll.

The relational model can be referred to as a **schema-on-write** model, meaning that the schema is defined before data is written to the database.

### Impedance Mismatch
Most programming languages are object-oriented, but relational databases are not. An **impedance mismatch** refers to the difficulty of mapping between the two.

Object Relational Mapping (ORM) is a tool that bridges the gap between the two, but they introduce overhead.

## Document Model
Document databases were designed to reduce impedance mismatch by using more flexible data structures, such as JSON. 

The document model can be referred to as a **schema-on-read** model, meaning that the schema is defined when the data is read from the database.

Advantages:
- JSON has better **locality** than relational tables, meaning that it is easier to access data that is stored close to each other. It handles one-to-many relationships more naturally.

Disadvantages:
- JSON makes it more difficult to establish many-to-one and many-to-many relationships.

## Property Graph Model
The property graph model is a data model that is similar to the document model, but it is designed to handle many-to-one and many-to-many relationships more naturally.

The syntax of most graph databases involves identifying the **vertices** (nodes) and **edges** (relationships between nodes).

### Cypher (Neo4j)
Cypher queries are composed of identifying the tail vertex, relationship edge, and head vertex. For example, the query `(alice)-[:knows]->(bob)` identifies the vertex `alice`, the relationship edge `knows`, and the vertex `bob`.

### SPARQL (RDF)
SPARQL is a query language for Resource Description Framework (RDF) data. RDF was a legacy concept that was intended to be a standard way to represent data in the web.

RDF data is stored in a **triple store**, which is a database that stores data in the form of triples (subject, predicate, object). An example SPARQL query is `SELECT ?subject WHERE { ?subject ?predicate ?object }`.

