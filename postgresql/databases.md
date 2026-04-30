# connection types
postgresql databases have hard limits on number of active connections at any time
so need different connection types to prevent crashing

## transaction pooler connection
port 6543
pooler holds small number of permanent connections to database
rapidly share them among your serverless functions, prevent connection exhaustion

### why use for serverless
serverless apps spin up rapidly, create many simultaneous short-lived connections

## direct connection
port 5432
continuous, uninterrupted session

### why use for database migrations
can execute complex schema changes

like running:
```bash
uv run alembic upgrade head
```

### why cannot use pooler for database migrations
they swap connections mid transaction
disrupt long running schema changes

# connection string format
`postgresql://postgres.[PROJECT_REF]:[PASSWORD]@aws-0-xx.pooler.supabase.com:6543/postgres`

**postgresql://**: the database protocol
**postgres.[PROJECT_REF]**: database user and specific project id
**[PASSWORD]**: database password
**@aws-0-xx.pooler.supabase.com**: host address of database, xx is the region
**:6543**: port number (change to 5432 for direct connection)
**/postgres**: default database name