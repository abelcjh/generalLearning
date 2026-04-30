# database password vs secret key
must first realize that for database (including supabase),

has two things,
- raw postgresql database
- set of apis wrapped around the database

## database password
in the DATABASE_URL,
password for the actual database
allow direct low level connections to database using standard sql protocol

### when needed
run database migrations using alembic
```bash
uv run alembic upgrade head
```
connect to database with traditional orms like sqlalchemy (fastapi likely uses this)
connect a database viewer software dbeaver or tableplus

## secret key
master api key to talk to supabase auto generated rest api (postgREST) and auth systems
bypass row level security

### when needed
perform admin tasks via supabase api
update data via supabase client library

## public key
opposite of secret key
has rls
expose to frontend for api