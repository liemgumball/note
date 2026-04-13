> ==**SQL**== stands for _**Structured Query Language**_ and is a standard for communicating with  
> ==_relational databases_==.

## Target:

- Connecting and persisting to a ==**MySQL**== database
- Connecting and persisting to a ==**PostgreSQL**== database

---

  

> [!important] Both
> 
> ==**MySQL**== and ==**PostgreSQL**== are popular and open source **Relational Database Management Systems** (**RDBMSes**)

> [!info] MySQL  
> MySQL HeatWave is a fully managed database service for transactions, real- time analytics across data warehouses and data lakes, and machine learning services, without the complexity, latency, and cost of ETL duplication.  
> [http://mysql.com](http://mysql.com)  

> [!info] PostgreSQL  
> The world's most advanced open source database.  
> [http://postgresql.org](http://postgresql.org)  

## ==Docker==

Using ==**Docker**== to provision databases in containers.

> [!info] Docker: Accelerated Container Application Development  
> Docker is a platform designed to help developers build, share, and run container applications.  
> [http://docker.com](http://docker.com)  

> [!important] The main reason for using
> 
> ==**Docker**== containers throughout this chapter is to save us having to manually install each of the database command-line interfaces and servers onto our system.

## Connecting and persisting to a ==MySQL== database

```undefined
require('dotenv').config()
const mysql = require('mysql')

const db = mysql.createConnection({
	user: process.env.DB_MYSQL_USER,
	password: process.env.DB_MYSQL_PASSWORD,
})

db.query('CREATE DATABASE tasks')
db.query('USE tasks')

db.query(`
	CREATE TABLE tasks.tasks (
		id INT NOT NULL AUTO_INCREMENT,
		task TEXT NOT NULL, PRIMARY KEY ( id )
	);
`)
```

The `createConnection()` method exposed from the `mysql` module establishes a connection to the server based on the configuration and credentials passed to the method.

> [!info] npm: mysql  
> A node.  
> [https://www.npmjs.com/package/mysql](https://www.npmjs.com/package/mysql)  

## Connecting and persisting to ==PostgreSQL== database

```Plain
PGUSER=postgres
PGPASSWORD=PASSWORD
PGPORT=5432
```

```JavaScript
require('dotenv').config()
const pg = require('pg')

const db = new pg.Client({})

const CREATE_TABLE_SQL = `CREATE TABLE IF NOT EXISTS tasks (
  id SERIAL, task TEXT NOT NULL,
  PRIMARY KEY ( id )
);`

const INSERT_TASK_SQL = `INSERT INTO tasks (task) VALUES($1);`

const GET_TASKS_SQL = `SELECT * FROM tasks;`

db.connect((err) => {
	if (err) throw err

	db.query(CREATE_TABLE_SQL, (err) => {
		if (err) throw err
	}
}
```

The configuration information required for a connection to our ==**PostgreSQL**== database was specified in the `.env` file. We used the `dotenv` module to load this configuration information as environment variables to our [[NodeJS]] process.

> [!important] Notice that we
> 
> ==didn't have to== directly pass any of the ==environment variables== to the client. This is because the `pg` module automatically looks for specifically named variables  
> (_PGHOST_, _PGPASSWORD_, and _PGUSER_).