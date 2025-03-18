

# Object Relational Mapping (ORMs)
ORMs provide an object-oriented approach to managing relational database queries and interactions. They close the gap between application objects and SQL for consistency and ease of use.

## SQLAlchemy (Python)
SQLAlchemy is an ORM that technically has two core APIs: (1) **Core** APIs (i.e., closer to raw SQL queries) and (2) **ORM** APIs. The ORM API is built on top of the Core API to provider a nicer abstraction layer typical of ORMs. The ORM API is typically used first, but the Core APIs enable lower level optimization. SQLAlchemy 2.0+ introduced better support for Python types.

SQLAlchemy integrates with Alembic for database migrations.

### Engine

```python
# Synchronous
from sqlalchemy import create_engine

DB_TYPE = 'postgresql'
DB_API = 'psycopg3' # Python's DBAPI specification is a low-level API used by Python to interact with databases. psycopg3 is a popular postgresql adapter and is compatible with SQLAlchemy 2.0.

POSTGRES_USER = 'username'
POSTGRES_PASSWORD = 'password'
POSTGRES_HOST = 'some-db.us.east-1.rds.amazonaws.com'
POSTGRES_DB = 'my_db'
DB_ADDRESS = f'{POSTGRES_USER}:{POSTGRES_PASSWORD}@{POSTGRES_HOST}:{POSTGRES_PORT}/{POSTGRES_DB}'
DATABASE_URL = f'{DB_TYPE}+{DB_API}://{DB_ADDRESS}'
engine = create_engine(DATABASE_URL)


# Asynchronous
from sqlalchemy.ext.asyncio import create_async_engine
async_engine = create_async_engine(DATABASE_URL)
```

### Transactions

### Metadata and Schemas

### CRUD Operations


## Drizzle (Typescript)
Drizzle is a Typescript-native ORM focused on an object-oriented approach to database interactions. It pairs nicely with `zod` for generating Typescript types from its database schemas. This combination is particularly powerful because it can enforce consistency starting from the database to inbound requests. 

```mermaid
flowchart LR
    db[(Database)] --> drizzle[Drizzle Schema]
    drizzle --> types[TypeScript Types]
    types --> zod[Zod Schemas]
    zod --> routes[API Routes]
    routes --> client[Frontend Client]
    
    classDef db fill:#4b5563,color:white
    classDef drizzle fill:#3178c6,color:white
    classDef types fill:#6366f1,color:white
    classDef zod fill:#ef4444,color:white
    classDef routes fill:#22c55e,color:white
    classDef client fill:#8b5cf6,color:white
    
    class db db
    class drizzle drizzle
    class types types
    class zod zod
    class routes routes
    class client client
```

### Schema

```typescript

// schema.ts
export const usersTable = pgTable('users', {
  id: serial('id').primaryKey(),
  firstName: text('first_name').notNull(),
  lastName: text('last_name').notNull(),
  userName: text('username').notNull().unique(),
  createdAt: timestamp('created_at').defaultNow().notNull(),
});

export const postsTable = pgTable('posts', {
  id: serial('id').primaryKey(),
  title: text('title').notNull(),
  text: text('text'),
  userId: integer('user_id').references(() => usersTable.id),
  createdAt: timestamp('created_at').defaultNow().notNull(),
});

```
### Connection

```typescript
// db.ts
const DATABASE_URL = `postgres://${process.env.POSTGRES_USER}:${process.env.POSTGRES_PASSWORD}@${process.env.POSTGRES_HOST}:${process.env.POSTGRES_PORT}/${process.env.POSTGRES_DB}`;
export const db = drizzle(DATABASE_URL, { schema });
```
