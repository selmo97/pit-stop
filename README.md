# Pit Stop

Welcome to the Pit Stop, a road-side no-nonsense full-service auto repair shop that's been
in the business for more than a century. They've kept pristine paper records of all the vehicles
that they've serviced, and you've been hired to do some data analysis as they digitize
their books.

## Initialize and connect to the database

Included in this repo is a `pit_stop.sql` file which will initialize a database on your
own computer with a sample set of vehicle records.

1. Run `psql -f pit_stop.sql`. This tells PostgreSQL to run the file, which will create
   the database and fill it with data. You should see a series of messages ending with
   `ALTER TABLE`.
2. Run `psql` to launch the interactive PostgreSQL terminal.
3. Run `\l` to see a list of databases on your computer. One of them should be named
   `pit_stop`.
4. Run `\c pit_stop` to connect to that database. You should receive a confirmation
   message.
5. Run `\conninfo` to get more information about your connection to the database.

## Examine the database

Now that you're connected to the `pit_stop` database, let's see what data it contains!

6. Run `\d` to list all of the tables in the connected database. You should see a single
   table named `vehicles`.
7. Run `\d vehicles` to get more details about the `vehicles` table. How many columns does
   `vehicles` have? 7 columns
8. What is the type of the `color` column?
   text

9. What is the type of the `date` column?
   timestamp(3) without time zone

10. Can any of the columns have a null value? no
11. Do any of the columns have a default value? no

## Query the database with SQL

In order to communicate with the database, we have to write **Structured Query Language (SQL)**.
A SQL **query**, or **statement**, is made up of several **clauses**.

For example, this SQL query contains the clauses `SELECT id` and `FROM vehicles`.

```sql
SELECT id FROM vehicles;
```

> [!NOTE]
>
> SQL is actually case-insensitive! `select id from vehicles;` is also a completely valid
> SQL statement. Capitalizing clauses is a common _stylistic_ convention that can help
> readers quickly identify and distinguish keywords.

> [!WARNING]
>
> Be mindful of the semicolon at the end of the SQL **statement**!
> Your queries will not work if you forget the semicolon.

12. Run the SQL query above. What is the output? You can press `q` to exit the list view.
   all rows only from the column id

13. What is the output of `SELECT id, model FROM vehicles;`? 
   the output is a list of all rows from the vehicles table showing only the id and model columns for each vehicle.

14. Write the SQL query to get the color, fuel, and manufacturer of every vehicle.
SELECT color, fuel, manufacturer FROM vehicle;

15. What is the output of `SELECT * FROM vehicles LIMIT 10;`? 
The output is a list of only 10 first rows from the vehicles table showing all columns for each vehicle.

16. Write the SQL query to:
    1. Get the id, type, and date of the first 20 vehicles.
    SELECT id, type, date FROM vehicles LIMIT 20;

    2. Get all columns of the first 5 vehicles.
    SELECT * FROM vehicles LIMIT 5;

    3. Get the date, model, and color of all vehicles.
    SELECT  date, model, color FROM vehicles;

    4. Get the id, color, and fuel of the first 50 vehicles.
    SELECT id, color, fuel FROM vehicles LIMIT 50;
    5. Get all columns of all vehicles.
    SELECT * FROM vehicles;

## Filter the results

Most of the time, we don't actually want all the **records** from a table. Instead, we
want to filter out the records based on some criteria. This can be accomplished with the
`WHERE` clause.

```sql
SELECT * FROM vehicles WHERE color = 'lime';
```

> [!IMPORTANT]
>
> In SQL, there is a difference between single quotes `'` and double quotes`"`!
> Single quotes are used around strings, such as `'lime'` or `'Electric'`,
> while double quotes are used around **identifiers**, such as the name of a
> table or a column.

17. What is the output of the SQL query above?
total of 10 rows showing  all columns for each vehicle thats value of color was 'lime'

18. What is the output of `SELECT * FROM vehicles WHERE id <= 'D' AND fuel = 'Hybrid';`?
total of 7 rows showing all columns for each vehicle whos id string value is alphabetically before or equal to 'D' AND fuel value is equal to the string 'Hybrid'

19. What is the output of `SELECT * FROM vehicles WHERE date BETWEEN '2020-01-01' AND '2022-01-01'`?
total of 8 rows showing all columns for each vehicle thats value of date column value is between specific date in question

20. What is the output of `SELECT * FROM vehicles WHERE type LIKE 'Co%'`?
56 rows of all columns for each vehicle thats value of type column starts with the string 'Co'

21. What is the output of `SELECT * FROM vehicles WHERE type LIKE 'co%'`?
0 rows (because string is case sensitive)

22. What is the output of `SELECT * FROM vehicles WHERE type ILIKE 'co%'`?
total of 56 rows of all columns for each vehicle thats type string value starts with 'co' case in-sensitive (the ILIKE is case insensitive in pattern matching)
23. What is the difference between `LIKE` and `ILIKE`?
LIKE = case sensitive 
ILIKE = case insensitive

24. `%` is a **wildcard** character used with `LIKE`. What does it do?
represents/matches zero or more characters

25. What is another wildcard character that can be used with `LIKE`?
underscore: _

26. Write the SQL query to:
    1. Select all columns from vehicles that are hatchbacks.
    SELECT * FROM vehicles WHERE type = 'Hatchback';

    2. Select the id, color, and model of vehicles that are green.
    SELECT id,color,model FROM vehicles WHERE color = 'green';

    3. Select the manufacturer and type of all vehicles that use either electric or diesel
       fuel. (_Hint:_ use `OR`)
       SELECT manufacturer, type FROM vehicles WHERE fuel = 'Electric' OR fuel = 'Diesel';

    4. Select all columns of vehicles that visited the pit stop before the year 1990.
    SELECT * FROM vehicles WHERE date < '1990-01-01';

    5. Select all columns of vehicles that visited the pit stop in the year 2038.
    SELECT * FROM vehicles WHERE date >= '2038-01-01' AND date < '2039-01-01';

    6. Select the color and type of all vehicles whose IDs start with the letter "P".
    SELECT color, type FROM vehicles WHERE id LIKE 'P%';

    7. Select the id, manufacturer, color, and type of all vehicles whose IDs end with the
       letter "K".
       SELECT id, manufacturer, color, type FROM vehicles WHERE id LIKE '%K';

    8. Select all columns of vehicles whose IDs contain the number "11".
    SELECT * FROM vehicles WHERE id LIKE '%11%';
