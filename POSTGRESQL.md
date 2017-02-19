# PostgreSQL

### Users
+ Select all active users in the current database:
       SELECT * FROM pg_stat_activity;

### Activies
+ Stop a activity
      SELECT pg_cancel_backend(pid of the postgres process);

+  Stop all activies

        SELECT pg_terminate_backend(pg_stat_activity.pid)
        FROM pg_stat_activity
        WHERE pg_stat_activity.datname = 'TARGET_DB'
        AND pid <> pg_backend_pid();

### Size
+ Check a database size

      select t1.datname AS db_name, pg_size_pretty(pg_database_size(t1.datname)) as db_size
      from pg_database t1
      order by pg_database_size(t1.datname) desc;

+ Check the size of each table

        SELECT nspname || '.' || relname AS "relation",
        pg_size_pretty(pg_total_relation_size(C.oid)) AS "total_size"
        FROM pg_class C
        LEFT JOIN pg_namespace N ON (N.oid = C.relnamespace)
        WHERE nspname NOT IN ('pg_catalog', 'information_schema')
        AND C.relkind <> 'i'
        AND nspname !~ '^pg_toast'
        ORDER BY pg_total_relation_size(C.oid) DESC
        LIMIT 20;

### Generating files
+ Generate a file by a query input
        Copy (<query>) To '/tmp/sc.txt' With CSV;

## Command line

+ `\l or \list`	-> list all databases
+ `\dt`-> list all tables in the current database
+ `\connect <database_name>`-> switch the database
+ `psql -h <host> -U <user-name> -d <db-name> -a -f <file>` -> Run a sql file using command line
