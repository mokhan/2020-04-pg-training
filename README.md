Postgresql trianing - Laurenz Albe

April. 27, 2020

* Read the docs: www.postgresql.org/docs/11/index.html
* Mailing list: www.postgresql.org/list/
  * pgsql-general
  * pgsql-hackers : development list
* Wiki: wiki.postgresql.org

Install
* postgresql-debuginfo package.
  * it doesn't hurt. doesn't slow things down.
  * if you get a crash from pg, then you can create a stack trace for anyone who needs to support you.
  * `perf` tool on linux can be used for performance monitoring.
* postgresql11-contrib
  * defined in appendix F.
  * always install this.
* user: postgres
  * dedicated user to run postgres
* create a database cluster
  * unfortunate name.
  * does not mean mutliple machines.
  * it's like an instance
  * it's a directory with files and a number of processes running against those files.

```text
  cluster

|----------|
| postgres |
|----------| -- (tcp:5432/unix) listen --
| course   |
|----------|
```

you cannot join tables between two different databases.

Shared between databases:

* users
* tablespaces

To create a cluster:

```bash
$ initdb -D $DATA_DIR -E UTF8 --locale=en_US.utf8
```

interesting options:

* --encoding=ENCODING (Always use UTF-8)
* --locale=LOCALE
* --lc-collate, --lc-ctype
  * determines which character is a space, digit etc.
  * collation: determines how string are sorted and ordered. (cannot be changed after db creation)
    * indexes are sorted lists. order is determined by collation for string data type
    * affects order by clauses based on collation in the database.
    * US-english. Or use C or posix locale. C locale is very fast.

* standard data dir: /var/lib/pgsql/11/data

To start:

```bash
$ pg_ctl -D /home/mokha/development/2020-04-pg-training/db/data -l logfile start
```

* 1 server process for each client connection.
  * good isolation

* `psql` is a command line client for connecting to the server.
