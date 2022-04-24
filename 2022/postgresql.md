# PostgreSQL on Node Quick Start

1. Start a postgres instance on docker and connect to it:

```sh
docker run --name some-postgres -p 5432:5432 -e POSTGRES_PASSWORD=mysecretpassword -d postgres
docker exec -it some-postgres /bin/bash
```

2. Connect to database as user `postgres` (administrator), then:

```sql
create database hellodb;
create user hellouser with password 'hellouser';
grant all privileges on database hellodb to hellouser;
```

3. Connect to database as user hellouser

```sh
psql postgres://hellouser:hellouser@localhost/hellodb
```

4. Create table

```sql
create table hellotable (name text);
insert into hellotable values ('Hello World');
```

## Using Postgres in Node

```javascript
const { Pool } = require('pg');
const pool = new Pool({
    connectionString: process.env.DATABASE_URL,
    ssl: {
        rejectUnauthorized: false,
    }
});

// Assuming an Express app is initialized
app.get('/db', async (req, res) => {
    try {
        const client = await pool.connect();
        const result = await client.query('SELECT * FROM test_table');
        const results = { 'results': (result) ? result.rows : null};

        // Assuming there is a rendering engine installed
        res.render('pages/db', results);
        client.release();
    } catch (err) {
        console.error(err);
        res.send('Error ' + err);
    }
});
```

> To Be Continued...

