1. The first thing you need to do is start the terminal. Do that by clicking the "hamburger" menu at the top left of the screen, going to the "terminal" section, and clicking "new terminal". Once you open a new one, type `echo hello terminal` into the terminal and press enter.
2. You are going to build a bike rental shop. It will have a database, and a bash script to interact with the database. Use the terminal to connect to PostgreSQL by entering `psql --username=freecodecamp --dbname=postgres`.
3. List the databases with `\l` to see what databases are here.
```txt
List of databases
+-----------+----------+----------+---------+---------+-----------------------+
|   Name    |  Owner   | Encoding | Collate |  Ctype  |   Access privileges   |
+-----------+----------+----------+---------+---------+-----------------------+
| postgres  | postgres | UTF8     | C.UTF-8 | C.UTF-8 |                       |
| template0 | postgres | UTF8     | C.UTF-8 | C.UTF-8 | =c/postgres          +|
|           |          |          |         |         | postgres=CTc/postgres |
| template1 | postgres | UTF8     | C.UTF-8 | C.UTF-8 | =c/postgres          +|
|           |          |          |         |         | postgres=CTc/postgres |
+-----------+----------+----------+---------+---------+-----------------------+
(3 rows)
```
4. You need your own database for the bike shop. Create a new database named `bikes`.

**Solution**: Type `CREATE DATABASE bikes;` into the psql prompt and press enter

5. List databases again to make sure your database got created.
6. There it is. Connect to it so you can start building the structure of your bike shop database.

*How to solve?*

- Use the connect shortcut command
- Add the database name to the command
- It's the `\c` command
- Here's an example: `\c` database_name
- Try entering `\c bikes` into the psql prompt
- Type `psql --username=freecodecamp --dbname=bikes` into the terminal to log in to psql if you aren't logged in first

7. Your database needs three tables. One for your bike inventory, one for your customers, and one for the bikes that are rented out. Create a table named bikes in your database for the inventory.

**Solution**: `CREATE TABLE bikes();`

8. Display the tables to make sure your table got created.
```txt
 List of relations
+--------+-------+-------+--------------+
| Schema | Name  | Type  |    Owner     |
+--------+-------+-------+--------------+
| public | bikes | table | freecodecamp |
+--------+-------+-------+--------------+
(1 row)
```
9. The table will have a few columns for bike information. First, is a unique ID column. Add a column to the `bikes` table named `bike_id`. Give it a type of `SERIAL` and make it a `PRIMARY KEY`.

*How to solve?*

- Use the `ALTER TABLE`, `ADD COLUMN`, `SERIAL`, and `PRIMARY KEY` keywords
- Here's an example: `ALTER TABLE table_name ADD COLUMN column_name TYPE CONSTRAINTS;`
- Try entering `ALTER TABLE bikes ADD COLUMN bike_id SERIAL PRIMARY KEY;` in the psql prompt
- Type psql --username=freecodecamp --dbname=bikes into the terminal to log in to psql if you aren't logged in first

10. Use the display command to view the details of the bikes table. Type: `\d bikes`

Output:
```txt
Table "public.bikes"
+---------+---------+-----------+----------+----------------------------------------+
| Column  |  Type   | Collation | Nullable |                Default                 |
+---------+---------+-----------+----------+----------------------------------------+
| bike_id | integer |           | not null | nextval('bikes_bike_id_seq'::regclass) |
+---------+---------+-----------+----------+----------------------------------------+
Indexes:
    "bikes_pkey" PRIMARY KEY, btree (bike_id)
```
11. The first column is set. Add a column named `type` for the type of bike. Make it a `VARCHAR(50`) and give it a constraint of `NOT NULL`.

*How to solve?*

- Use the `ALTER TABLE`, `ADD COLUMN`, `VARCHAR(50)`, and `PRIMARY KEY` keywords
- Here's an example: `ALTER TABLE table_name ADD COLUMN column_name TYPE CONSTRAINTS;`
- Try entering `ALTER TABLE bikes ADD COLUMN type VARCHAR(50) NOT NULL;` in the psql prompt
- Type `psql --username=freecodecamp --dbname=bikes` into the terminal to log in to psql if you aren't logged in first

12. Display the details of the bikes table again.
```txt
Table "public.bikes"
+---------+-----------------------+-----------+----------+----------------------------------------+
| Column  |         Type          | Collation | Nullable |                Default                 |
+---------+-----------------------+-----------+----------+----------------------------------------+
| bike_id | integer               |           | not null | nextval('bikes_bike_id_seq'::regclass) |
| type    | character varying(50) |           | not null |                                        |
+---------+-----------------------+-----------+----------+----------------------------------------+
Indexes:
    "bikes_pkey" PRIMARY KEY, btree (bike_id)
```
13. The first two columns look good. Add a column named `size` to the `bikes` table that is an `INT` and has the `NOT NULL` constraint. This will be for the size of each bike.

*How to solve?*
- Use the `ALTER TABLE`, `ADD COLUMN`, `INT`, and `NOT NULL` keywords
- Here's an example: `ALTER TABLE table_name ADD COLUMN column_name TYPE CONSTRAINTS;`
- Try entering `ALTER TABLE bikes ADD COLUMN size INT NOT NULL;` in the psql prompt
- Type `psql --username=freecodecamp --dbname=bikes` into the terminal to log in to psql if you aren't logged in

14. Add another column to the table named `available`. Make it a `boolean` and has a constraint of `NOT NULL`. Also give it a default value of `TRUE`. This will be set to `false` when someone rents out a bike.

*How to solve?*

- Use the `ALTER TABLE`, `ADD COLUMN`, `BOOLEAN`, `NOT NULL` and `DEFAULT TRUE` keywords
- Here's an example: `ALTER TABLE table_name ADD COLUMN column_name TYPE CONSTRAINTS DEFAULT;`
- Try entering `ALTER TABLE bikes ADD COLUMN available BOOLEAN NOT NULL DEFAULT TRUE;` in the psql prompt
- Type `psql --username=freecodecamp --dbname=bikes` into the terminal to log in to psql if you aren't logged in

15. Display the details of the `bikes` table again so you can make sure it's how you want it.
```txt
Table "public.bikes"
+-----------+-----------------------+-----------+----------+----------------------------------------+
|  Column   |         Type          | Collation | Nullable |                Default                 |
+-----------+-----------------------+-----------+----------+----------------------------------------+
| bike_id   | integer               |           | not null | nextval('bikes_bike_id_seq'::regclass) |
| type      | character varying(50) |           | not null |                                        |
| size      | integer               |           | not null |                                        |
| available | boolean               |           | not null | true                                   |
+-----------+-----------------------+-----------+----------+----------------------------------------+
Indexes:
    "bikes_pkey" PRIMARY KEY, btree (bike_id)
```
16. That table is done for now. Create another table named `customers`. It will store a name and phone number for each customer that rents a bike.

**Solution**: Try entering `CREATE TABLE customers();

17. Add a `customer_id` column to your new table that is a type of `SERIAL` and make it a `PRIMARY KEY`.

*How to solve?*

- Use the `ALTER TABLE`, `ADD COLUMN`, `SERIAL`, and `PRIMARY KEY` keywords
- Here's an example: `ALTER TABLE table_name ADD COLUMN column_name TYPE CONSTRAINTS;`
- Try entering `ALTER TABLE customers ADD COLUMN customer_id SERIAL PRIMARY KEY;` in the psql prompt
- Type `psql --username=freecodecamp --dbname=bikes` into the terminal to log in to psql if you aren't logged in first
18. Display the details of the customers table so you can make sure your new column is there.

Type: `\d customers`

Output:
```txt
Table "public.customers"
+-------------+---------+-----------+----------+------------------------------------------------+
|   Column    |  Type   | Collation | Nullable |                    Default                     |
+-------------+---------+-----------+----------+------------------------------------------------+
| customer_id | integer |           | not null | nextval('customers_customer_id_seq'::regclass) |
+-------------+---------+-----------+----------+------------------------------------------------+
Indexes:
    "customers_pkey" PRIMARY KEY, btree (customer_id)
```
19. There it is. Add a column named `phone` for customers phone numbers. Make it a varying character that has a maximum length of `15` characters. Also make sure it can't be null, and that it has to be unique.

*How to solve?*

- Use the `ALTER TABLE`, `ADD COLUMN`, `VARCHAR()`, `NOT NULL`, and `UNIQUE` keywords
- Here's an example: `ALTER TABLE table_name ADD COLUMN column_name TYPE CONSTRAINTS;`
- Try entering `ALTER TABLE customers ADD COLUMN phone VARCHAR(15) NOT NULL UNIQUE;` in the psql prompt
- Type `psql --username=freecodecamp --dbname=bikes` into the terminal to log in to psql if you aren't logged in first

20. Add the last column. Call it `name` and make it a `VARCHAR(40)` that can't be null.

**Solution**: Try entering `ALTER TABLE customers ADD COLUMN name VARCHAR(40) NOT NULL;` in the psql prompt

21. Display the details of the `customers` table.

Output:
```txt
Table "public.customers"
+-------------+-----------------------+-----------+----------+------------------------------------------------+
|   Column    |         Type          | Collation | Nullable |                    Default                     |
+-------------+-----------------------+-----------+----------+------------------------------------------------+
| customer_id | integer               |           | not null | nextval('customers_customer_id_seq'::regclass) |
| phone       | character varying(15) |           | not null |                                                |
| name        | character varying(40) |           | not null |                                                |
+-------------+-----------------------+-----------+----------+------------------------------------------------+
Indexes:
    "customers_pkey" PRIMARY KEY, btree (customer_id)
    "customers_phone_key" UNIQUE CONSTRAINT, btree (phone)
```
22. That table is finished. Lastly, you need a table to store which bikes are rented and who has rented them. Create a new table named `rentals`.

**Solution**: Try entering `CREATE TABLE rentals();` in the psql prompt

23. Add a rental_id column to your new table. Make it automatically increment with SERIAL and make it the primary key for this table.

*How to solve?*
- The other two properties are `SERIAL` and `PRIMARY KEY`
- Use the `ALTER TABLE`, `ADD COLUMN`, `SERIAL`, and `PRIMARY KEY` keywords
- Here's an example: `ALTER TABLE table_name ADD COLUMN column_name TYPE CONSTRAINTS;`
- Try entering `ALTER TABLE rentals ADD COLUMN rental_id SERIAL PRIMARY KEY;` in the psql prompt
- Type `psql --username=freecodecamp --dbname=bikes` into the terminal to log in to psql if you aren't logged in first
24. Display the details of the rentals table.

**Solution**: Type `\d rentals`

Output:
```txt
Table "public.rentals"
+-----------+---------+-----------+----------+--------------------------------------------+
|  Column   |  Type   | Collation | Nullable |                  Default                   |
+-----------+---------+-----------+----------+--------------------------------------------+
| rental_id | integer |           | not null | nextval('rentals_rental_id_seq'::regclass) |
+-----------+---------+-----------+----------+--------------------------------------------+
Indexes:
    "rentals_pkey" PRIMARY KEY, btree (rental_id)
```
25. Next, you need a column for the customer who is renting a bike. Add column named customer_id. This will have an id of a customer from the customers table. Make the column an `INT` and `NOT NULL` to start.

*How to solve?*

- Add the column to the rentals table
- Use the `ALTER TABLE`, `ADD COLUMN`, `INT`, and `NOT NULL` keywords
- Here's an example: `ALTER TABLE table_name ADD COLUMN column_name TYPE CONSTRAINTS;`
- Try entering `ALTER TABLE rentals ADD COLUMN customer_id INT NOT NULL;` in the psql prompt
- Type `psql --username=freecodecamp --dbname=bikes` into the terminal to log in to psql if you aren't logged in first

26. Make the column you just added a foreign key that references the `customer_id` column from the `customers` table. Here's an example of how you can do that:
```sql
ALTER TABLE table_name ADD FOREIGN KEY(column_name) REFERENCES referenced_table(referenced_column);
```

*How to solve?*

- Without the keywords, it looks like tihs: `rentals customer_id customers(customer_id)`
- Try entering `ALTER TABLE rentals ADD FOREIGN KEY(customer_id) REFERENCES customers(customer_id);` in the psql prompt
- Type psql --username=freecodecamp --dbname=bikes into the terminal to log in to psql if you aren't logged in first

27. Display the details of the rentals table to make sure your key is set.
```txt
Table "public.rentals"
+-------------+---------+-----------+----------+--------------------------------------------+
|   Column    |  Type   | Collation | Nullable |                  Default                   |
+-------------+---------+-----------+----------+--------------------------------------------+
| rental_id   | integer |           | not null | nextval('rentals_rental_id_seq'::regclass) |
| customer_id | integer |           | not null |                                            |
+-------------+---------+-----------+----------+--------------------------------------------+
Indexes:
    "rentals_pkey" PRIMARY KEY, btree (rental_id)
Foreign-key constraints:
    "rentals_customer_id_fkey" FOREIGN KEY (customer_id) REFERENCES customers(customer_id)
```
28. That foreign key is set. You need another column so you know what bike a customer is renting. Add a column named `bike_id` and make it an `INT` and `NOT NULL`.

*How to solve?*

- Add the column to the `rentals` table
- Use the `ALTER TABLE`, `ADD COLUMN`, `INT`, and `NOT NULL` keywords
- Here's an example: `ALTER TABLE table_name ADD COLUMN column_name TYPE CONSTRAINTS;`
- Try entering `ALTER TABLE rentals ADD COLUMN bike_id INT NOT NULL;` in the psql prompt
- Type `psql --username=freecodecamp --dbname=bikes` into the terminal to log in to psql if you aren't logged in first
29. Make that column a foreign key that references the `bike_id` column from the `bikes` table so you know what bike the id is for.

*How to solve?*

- Here's the example again: `ALTER TABLE table_name ADD FOREIGN KEY(column_name) REFERENCES referenced_table(referenced_column);`
- Without the keywords, it looks like tihs: `rentals bike_id bikes(bike_id)`
- Try entering `ALTER TABLE rentals ADD FOREIGN KEY(bike_id) REFERENCES bikes(bike_id);` in the psql prompt
- Type `psql --username=freecodecamp --dbname=bikes` into the terminal to log in to psql if you aren't logged in first
30. Display the details of the `rentals` table so you can make sure the key is correct.

Output:
```txt
Table "public.rentals"
+-------------+---------+-----------+----------+--------------------------------------------+
|   Column    |  Type   | Collation | Nullable |                  Default                   |
+-------------+---------+-----------+----------+--------------------------------------------+
| rental_id   | integer |           | not null | nextval('rentals_rental_id_seq'::regclass) |
| customer_id | integer |           | not null |                                            |
| bike_id     | integer |           | not null |                                            |
+-------------+---------+-----------+----------+--------------------------------------------+
Indexes:
    "rentals_pkey" PRIMARY KEY, btree (rental_id)
Foreign-key constraints:
    "rentals_bike_id_fkey" FOREIGN KEY (bike_id) REFERENCES bikes(bike_id)
    "rentals_customer_id_fkey" FOREIGN KEY (customer_id) REFERENCES customers(customer_id)
```
31. Moving along. You want to know when a customer rents a bike, and when it gets returned. Add a column to your `rentals` table named `date_rented` that's a type of `DATE`. Make sure the entry can't be null, and give it a default value of NOW().

*How to solve?*

- Add the column to the rentals table
- Use the `ALTER TABLE`, `ADD COLUMN`, `DATE`, `NOT NULL`, and `DEFAULT NOW()` keywords
- Here's an example: `ALTER TABLE table_name ADD COLUMN column_name TYPE CONSTRAINTS;`
- Try entering `ALTER TABLE rentals ADD COLUMN date_rented DATE NOT NULL DEFAULT NOW();` in the psql prompt
- Type `psql --username=freecodecamp --dbname=bikes` into the terminal to log in to psql if you aren't logged in first

32. Display the details of the `rentals` table again.
```txt
Table "public.rentals"
+-------------+---------+-----------+----------+--------------------------------------------+
|   Column    |  Type   | Collation | Nullable |                  Default                   |
+-------------+---------+-----------+----------+--------------------------------------------+
| rental_id   | integer |           | not null | nextval('rentals_rental_id_seq'::regclass) |
| customer_id | integer |           | not null |                                            |
| bike_id     | integer |           | not null |                                            |
| date_rented | date    |           | not null | now()                                      |
+-------------+---------+-----------+----------+--------------------------------------------+
Indexes:
    "rentals_pkey" PRIMARY KEY, btree (rental_id)
Foreign-key constraints:
    "rentals_bike_id_fkey" FOREIGN KEY (bike_id) REFERENCES bikes(bike_id)
    "rentals_customer_id_fkey" FOREIGN KEY (customer_id) REFERENCES customers(customer_id)
```
33. It looks good. Lastly, you need column for when a customer returns a bike. Add a column named `date_returned` that's a type of `DATE`.

*How to solve?*

- Use the `ALTER TABLE`, `ADD COLUMN`, `DATE` keywords
- Add the column to the `rentals` table
- Here's an example: `ALTER TABLE table_name ADD COLUMN column_name TYPE;`
- Try entering `ALTER TABLE rentals ADD COLUMN date_returned DATE;` in the psql prompt
- Type `psql --username=freecodecamp --dbname=bikes` into the terminal to log in to psql if you aren't logged in first

34. View the details of the table again.
```txt
Table "public.rentals"
+---------------+---------+-----------+----------+--------------------------------------------+
|    Column     |  Type   | Collation | Nullable |                  Default                   |
+---------------+---------+-----------+----------+--------------------------------------------+
| rental_id     | integer |           | not null | nextval('rentals_rental_id_seq'::regclass) |
| customer_id   | integer |           | not null |                                            |
| bike_id       | integer |           | not null |                                            |
| date_rented   | date    |           | not null | now()                                      |
| date_returned | date    |           |          |                                            |
+---------------+---------+-----------+----------+--------------------------------------------+
Indexes:
    "rentals_pkey" PRIMARY KEY, btree (rental_id)
Foreign-key constraints:
    "rentals_bike_id_fkey" FOREIGN KEY (bike_id) REFERENCES bikes(bike_id)
    "rentals_customer_id_fkey" FOREIGN KEY (customer_id) REFERENCES customers(customer_id)
```
35. The tables are all finished. Display all the tables so you can see what you ended up with.
```txt
List of relations
+--------+---------------------------+----------+--------------+
| Schema |           Name            |   Type   |    Owner     |
+--------+---------------------------+----------+--------------+
| public | bikes                     | table    | freecodecamp |
| public | bikes_bike_id_seq         | sequence | freecodecamp |
| public | customers                 | table    | freecodecamp |
| public | customers_customer_id_seq | sequence | freecodecamp |
| public | rentals                   | table    | freecodecamp |
| public | rentals_rental_id_seq     | sequence | freecodecamp |
+--------+---------------------------+----------+--------------+
(6 rows)
```
36. You have nine bikes in your inventory. Add the first one to your `bikes` table. It has a `type` of `Mountain` and a `size` of `27`. Make sure to put your `VARCHAR` values in single quotes. The `bike_id` and `available` columns should be filled in automatically, so you don't need to worry about those.

*How to solve?*

- Use the `INSERT INTO` and `VALUES` keywords
- Here's an example: `INSERT INTO table_name(column_name, column_name) VALUES(value, value);`
- View the details of the bikes table with `\d bikes` to see what values it expects
- Try entering `INSERT INTO bikes(type, size) VALUES('Mountain', 27);` in the psql prompt
- Type `psql --username=freecodecamp --dbname=bikes` into the terminal to log in to psql if you aren't logged in first

37. View all the columns in your bikes table with SELECT.

*Solution*: `SELECT * FROM bikes;`

Output:
```txt
+---------+----------+------+-----------+
| bike_id |   type   | size | available |
+---------+----------+------+-----------+
|       1 | Mountain |   27 | t         |
+---------+----------+------+-----------+
(1 row)
```
38. Looks like it's all working, the `bike_id` and `available` columns were filled in automatically. Insert another bike. Give it a `type` of `Mountain` and a `size` of `28`.

*Solution*: `INSERT INTO bikes(type, size) VALUES('Mountain', 28);`

39. Add another `Mountain` bike to your inventory. Make it a `29` inch bike.

*Solution*: `INSERT INTO bikes(type, size) VALUES('Mountain', 29);`

40. Add a `27` inch `Road` bike to the table.

*Solution*: `INSERT INTO bikes(type, size) VALUES('Road', 27);`

41. Use `SELECT` to view all the data in the `bikes` table again.

*Solution*: `SELECT * FROM bikes;`

Output:
```txt
+---------+----------+------+-----------+
| bike_id |   type   | size | available |
+---------+----------+------+-----------+
|       1 | Mountain |   27 | t         |
|       2 | Mountain |   28 | t         |
|       3 | Mountain |   29 | t         |
|       4 | Road     |   27 | t         |
+---------+----------+------+-----------+
(4 rows)
```
42. Add the two bikes to your inventory, they are `28` and `29` inch `Road` bikes. Try to add them both with one command.

*How to solution?*

- Here's an example: `INSERT INTO table_name(column_name, column_name) VALUES(value, value), (value, value);`
- Make sure to put your `VARCHAR` values in single quotes
- Try entering `INSERT INTO bikes(type, size) VALUES('Road', 28), ('Road', 29);` in the psql prompt
- Type `psql --username=freecodecamp --dbname=bikes` into the terminal to log in to psql if you aren't logged in first

43. There's three more bikes. Add 19, 20, and 21 inch `BMX` bikes to your table. Try to add them with one command.

*How to solve?*

- Here's an example: `INSERT INTO table_name(column_name, column_name) VALUES(value, value), (value, value), (value, value);`
- Make sure to put your `VARCHAR` values in single quotes
- Try entering `INSERT INTO bikes(type, size) VALUES('BMX', 19), ('BMX', 20), ('BMX', 21);` in the psql prompt
- Type `psql --username=freecodecamp --dbname=bikes` into the terminal to log in to psql if you aren't logged in first

44. View all the data in your bikes table.
```txt
+---------+----------+------+-----------+
| bike_id |   type   | size | available |
+---------+----------+------+-----------+
|       1 | Mountain |   27 | t         |
|       2 | Mountain |   28 | t         |
|       3 | Mountain |   29 | t         |
|       4 | Road     |   27 | t         |
|       5 | Road     |   28 | t         |
|       6 | Road     |   29 | t         |
|       7 | BMX      |   19 | t         |
|       8 | BMX      |   20 | t         |
|       9 | BMX      |   21 | t         |
+---------+----------+------+-----------+
(9 rows)
```
45. Your current inventory is all added. For the rest of the project, I recommend leaving that terminal open and connected, and that you should "split" the terminal so you have a second one to use for bash commands. Do that by clicking the "hamburger" menu at the top left of the window, going to the "terminal" section, and clicking "split terminal". After you have opened it, use the `touch` command to create a file named `bike-shop.sh` in the project folder.
46. This file will be the program for your bike rental shop. Open the file and add a "shebang" at the top so it uses bash when it's executed. If you don't remember, it looks like this: `#!/bin/bash`.
47. In the file, use echo with the `-e` flag to print `~~~~~ Bike Rental Shop ~~~~~` with a new line at the beginning and end.

*How to solve?*

- The newline character is `\n`
- Use double quotes around the message so the new lines are printed
- Here's an example: `echo -e "\n<message_here>\n"`
- Add `echo -e "\n~~~~~ Bike Rental Shop ~~~~~\n"` to the bike-shop-sh file

48. Use the terminal (not the psql one) and the `chmod` command to make your file executable. Add the `+x` flag and `bike-shop.sh` to the command to do that.
49. Type `./bike-shop.sh` in the terminal to run your script.
50. In the script, create an empty function named `MAIN_MENU`. This will have a few options to enter when the script runs to rent or return a bike.

*How to solve?*

Here's an example:
```sh
FUNCTION_NAME() {

}
```

Add this to the bottom of the script:
```sh
MAIN_MENU() {

}
```
51. In your function, echo the text `How may I help you?` so that there's a greeting when you go to the menu.
```sh
MAIN_MENU() {
  echo "How may I help you?"
}
```
52. Call your `MAIN_MENU` at the bottom of the file so the function runs when you start the script.
53. Run the file in the terminal again so you can see what it is outputting.
```txt
~~~~~ Bike Rental Shop ~~~~~

How may I help you?
```
54. It's coming along. Add another `echo` command in the function below the other one. Make it output text that looks like this:
```sh

1. Rent a bike
2. Return a bike
3. Exit
```
Note that there's an empty line at the start.

*How to solve?*

- Use the `echo` command with the `-e` flag and line breaks (`\n`) to produce the suggested output
- Without the words, it looks like this: `echo -e "\n1. \n2. \n3. "`
- Run your script if you need to see if the output matches
- Add `echo -e "\n1. Rent a bike\n2. Return a bike\n3. Exit"` to your function

```sh
MAIN_MENU() {
  echo "How may I help you?"
  echo -e "\n1. Rent a bike\n2. Return a bike\n3. Exit"
}
```
55. Run the file to make sure it worked.
```txt
~~~~~ Bike Rental Shop ~~~~~

How may I help you?

1. Rent a bike
2. Return a bike
3. Exit
```
56. You have some options displaying. Next, you need to get input from whoever is using the program. Use the `read` command to read input into a variable called `MAIN_MENU_SELECTION` below the options.

*How to solve?*

- Here's an example: read <VARIABLE_NAME>
- Here's what the code looks like: read MAIN_MENU_SELECTION
- Add the code at the bottom of the MAIN_MENU function
- The MAIN_MENU function should look like this:
```sh
MAIN_MENU() {
  echo "How may I help you?"
  echo -e "\n1. Rent a bike\n2. Return a bike\n3. Exit"
  read MAIN_MENU_SELECTION
}
```
57. When an option gets entered, you need to take a user to one of those other menus. Add an empty `RENT_MENU` function below the `MAIN_MENU` function.

*How to solve?*

- Make sure the `RENT_MENU` function is below the MAIN_MENU function and above where you call `MAIN_MENU`
- Add this in the suggested area:
```sh
RENT_MENU() {

}
```
58. For the time being, just echo `Rent Menu` in the function so you can see if it's working.

*How to solve?*

- Don't use any flags with the command
- Add `echo "Rent Menu"` in the `RENT_MENU` function
```sh
RENT_MENU() {
  echo "Rent Menu"
}
```
59. Add an empty `RETURN_MENU` function below the `RENT_MENU` function for when a user enters the option to return a bike.

*How to solve?*
Add this in the suggested area:
```sh
RETURN_MENU() {

}
```
60. Use echo to print "Return Menu" in the function you just added. You will change these later.

**Solution**: Add echo "Return Menu" in the RETURN_MENU function
```sh
RETURN_MENU() {
  echo "Return Menu"
}
```
61. Add an empty `EXIT` function below the `RETURN_MENU` function for when a user wants to exit the program.

*How to solve?*

Add this in the suggested area:
```sh
EXIT() {

}
```
62. This one probably doesn't need a placeholder message. In the `EXIT` function, use `echo` to print `Thank you for stopping in.` with a new line at the beginning and end of the message.

*How to solve?*

- The newline character is `\n`
- Use double quotes around the message so the new lines are printed
- Here's an example: `echo -e "\n<message_here>\n"`
- Add `echo -e "\nThank you for stopping in.\n"` to the EXIT function

63. When a user enters an option at the main menu, you want to take them to the appropriate sub-menu. You can use a case statement for this. Here's an example:
```sh
case EXPRESSION in
  PATTERN) STATEMENTS ;;
  PATTERN) STATEMENTS ;;
  PATTERN) STATEMENTS ;;
  *) STATEMENTS ;;
esac
```
The expression you want is the `$MAIN_MENU_SELECTION` variable. You are expecting it to be a 1, 2, or 3 for your various menus. Add a case statement that takes users to their corresponding menus. The `*` is for when anything else is entered. Take users to the MAIN_MENU when the variable isn't a 1, 2, or 3.

*How to solve?*

- Add the `case` statement in the `MAIN_MENU` function below the read `MAIN_MENU_SELECTION` line
- Here's how it starts:
```sh
case $MAIN_MENU_SELECTION in
  1) RENT_MENU ;;
```
- Add this case statement below the;
```sh
case $MAIN_MENU_SELECTION in
  1) RENT_MENU ;;
  2) RETURN_MENU ;;
  3) EXIT ;;
  *) MAIN_MENU ;;
esac
```

Full source code:
```sh
MAIN_MENU() {
  echo "How may I help you?" 
  echo -e "\n1. Rent a bike\n2. Return a bike\n3. Exit"
  read MAIN_MENU_SELECTION
  case $MAIN_MENU_SELECTION in
    1) RENT_MENU ;;
    2) RETURN_MENU ;;
    3) EXIT ;;
    *) MAIN_MENU ;;
  esac
}
```
64. Run the script a few times and try out the different menus. Be sure to enter something other than one of the options to go to the main menu.

[![image.png](https://i.postimg.cc/bw8Gq1mF/image.png)](https://postimg.cc/2VcjwLR4)

65. Add an argument to where you call `MAIN_MENU` in the case statement. It should be `Please enter a valid option.`. The next step will adjust the function so the message is printed when a user enters an invalid option.

*How to solve?*

- Here's an example: FUNCTION_CALL "<argument_message>"
- Here's how the function call should look:
```sh
  *) MAIN_MENU "Please enter a valid option." ;;
```
- The whole case statement should look like this:
```sh
case $MAIN_MENU_SELECTION in
  1) RENT_MENU ;;
  2) RETURN_MENU ;;
  3) EXIT ;;
  *) MAIN_MENU "Please enter a valid option." ;;
esac
```
66. At the top of the MAIN_MENU function, add an if condition that checks if there's an argument (`$1`) passed to the function. If there is, print the message with a new line in front of it.

*How to solve?*

- Here's an example of an `if`:
```sh
if [[ <CONDITION> ]]
then
  <STATEMENTS>
fi
```
- The condition you want is `$1`
- Use `echo` with the `-e` flag and a new line character (`\n`) to print the argument with a new line at the beginning in the `<STATEMENTS>` area
- Here's an example of that part: `echo -e "\n<argument_here>"`
- The if statement should look like this:
```sh
if [[ $1 ]]
then
  echo -e "\n$1"
fi
```
- Make sure to put it at the top of the `MAIN_MENU` function

Full source code:
```sh
MAIN_MENU() {
  if [[ $1 ]]
  then
    echo -e "\n$1"
  fi
  echo "How may I help you?" 
  echo -e "\n1. Rent a bike\n2. Return a bike\n3. Exit"
  read MAIN_MENU_SELECTION
  case $MAIN_MENU_SELECTION in
    1) RENT_MENU ;;
    2) RETURN_MENU ;;
    3) EXIT ;;
    *) MAIN_MENU "Please enter a valid option.";;
  esac
}
```
67. Run the script and enter an invalid option to see the message. Exit the program when you are done.
68. Looks good. Delete the echo `"Rent Menu"` from the `RENT_MENU` function so you can start adding the ability to rent a bike from the database.
```sh
RENT_MENU() {
  
}
```
69. In the RENT_MENU function, add three single line comments; `get available bikes`, `if no bikes available`, and `send to main menu`, in that order.

*How to solve?*

- Here's an example of a single line comment: # <comment here>
- The RENT_MENU function should look like this:
```sh
RENT_MENU() {
  # get available bikes

  # if no bikes available

  # send to main menu

}
```
70. To get the bikes available, you need to query the database from your script. Below the "shebang", add a PSQL variable that looks like this: PSQL="psql -X --username=freecodecamp --dbname=bikes --tuples-only -c". You will then be able to use it to query the database like this: $($PSQL "<query_here>").

**How to solution**: Add the suggested variable below the "shebang" and above where you print the Bike Rental Shop line:
```sh
#!/bin/bash
PSQL="psql -X --username=freecodecamp --dbname=bikes --tuples-only -c"
```
71. Below the get available bikes comment. Create an AVAILABLE_BIKES variable that gets the bike_id, type, and size columns from the bikes table for the bikes that are available. Order the results by their bike_id column. Here's an example: AVAILABLE_BIKES=$($PSQL "<query_here>")

*How to solve?*

- Use the SELECT, FROM, WHERE, and ORDER BY keywords in your query
- Get the three suggested columns in the same order they are listed; bike_id, type, size
- The condition you want is WHERE available = true
- Without the keywords, the query looks like this: bike_id, type, size bikes available = true bike_id
- The query should be SELECT bike_id, type, size FROM bikes WHERE available = true ORDER BY bike_id
- Add AVAILABLE_BIKES=$($PSQL "SELECT bike_id, type, size FROM bikes WHERE available = true ORDER BY bike_id") below the get available bikes comment
```sh
RENT_MENU() {
  # get available bikes
  AVAILABLE_BIKES=$($PSQL "SELECT bike_id, type, size FROM bikes WHERE available = true ORDER BY bike_id")
  # if no bikes available

  # send to main menu
}
```
72. Below the new variable, use echo to print it. Place it in double quotes so it prints any new lines.

**Solution::**

- Use the variable with $AVAILABLE_BIKES
- Add echo "$AVAILABLE_BIKES" to the suggested area
```sh
RENT_MENU() {
  # get available bikes
  AVAILABLE_BIKES=$($PSQL "SELECT bike_id, type, size FROM bikes WHERE available = true ORDER BY bike_id")
  echo "$AVAILABLE_BIKES"
  # if no bikes available

  # send to main menu
}
```
73. Run your script and go to the rent menu to see if the available bikes are being printed.

Output:
```txt
~~~~~ Bike Rental Shop ~~~~~

How may I help you?

1. Rent a bike
2. Return a bike
3. Exit
1
       1 | Mountain |   27
       2 | Mountain |   28
       3 | Mountain |   29
       4 | Road     |   27
       5 | Road     |   28
       6 | Road     |   29
       7 | BMX      |   19
       8 | BMX      |   20
       9 | BMX      |   21
```
74. Awesome. In the psql prompt, set the available column to false for all the bikes so you can see what it prints when there's no bikes available.

*How to solve?*

- Use the UPDATE, SET, and WHERE keywords
- Here's an example: `UPDATE <table> SET <column> = <value> WHERE <condition>`
- You want to set available to false for columns that are true
- After the SET can look like this: `available = false WHERE available = true`
- Try entering `UPDATE bikes SET available = false WHERE available = true;` in the psql prompt
- Type `psql --username=freecodecamp --dbname=bikes` into the terminal to log in to psql if you aren't logged in. I recommend "splitting" the terminal so you can have one for bash commands and one for psql commands. You can do that by clicking the "hamburger" menu at the top left of the window, going to the "terminal" section, and clicking "split terminal".

75. Run your script and go to the rent menu to see the output.

As you can see, there's no rent bike.

76. So if there's no bike available, the variable will be empty. In the script, below the `if no bikes available` comment, add an if condition that checks if the variable is empty. Use `-z` to check if it's empty. Place the `send to main menu` comment in its `STATEMENTS` area.

*How to solve?*

- Use -z <VARIABLE> to see if a variable is empty
- Here's an example:
```sh
if [[ -z <VARIABLE> ]]
then
  <STATEMENTS>
fi
```
- The if condition should look like this:
```sh
if [[ -z $AVAILABLE_BIKES ]]
then
  # send to main menu
fi
```
77. Below the comment in the if you just added. Send users to the main menu and give them the message, `Sorry, we don't have any bikes available right now.`

*How to solve?*

- Here's an example MAIN MENU "<message_here>"
- Make sure it's in the if condition below the send to main menu comment
- The function call should look like this: MAIN_MENU "Sorry, we don't have any bikes available right now."
- The if condition should look like this:
```sh
if [[ -z $AVAILABLE_BIKES ]]
then
  # send to main menu
  MAIN_MENU "Sorry, we don't have any bikes available right now."
fi
```
78. Run the script and go to the rent menu to see the message. When you are done, exit the program.

Output:
```txt
~~~~~ Bike Rental Shop ~~~~~

How may I help you?

1. Rent a bike
2. Return a bike
3. Exit
1


Sorry, we don't have any bikes available right now.
How may I help you?
```
79. If no bikes are available, you will get that message. Add an `else` to the `if` condition for when there is bikes available. In it, add four single line comments; `display available bikes`, `ask for bike to rent`, `if input is not a number`, and `send to main menu`.

*How to solve?*

- Here's an example of a single line comment: `# <comment_here>
- Make sure the comments are in the same order listed
- An `if/else` statement looks like this:
```sh
if [[ <CONDITION> ]]
then
  <STATEMENTS>
else
  <STATEMENTS>
fi
```
- The `else` should look like this:
```sh
else
  # display available bikes

  # ask for bike to rent

  # if input is not a number

  # send to main menu

```
Full source code:
```sh
RENT_MENU() {
  # get available bikes
  AVAILABLE_BIKES=$($PSQL "SELECT bike_id, type, size FROM bikes WHERE available = true ORDER BY bike_id")
  echo "$AVAILABLE_BIKES"
  
  # if no bikes available

  if [[ -z $AVAILABLE_BIKES ]]
  then
    # send to main menu
    MAIN_MENU "Sorry, we don't have any bikes available right now."
  else
    # display available bikes

    # ask for bike to rent

    # if input is not a number

    # send to main menu
  fi
}
```
80. Below the `display available bikes` comment you just added, use echo to print `Here are the bikes we have available:` with a new line in front of the message

*How to solve?*

- Use echo with the -e flag and the new line character (\n) to print the suggested message
- Use double quotes around the message
- Here's an example: `echo -e "\n<message_here>"`
- Add `echo -e "\nHere are the bikes we have available:"` below the suggested comment

81. Move the `echo` command that prints all the available bikes below the message you just added.

**Solution**: It's the `echo $AVAILABLE_BIKES` command. It should be below the `Here are the bikes we have available:` message. You should only print the bikes available in that one spot. Place the `echo "$AVAILABLE_BIKES"` line in the suggested spot

Here is my source code:
```sh
RENT_MENU() {
  # get available bikes
  AVAILABLE_BIKES=$($PSQL "SELECT bike_id, type, size FROM bikes WHERE available = true ORDER BY bike_id")

  # if no bikes available
  if [[ -z $AVAILABLE_BIKES ]]
  then
    # send to main menu
    MAIN_MENU "Sorry, we don't have any bikes available right now."
  else
    # display available bikes
    echo -e "\nHere are the bikes we have available:"
    echo "$AVAILABLE_BIKES"

    # ask for bike to rent

    # if input is not a number

    # send to main menu

  fi
}
```
82. In the psql prompt, set all the bikes, except for the `BMX` bikes, back to true so you can see a list of bikes to rent.

*How to solve?*

- Use the `UPDATE`, `SET`, and `WHERE` keywords
- Here's an example: `UPDATE <table> SET <column> = <value> WHERE <condition>`
- You want to set `available` to `true` for columns that don't have a `type` of `BMX`
- You can use the `!=` operator to check for columns not equal to a value
- After the `SET` can look like this: `available = true WHERE type != 'BMX'`
- Try entering `UPDATE bikes SET available = true WHERE type != 'BMX';` in the psql prompt
83. Run the script and go to the rent menu to see the list of bikes available.

Output:
```txt
How may I help you?

1. Rent a bike
2. Return a bike
3. Exit
1

Here are the bikes we have available:
       1 | Mountain |   27
       2 | Mountain |   28
       3 | Mountain |   29
       4 | Road     |   27
       5 | Road     |   28
       6 | Road     |   29
```
84. Instead of directly printing the list, `pipe` the output into a `while` loop that reads each line. Here's how that looks:
```sh
echo "$AVAILABLE_BIKES" | while read <VAR_1> <VAR_2> <VAR_3> <VAR_4> <VAR_5>
do
  <STATEMENTS>
done
```
It will read the first line of your `AVAILABLE_BIKES` variable into the five variables. Each variable being the next word in the line. Read each line into variables, `BIKE_ID BAR TYPE BAR SIZE`. In the `<STATEMENTS>` area, use echo to print the `BIKE_ID`, `TYPE`, and `SIZE` variables, in that order.

*How to solve?*

- The first line should be echo "$AVAILABLE_BIKES" | while read BIKE_ID BAR TYPE BAR SIZE
- The <STATEMENTS> area looks like this: echo "$BIKE_ID $TYPE $SIZE"
- Here's how it should look:
```sh
echo "$AVAILABLE_BIKES" | while read BIKE_ID BAR TYPE BAR SIZE
do
  echo "$BIKE_ID $TYPE $SIZE"
done
```
85. Run the script and go to the rent menu again to see if it's working.
Output:
```txt
~~~~~ Bike Rental Shop ~~~~~

How may I help you?

1. Rent a bike
2. Return a bike
3. Exit
1

Here are the bikes we have available:
1 Mountain 27
2 Mountain 28
3 Mountain 29
4 Road 27
5 Road 28
6 Road 29
```
86. It's working! Adjust the echo command that prints the bike info so that the first line printed would look like this: `1) 27" Mountain Bike`. The rest would look the same, but with their bike info. Make sure to escape any characters you need to.

*How to solve?*

- Be sure to use double quotes and escape the `"` after `SIZE`
- Run your script and check the output if you want to see if it matches the suggestion
- Escape a `"` with `\"`
- Here's an example: `echo "<bike_id>) <size>" <type> Bike"`
- Make the suggested line look like this: `echo "$BIKE_ID) $SIZE\" $TYPE Bike"`
- The whole loop should look like this:
```sh
echo "$AVAILABLE_BIKES" | while read BIKE_ID BAR TYPE BAR SIZE
do
  echo "$BIKE_ID) $SIZE\" $TYPE Bike"
done
```
87. Run the script and go to the rent menu again to see what it looks like now.

Output:
```txt
How may I help you?

1. Rent a bike
2. Return a bike
3. Exit
1

Here are the bikes we have available:
1) 27" Mountain Bike
2) 28" Mountain Bike
3) 29" Mountain Bike
4) 27" Road Bike
5) 28" Road Bike
6) 29" Road Bike
```
88. That's better. Below the `ask for bike to rent` comment, print `Which one would you like to rent?` with a new line in front of it.

**Solution:** Add `echo -e "\nWhich one would you like to rent?"` below the suggested comment

89. Just below that, add a command to `read` input into a variable named `BIKE_ID_TO_RENT`.

*How to solve?*

Add this to the suggested area: read BIKE_ID_TO_RENT

90. Next, you want to find out how to test if the user input is a number. In the terminal, enter `[[ a =~ [0-9] ]]; echo $?` to see if a is a number. The conditional expression will run, and echo $? will print the exit code of it (the last command). It is return to 1.
91. It printed 1 for false. Meaning that a did not match the pattern [0-9], or a did not contain a number from 0-9. Enter the same commands, but check if a1 matches the pattern. **Solution:** enter `[[ a1 =~ [0-9] ]]; echo $?`. It is return to 0.
92. That printed 0 for true. a1 does contain a number from 0-9. Enter the same command, but change the pattern to `^[0-9]$`. The `^` signifies the start of the pattern, and `$` means the end. So the input will have to start, contain a number 0-9, and end. **Solution:** `[[ a1 =~ ^[0-9]$ ]]; echo $?`. It is return to 1.
93. 1 for false. a1 does not match the pattern. Using the same syntax, check if 1 matches the pattern. **Solution**: Enter `[[ 1 =~ ^[0-9]$ ]]; echo $?` in the terminal. It is return to 0.
94. 1 does match the pattern. It starts, contains a number, and ends. Check if 11 matches the same pattern. **Solution**: `[[ 11 =~ ^[0-9]$ ]]; echo $?`. It is return to 1.
95. That did not match because the pattern only allows a single number. Add a `+` after the `[0-9]` to allow any strings that start, contain one or more numbers, and end. **Solution**: `[[ 11 =~ ^[0-9]+$ ]]; echo $?`. It is return to 0.
96. So that pattern will match any positive integers. You want to check if the input is not a number. Add `!` in front of the comparison of the previous command to do that. **Solution:** `[[ ! 11 =~ ^[0-9]+$ ]]; echo $?`. It is return to 1.
97. Back in your script, below the `if input is not a number` comment, add an if condition that checks if the input is not a number using the method you just practiced. Add the `send to main menu` comment in the `then` area of the `if`.

*How to solve?*

- You want to check if the $BIKE_ID_TO_RENT variable is not a number
- You entered `[[ ! 11 =~ ^[0-9]+$ ]]; echo $?` in the terminal on the last step
- Here's an example:
```sh
if [[ <CONDITION> ]]
then
  # send to main menu
fi
```
- The condition you want is `[[ ! $BIKE_ID_TO_RENT =~ ^[0-9]+$ ]]`
- Add this in the suggestion area:
```sh
# if input is not a number
if [[ ! $BIKE_ID_TO_RENT =~ ^[0-9]+$ ]]
then
  # send to main menu
fi
```
98. If the `$BIKE_ID_TO_RENT` variable is not a number, add the code to send users to the main menu with the message, `That is not a valid bike number.`

*How to solve?*

- You want to call the `MAIN_MENU` function with the message as an argument
- Here's an example: `MAIN_MENU "<message_here>"`
- Add `MAIN_MENU "That is not a valid bike number."` below the send to main menu comment
```sh
# if input is not a number
if [[ ! $BIKE_ID_TO_RENT =~ ^[0-9]+$ ]]
then
  # send to main menu
  MAIN_MENU "That is not a valid bike number."
fi
```
99. Run the script, go to the rent menu, and enter something that isn't a number to make sure it is working. When you are done, exit the program.

Output:
```txt
~~~~~ Bike Rental Shop ~~~~~

How may I help you?

1. Rent a bike
2. Return a bike
3. Exit
1

Here are the bikes we have available:
1) 27" Mountain Bike
2) 28" Mountain Bike
3) 29" Mountain Bike
4) 27" Road Bike
5) 28" Road Bike
6) 29" Road Bike

Which one would you like to rent?
1
```
100. Add an `else` area for when the input is a number. Add these three single line comments in it; `get bike availability`, `if not available`, `send to main menu`.

*How to solve?*

- Here's an example of a single line comment: `# <comment_here>`
- Make sure the comments are in the same order listed
- An `if/else` statement looks like this:
```sh
if [[ <CONDITION> ]]
then
  <STATEMENTS>
else
  <STATEMENTS>
fi
```
- The `else` area should look like this:
```sh
# if input is not a number
if [[ ! $BIKE_ID_TO_RENT =~ ^[0-9]+$ ]]
then
  # send to main menu
  MAIN_MENU "That is not a valid bike number."
else
  # get bike availability

  # if not available

  # send to main menu
fi
```
101. Below the `get bike availability` comment you just added, create a `BIKE_AVAILABILITY` variable. Set it equal to a query that gets the `available` column from the `bikes` table for the input. Also, make sure to only get the row if it is available.

*How to solve?*

- Here's an example: `BIKE_AVAILABILITY=$($PSQL "<query_here>")`
- Use the `SELECT`, `FROM`, `WHERE`, and `AND` keywords
- Here's an example of the query: `SELECT <column> FROM <table> WHERE <condition1> AND <condition2>`
- You only want the `available` column for the bike with a `bike_id` equal to the `$BIKE_ID_TO_RENT` variable and only if the bike is available
- You want two conditions, `WHERE bike_id = $BIKE_ID_TO_RENT AND available = true`
- Add `BIKE_AVAILABILITY=$($PSQL "SELECT available FROM bikes WHERE bike_id = $BIKE_ID_TO_RENT AND available = true")` below the `get bike availability` comment
```sh
# if input is not a number
if [[ ! $BIKE_ID_TO_RENT =~ ^[0-9]+$ ]]
then
  # send to main menu
  MAIN_MENU "That is not a valid bike number."
else
  # get bike availability
  BIKE_AVAILABILITY=$($PSQL "SELECT available FROM bikes WHERE bike_id = $BIKE_ID_TO_RENT AND available = true")
  # if not available

  # send to main menu
fi
```
102. Right below the variable you just created, use echo to print it so you can see what it looks like.

*How to solve?*

- Print a variable like this: `echo $<VARIABLE_NAME>`
- The variable you want is `BIKE_AVAILABILITY`
- Add `echo $BIKE_AVAILABILITY` in the suggested area
```sh
# if input is not a number
if [[ ! $BIKE_ID_TO_RENT =~ ^[0-9]+$ ]]
then
  # send to main menu
  MAIN_MENU "That is not a valid bike number."
else
  # get bike availability
  BIKE_AVAILABILITY=$($PSQL "SELECT available FROM bikes WHERE bike_id = $BIKE_ID_TO_RENT AND available = true")
  echo $BIKE_AVAILABILITY
  # if not available

  # send to main menu
fi
```
103. Run the script a few times, go to the rent menu, enter a bike that is available and one that isn't. You should have some `BMX` bikes that aren't available.
104. The variable will be `t` or empty. Below the `if not available` comment, add an `if` condition that checks if it's empty. Put the `send to main menu` comment in it's statements area.

*How to solve?*

- Here's an example:
```sh
if [[ <CONDITION> ]]
then
  <STATEMENTS>
fi
```
- The condition you want is `-z $BIKE_AVAILABILITY`
- Place the `# send to main menu` comment in the `<STATEMENTS>` area
- The `if` condition should look like this:
```sh
if [[ -z $BIKE_AVAILABILITY ]]
then
  # send to main menu
fi
```
105. In the `if` condition you just added, send users to the main menu with the message `That bike is not available.` if they input a number that isn't available.

*How to solve?*

- You want to call the `MAIN_MENU` function with the message as an argument
- Here's an example: `MAIN_MENU "<message_here>"`
- Add `MAIN_MENU "That bike is not available."` below the send to main menu comment
```sh
# if not available
if [[ -z $BIKE_AVAILABILITY ]]
then
  # send to main menu
  MAIN_MENU "That bike is not available."
fi
```
106. Remove the line where you print the BIKE_AVAILABILITY variable. You don't need it anymore.
107. Run the script and go to the rent menu, enter a bike that isn't available to make sure it's working. When you are done, exit the program.

Full source code currently:
```sh
#!/bin/bash

PSQL="psql -X --username=freecodecamp --dbname=bikes --tuples-only -c"

echo -e "\n~~~~~ Bike Rental Shop ~~~~~\n"

MAIN_MENU() {
  if [[ $1 ]]
  then
    echo -e "\n$1"
  fi

  echo "How may I help you?" 
  echo -e "\n1. Rent a bike\n2. Return a bike\n3. Exit"
  read MAIN_MENU_SELECTION

  case $MAIN_MENU_SELECTION in
    1) RENT_MENU ;;
    2) RETURN_MENU ;;
    3) EXIT ;;
    *) MAIN_MENU "Please enter a valid option." ;;
  esac
}

RENT_MENU() {
  # get available bikes
  AVAILABLE_BIKES=$($PSQL "SELECT bike_id, type, size FROM bikes WHERE available = true ORDER BY bike_id")

  # if no bikes available
  if [[ -z $AVAILABLE_BIKES ]]
  then
    # send to main menu
    MAIN_MENU "Sorry, we don't have any bikes available right now."
  else
    # display available bikes
    echo -e "\nHere are the bikes we have available:"
    echo "$AVAILABLE_BIKES" | while read BIKE_ID BAR TYPE BAR SIZE
    do
      echo "$BIKE_ID) $SIZE\" $TYPE Bike"
    done

    # ask for bike to rent
    echo -e "\nWhich one would you like to rent?"
    read BIKE_ID_TO_RENT

    # if input is not a number
    if [[ ! $BIKE_ID_TO_RENT =~ ^[0-9]+$ ]]
    then
      # send to main menu
      MAIN_MENU "That is not a valid bike number."
    else
      # get bike availability
      BIKE_AVAILABILITY=$($PSQL "SELECT available FROM bikes WHERE bike_id = $BIKE_ID_TO_RENT AND available = true")
      
      # if not available
      if [[ -z $BIKE_AVAILABILITY ]]
      then
        # send to main menu
        MAIN_MENU "That bike is not available."
      fi
    fi
  fi
}

RETURN_MENU() {
  echo "Return Menu"
}

EXIT() {
  echo -e "\nThank you for stopping in.\n"
}

MAIN_MENU
```
108. In the psql prompt, set all the bikes availability back to true.

*How to solve?*

- Use the `UPDATE`, `SET`, and `WHERE` keywords
- Here's an example: `UPDATE <table> SET <column> = <value> WHERE <condition>`
- You want to set `available` to `true` for all the bikes
- After the `SET` can look like this: `available = true WHERE available = false`
- Try entering `UPDATE bikes SET available = true WHERE available = false;` in the psql prompt
- You can type `psql --username=freecodecamp --dbname=bikes` into the terminal to log in to psql if you aren't logged in.
109. In your script, add an `else` for when a bike is available. Add these four comments in the `else` area `get customer info`, `if customer doesn't exist`, `get new customer name`, and `insert new customer`.

*How to solve?*

- Here's an example of a single line comment: # <comment_here>
- Make sure the comments are in the same order listed
- An if/else statement looks like this:
```sh
if [[ <CONDITION> ]]
then
  <STATEMENTS>
else
  <STATEMENTS>
fi
```
- The `else` area should look like this:
```sh
else
  # get customer info

  # if customer doesn't exist

  # get new customer name

  # insert new customer

```
- The whole `if` should look like this:
```sh
if [[ -z $BIKE_AVAILABILITY  ]]
then
  # send to main menu
  MAIN_MENU "That bike is not available."
else
  # get customer info

  # if customer doesn't exist

  # get new customer name

  # insert new customer

fi
```
110. As the comments say, you need to get the customer info and find out if they are an existing customer. Below the `get customer info` comment, print `What's your phone number?` with a new line in front of it.

**Solution:** Add `echo -e "\nWhat's your phone number?"` below the suggested comment
````sh
if [[ -z $BIKE_AVAILABILITY  ]]
then
  # send to main menu
  MAIN_MENU "That bike is not available."
else
  # get customer info
  echo -e "\nWhat's your phone number?"
  # if customer doesn't exist

  # get new customer name

  # insert new customer

fi
````
111. Below the line you just printed, read input into a `PHONE_NUMBER` variable. Since the phone number is unique, you can use it to identify a customer.

*How to solution?*

Add `read PHONE_NUMBER` to the suggested area. Add it below where you print `What's your phone number?`
```sh
if [[ -z $BIKE_AVAILABILITY  ]]
then
  # send to main menu
  MAIN_MENU "That bike is not available."
else
  # get customer info
  echo -e "\nWhat's your phone number?"
  read PHONE_NUMBER
  # if customer doesn't exist

  # get new customer name

  # insert new customer

fi
```
112. With the customer's phone number, you can get their name. Below where you get the phone number, create a `CUSTOMER_NAME` variable that gets the customers name from the database using the phone number.

*How to solve?*

- Query the database to set the `CUSTOMER_NAME` variable
- Here's an example: `CUSTOMER_NAME=$($PSQL "<query_here>")`
- Use the `SELECT`, `FROM` and `WHERE` keywords for your query
- You want only the `name` column from the `customers` table
- The condition you want is `phone = '$PHONE_NUMBER'`
- The query should look like this: `SELECT name FROM customers WHERE phone = '$PHONE_NUMBER'`
- Add `CUSTOMER_NAME=$($PSQL "SELECT name FROM customers WHERE phone = '$PHONE_NUMBER'")` below the read PHONE_NUMBER line
```sh
# if not available
if [[ -z $BIKE_AVAILABILITY ]]
then
  # send to main menu
  MAIN_MENU "That bike is not available."
else
  # get customer info
  echo -e "\nWhat's your phone number?"
  read PHONE_NUMBER
  CUSTOMER_NAME=$($PSQL "SELECT name FROM customers WHERE phone = '$PHONE_NUMBER'")
  # if customer doesn't exist

  # get new customer name

  # insert new customer
fi
```
113. If the customer is in the database with the phone number used, the variable will be set to the name. If not, it will be empty. Add an `if` condition below the `if customer doesn't exist` comment that checks if the variable is empty. Place the next two comments in the `then` area.

*How to solve?*

- Here's an example:
```sh
if [[ <CONDITION> ]]
then
  <STATEMENTS>
fi
```
- The condition you want is `-z $CUSTOMER_NAME`
- Place the `# get new customer name` and `# insert new customer` comments in the `<STATEMENTS>` area
- The if condition should look like this:
```sh
if [[ -z $CUSTOMER_NAME ]]
then
  # get new customer name

  # insert new customer

fi
```
- Make sure it's below the `if customer doesn't exist` comment

114. If the customer isn't in the database, you need to get their name so you can add them. Below the `get new customer name` comment, print `What's your name?` with a new line in front of the message.

**Solution:** Add echo -e "\nWhat's your name?" below the suggested comment
```sh
# if customer doesn't exist
if [[ -z $CUSTOMER_NAME ]]
then
  # get new customer name
  echo -e "\nWhat's your name?"
  # insert new customer
fi
```
115. Below the question you just printed, read input into a variable named `CUSTOMER_NAME`.
```sh
# if customer doesn't exist
if [[ -z $CUSTOMER_NAME ]]
then
  # get new customer name
  echo -e "\nWhat's your name?"
  read CUSTOMER_NAME
  # insert new customer
fi
```
116. You have the two pieces of information you need. Below the `insert new customer` comment, create an `INSERT_CUSTOMER_RESULT` variable that inserts the customer into the database.

*How to solve?*

- Here's an example: `INSERT_CUSTOMER_RESULT=$($PSQL "<query_here>")`
- View the `customers` table in the psql prompt with `\d customers` to see the columns you need to add data to
- Be sure to use single quotes around `VARCHAR` values
- The query looks similar to this: `INSERT INTO customers(column1, column2) VALUES('value1', 'value2')`
- You want to use the `CUSTOMER_NAME` and `PHONE_NUMBER` variables for the values
- Here's the query: `INSERT INTO customers(name, phone) VALUES('$CUSTOMER_NAME', '$PHONE_NUMBER')`
- Add `INSERT_CUSTOMER_RESULT=$($PSQL "INSERT INTO customers(name, phone) VALUES('$CUSTOMER_NAME', '$PHONE_NUMBER')")` below the `insert new customer` comment
```sh
# if customer doesn't exist
if [[ -z $CUSTOMER_NAME ]]
then
  # get new customer name
  echo -e "\nWhat's your name?"
  read CUSTOMER_NAME
  # insert new customer
  INSERT_CUSTOMER_RESULT=$($PSQL "INSERT INTO customers(name, phone) VALUES('$CUSTOMER_NAME', '$PHONE_NUMBER')")
fi
```
117. Run your script and go to the rent menu. Pick a bike to rent, then enter 555-5555 when it asks for a phone number, and `Me` when it asks for your name.

Output:
```txt
~~~~~ Bike Rental Shop ~~~~~

How may I help you?

1. Rent a bike
2. Return a bike
3. Exit
1

Here are the bikes we have available:
1) 27" Mountain Bike
2) 28" Mountain Bike
3) 29" Mountain Bike
4) 27" Road Bike
5) 28" Road Bike
6) 29" Road Bike
7) 19" BMX Bike
8) 20" BMX Bike
9) 21" BMX Bike

Which one would you like to rent?
1

What's your phone number?
555-5555

What's your name?
Me
```
118. That should have added a new customer to the database. In the psql prompt, view all the data in the `customers` table to see if it's working. Solution: `SELECT * FROM customers;
```txt
+-------------+----------+------+
| customer_id |  phone   | name |
+-------------+----------+------+
|           1 | 555-5555 | Me   |
+-------------+----------+------+
(1 row)
```
119. Excellent. View all the data in the rentals table.

**Solution:** `SELECT * FROM rentals;`

Output:
```txt
+-----------+-------------+---------+-------------+---------------+
| rental_id | customer_id | bike_id | date_rented | date_returned |
+-----------+-------------+---------+-------------+---------------+
+-----------+-------------+---------+-------------+---------------+
(0 rows)
```
120. So you still need to add the rental to the rentals table when a bike is picked out. View all the data in the bikes table. `SELECT * FROM bikes;`
```txt
+---------+----------+------+-----------+
| bike_id |   type   | size | available |
+---------+----------+------+-----------+
|       1 | Mountain |   27 | t         |
|       2 | Mountain |   28 | t         |
|       3 | Mountain |   29 | t         |
|       4 | Road     |   27 | t         |
|       5 | Road     |   28 | t         |
|       6 | Road     |   29 | t         |
|       7 | BMX      |   19 | t         |
|       8 | BMX      |   20 | t         |
|       9 | BMX      |   21 | t         |
+---------+----------+------+-----------+
(9 rows)
```
121. And set the `available` column to false for the bike rented. Below the end of the `if` statement that inserts a new customer, add five more comments; `get customer_id`, `insert bike rental`, `set bike availability to false`, `get bike info`, and `send to main menu`

*How to solve?*

- Here's an example of a single line comment: # <comment_here>
- Make sure the comments are in the same order listed
- The comments should be below (not in) the if [[ -z $CUSTOMER_NAME ]] statement
- The comments should look like this:
```sh
  if [[ -z $CUSTOMER_NAME ]]
  then
    # get new customer name
    echo -e "\nWhat's your name?"
    read CUSTOMER_NAME

    # insert new customer
    INSERT_CUSTOMER_RESULT=$($PSQL "INSERT INTO customers(name, phone) VALUES('$CUSTOMER_NAME', '$PHONE_NUMBER')")
  fi

  # get customer_id

  # insert bike rental

  # set bike availability to false

  # get bike info

  # send to main menu
```
122. You're getting close to done with the rent functionality. To add a rental to the database, you need the customer ID. Below the `get customer_id` comment, create a `CUSTOMER_ID` variable that gets the `customer_id` using the phone number.

*How to solve?*

- Here's an example: CUSTOMER_ID=$($PSQL "<query_here>")
- You want to get the customer_id column from the customers table using the PHONE_NUMBER variable in your condition to get it
- The condition you want is WHERE phone = '$PHONE_NUMBER'
- The query looks like this: SELECT customer_id FROM customers WHERE phone = '$PHONE_NUMBER'
- Add CUSTOMER_ID=$($PSQL "SELECT customer_id FROM customers WHERE phone = '$PHONE_NUMBER'") below the get customer_id comment
```sh
# get customer_id
CUSTOMER_ID=$($PSQL "SELECT customer_id FROM customers WHERE phone = '$PHONE_NUMBER'")
```
123. Now that you have the bike ID and customer ID, you can add the rental to the database. Below the `insert bike rental` comment, create a `INSERT_RENTAL_RESULT` variable that adds the rental to the database.

*How to solve?*

- Here's an example: `INSERT_RENTAL_RESULT=$($PSQL "<query_here>")`
- View the `rentals` table by entering `\d rentals` in the psql prompt to see what the columns are
- The query looks similar to this: `INSERT INTO rentals(column1, column2) VALUES(value1, value2)`
- You want to insert the `BIKE_ID_TO_RENT` and `CUSTOMER_ID` variables into the `bike_id` and `customer_id` columns
- The query should look like this: `INSERT INTO rentals(bike_id, customer_id) VALUES($BIKE_ID_TO_RENT, $CUSTOMER_ID)`
- Add `INSERT_RENTAL_RESULT=$($PSQL "INSERT INTO rentals(customer_id, bike_id) VALUES($CUSTOMER_ID, $BIKE_ID_TO_RENT)")` below the insert bike rental comment
```sh
# insert bike rental
INSERT_RENTAL_RESULT=$($PSQL "INSERT INTO rentals(customer_id, bike_id) VALUES($CUSTOMER_ID, $BIKE_ID_TO_RENT)")
```
124. That should add the rental to the database. The last thing to do is set `available` to false for the bike. Below the `set bike availability to false` comment, create a `SET_TO_FALSE_RESULT` variable that does that.

*How to solve?*

- Here's an example: `SET_TO_FALSE_RESULT=$($PSQL "<query_here>")`
- You want to use the `UPDATE`, `SET`, and `WHERE` keywords
- You want to set the `available` column to false for the `bike_id` of `BIKE_ID_TO_RENT`
- The query looks similar to this: `UPDATE <table> SET <column> = <value> WHERE <condition>`
- The query looks like this: `UPDATE bikes SET available = false WHERE bike_id = $BIKE_ID_TO_RENT`
- Add `SET_TO_FALSE_RESULT=$($PSQL "UPDATE bikes SET available = false WHERE bike_id = $BIKE_ID_TO_RENT")` below the set bike availability to false comment
```sh
# set bike availability to false
SET_TO_FALSE_RESULT=$($PSQL "UPDATE bikes SET available = false WHERE bike_id = $BIKE_ID_TO_RENT")
```
125. Run the script and go to the rent menu. Pick the first bike on the list and enter 555-5555 when it asks for a phone number again. That phone number should already be in the database, so it won't ask for a name or insert a customer.
```txt
~~~~~ Bike Rental Shop ~~~~~

How may I help you?

1. Rent a bike
2. Return a bike
3. Exit
1

Here are the bikes we have available:
1) 27" Mountain Bike
2) 28" Mountain Bike
3) 29" Mountain Bike
4) 27" Road Bike
5) 28" Road Bike
6) 29" Road Bike
7) 19" BMX Bike
8) 20" BMX Bike
9) 21" BMX Bike

Which one would you like to rent?
1

What's your phone number?
555-5555
```
126. In the psql prompt, view all the data in the `rentals` table. There should be a new rental.

Output:
```txt
bikes=> SELECT * FROM rentals;
                                  
+-----------+-------------+---------+-------------+---------------+
| rental_id | customer_id | bike_id | date_rented | date_returned |
+-----------+-------------+---------+-------------+---------------+
|         1 |           1 |       1 | 2023-04-19  |               |
+-----------+-------------+---------+-------------+---------------+
(1 row)
```
127. The rental was added and the `date_rented` was filled in automatically. Next, view all the data in the `bikes` table. Order the results by `bike_id`

**Solution**: Enter SELECT * FROM bikes ORDER BY bike_id; in the psql prompt
```txt
+---------+----------+------+-----------+
| bike_id |   type   | size | available |
+---------+----------+------+-----------+
|       1 | Mountain |   27 | f         |
|       2 | Mountain |   28 | t         |
|       3 | Mountain |   29 | t         |
|       4 | Road     |   27 | t         |
|       5 | Road     |   28 | t         |
|       6 | Road     |   29 | t         |
|       7 | BMX      |   19 | t         |
|       8 | BMX      |   20 | t         |
|       9 | BMX      |   21 | t         |
+---------+----------+------+-----------+
(9 rows)
```
128. The available column was set to false for the bike you rented. The last thing to do is give a nice message about the rental. Below the `get bike info` comment, create a `BIKE_INFO` variable that gets the `size` and `type`, in that order, of the bike rented.

*How to solve?*

- Here's an example: `BIKE_INFO=$($PSQL "<query_here>")`
- You want to use the `SELECT`, `FROM`, and `WHERE` keywords
- Use the `BIKE_ID_TO_RENT` variable to find the needed info for the bike
- The query looks similar to this: `SELECT size, type FROM <table> WHERE <condition>`
- The condition you want is `WHERE bike_id = $BIKE_ID_TO_RENT`
- The query looks like this: `SELECT size, type FROM bikes WHERE bike_id = $BIKE_ID_TO_RENT`
- Add `BIKE_INFO=$($PSQL "SELECT size, type FROM bikes WHERE bike_id = $BIKE_ID_TO_RENT")` below the get bike info comment
```sh
# get bike info
BIKE_INFO=$($PSQL "SELECT size, type FROM bikes WHERE bike_id = $BIKE_ID_TO_RENT")
```
129. Below the variable you just created, use echo to print it.

**Solution:**

- Print a variable like this: `echo $<VARIABLE_NAME>`
- The variable you want is `BIKE_INFO`
- Add `echo $BIKE_INFO` in the suggested area

130. Run the script again and go to the rent menu, there should now be one less bike displayed. Pick the next bike on the list and rent it using the customer with phone number 555-5555 again so you can see the variable.

Output:
```txt
~~~~~ Bike Rental Shop ~~~~~

How may I help you?

1. Rent a bike
2. Return a bike
3. Exit
1

Here are the bikes we have available:
2) 28" Mountain Bike
3) 29" Mountain Bike
4) 27" Road Bike
5) 28" Road Bike
6) 29" Road Bike
7) 19" BMX Bike
8) 20" BMX Bike
9) 21" BMX Bike

Which one would you like to rent?
2

What's your phone number?
555-5555
28 | Mountain
```
131. It should have printed `28 | Mountain`. The message you want to print after someone rents a bike would have said `I have put you down for the 28" Mountain Bike, Me.`. You need to format that variable for the message. The `sed` command can be used to replace characters and patterns in text. It looks like this: `sed s/<regex_pattern_to_replace>/<characters_to_replace_with>/<regex_flags>`. In the terminal, enter `echo '28 | Mountain' | sed 's/ /=/g'` to practice. Output: `28=|=Mountain`
132. The command you used, "piped" a string (`28 | Mountain`) to the `sed` command, where it replaced all the spaces with `=`. Enter the same command, but replace all the spaces with nothing.

**Solution:** Enter echo '28 | Mountain' | sed 's/ //g' in the terminal. Output: `28|Mountain`

133. The `g` regex flag stands for "global". It will replace all instance of the pattern. In this case, it replaced all the spaces. Enter the same command but without that flag.

**Solution**: Enter `echo '28 | Mountain' | sed 's/ //'` in the terminal. Output: `28| Mountain`

134. That time, only the first instance of the pattern was replaced. The first space was removed. Enter the same command, but replace the first instance of  `| (<space>|)` with nothing.

**Solution:**

- You want to replace the space in the pattern of the last command with  `| (<space_here>|)`
- Enter `echo '28 | Mountain' | sed 's/ |//'` in the terminal. Output: `28 Mountain`

135. Enter the same command, but make the output look like how you want in the message, `28" Mountain`.

*How to solve?*

- Use `"` as the character to replace  `| (<space>|)` with
- Enter `echo '28 | Mountain' | sed 's/ |/"/'` in the terminal. Output: `28" Mountain`

136. Back in your script, where you `echo` the `BIKE_INFO`, pipe the output into a sed command that replaces  `| (<space>|)` with `"` so the text will read `<SIZE>" <TYPE>`. `28 | Mountain` would become `28" Mountain`, for instance.

*How to solve?*

- The previous command was `echo '28 | Mountain' | sed 's/ |/"/'`
- You want to add the `| sed 's/ |/"/'` part of the previous command after your `echo $BIKE_INFO` line
- Make the suggested area look like this:
```sh
echo $BIKE_INFO | sed 's/ |/"/'
```
137. Run the script and rent another bike using the customer with phone number 555-5555 again. Make sure the bike info printed looks like you want.

Output:
```txt
~~~~~ Bike Rental Shop ~~~~~

How may I help you?

1. Rent a bike
2. Return a bike
3. Exit
1

Here are the bikes we have available:
3) 29" Mountain Bike
4) 27" Road Bike
5) 28" Road Bike
6) 29" Road Bike
7) 19" BMX Bike
8) 20" BMX Bike
9) 21" BMX Bike

Which one would you like to rent?
3

What's your phone number?
555-5555
29" Mountain
```
138. Now it is formatted for the message. Take that `echo` command and the part that formats it, put it in a sub shell, and set the output into a variable named `BIKE_INFO_FORMATTED`. Here's an example: `BIKE_INFO_FORMATTED=$(<formatted info here>)`

*How to solve?*

- You want to put the echo `$BIKE_INFO | sed 's/ |/"/'` part in the subshell
- It should look like this: `BIKE_INFO_FORMATTED=$(echo $BIKE_INFO | sed 's/ |/"/')`
139. What you put the in subshell (`$(...)`) will be executed, and the result of it will replace the subshell. In this case, the formatted bike info was printed when you ran the script before, so the `BIKE_INFO_FORMATTED` variable will be set to that. Below the `send to main menu` comment, send users to the main menu with a message that would print `I have put you down for the 28" Mountain Bike, Me.` if `Me` rented the 28 inch Mountain Bike.

*How to solve?*

- Use dynamic info for the bike info and the customer's name
- You want to use the `BIKE_INFO_FORMATTED` and `CUSTOMER_NAME` variables
- The message should look like this: `I have put you down for the $BIKE_INFO_FORMATTED Bike, $CUSTOMER_NAME`.
- Add `MAIN_MENU "I have put you down for the $BIKE_INFO_FORMATTED Bike, $CUSTOMER_NAME."` below the send to main menu comment

140. Run the script and rent the next bike on the list. Use the customer with 555-5555 as their phone number. When you are done, exit the program.

Output:
```txt
~~~~~ Bike Rental Shop ~~~~~

How may I help you?

1. Rent a bike
2. Return a bike
3. Exit
1

Here are the bikes we have available:
4) 27" Road Bike
5) 28" Road Bike
6) 29" Road Bike
7) 19" BMX Bike
8) 20" BMX Bike
9) 21" BMX Bike

Which one would you like to rent?
4

What's your phone number?
555-5555

I have put you down for the 27" Road Bike,  Me.
How may I help you?

1. Rent a bike
2. Return a bike
3. Exit
3

Thank you for stopping in.
```
141. There's an extra space around the customer's name. You can use `sed` again to fix that. In the terminal, enter `echo ' M e '` to print `M e` with spaces around it to see if you can find out how.
142. It printed, but you can only assume there's a space at the end. Place the last command in a subshell with quotes around it. Put a period right after the subshell and echo the whole thing in the terminal. Here's how it looks: `echo "$(echo ' M e ')."`. Output: ` M e .`
143. Now you can be certain there's a space at the end. Within the subshell of the last command, use a pipe and the `sed` command to replace the first space with no space. Here's the `sed` replacement pattern you want: `'s/ //'`.

*How to solve?*

- The previous command was `echo "$(echo ' M e ')."`
- Here's an example of how the subshell should look: `$(echo ' M e ' | sed <pattern>)`
- This is the exact subshell: `$(echo ' M e ' | sed <pattern>)`
- Enter `echo "$(echo ' M e ' | sed 's/ //')."` in the terminal

Output: `M e .`

144. That removed only the first space it found. Change the previous command to replace all instances of a space instead of just the first one.

*How to solve?*

- The previous command was `echo "$(echo ' M e ' | sed 's/ //')."`
- Use a regex flag to make the suggested modification
- You want to add the `g` flag to the `sed` replacement pattern.
- The `sed` pattern should look like this: `'s/ //g'`
- Enter `echo "$(echo ' M e ' | sed 's/ //g')."` in the terminal

Output: `Me.`

145. That replaced all the spaces. You only had an extra space at the beginning of the customer name. Add a `^` in front of the space in the replacement pattern of the last command to only replace a space at the beginning of the text.

*How to solve?*

- The previous command was `echo "$(echo ' M e ' | sed 's/ //g')."`
- You want to change the matching pattern to `^  (^<space>)`
- The matching pattern is between the first and second forward slashes
- The sed pattern should look like this: `s/^ //g`
- Enter `echo "$(echo ' M e ' | sed 's/^ //g')."` in the terminal

Output: `M e .`

146. The caret you added means that's the start of the text. So it will replace a space only if it's at the beginning. Enter the last command, but add two more spaces (three total) at the beginning of the text.

*How to solve?*

- The previous command was `echo "$(echo ' M e ' | sed 's/^ //g')."`
- Change the `' M e '` part to include the suggestion
- The new text should be `'   M e ' ('<three_spaces>M e ')`
- In the terminal, enter `echo "$(echo '   M e ' | sed 's/^ //g')."`

Output: `  M e .`

147. The `^  (^<space>)` pattern only replaced the first space. Add `*` at the end of the matching pattern to replace all spaces at the beginning of text.

*How to solve?*

- The previous command was `echo "$(echo '   M e ' | sed 's/^ //g')."`
- The matching pattern is between the first and second forward slash
- The new pattern is: `'s/^ *//g'`
- Enter `echo "$(echo '   M e ' | sed 's/^ *//g')."` in the terminal

Output: `M e .`

148. The customer name only had an extra space at the beginning. Unsure as to why, but there may be others with extra spaces at the end as well. You can match the end of text with `$`. Change the matching pattern of the last command so it replaces a single space at the end. The pattern is  `$ (<space>$).`

*How to solve?*

- The previous command was `echo "$(echo '   M e ' | sed 's/^ *//g')."`
- The matching pattern is between the first and second forward slash
- Change the matching pattern to the suggestion
- Enter `echo "$(echo '   M e ' | sed 's/ $//g')."` in the terminal

Output: `   M e.`

149. Add two more spaces to the end of the text in the previous command (three spaces total).

*How to solve?*

- The matching pattern is between the first and second forward slash
- Change the matching pattern to the suggestion
- Enter `echo "$(echo '   M e   ' | sed 's/ $//g')."` in the terminal

Output: `   M e  .`

150. The pattern only replaces a single space at the end. Change the last command so it replaces all spaces at the end of the text.

*How to solve?*

- Use `*` in a pattern after a character to replace zero or more of that character
- The matching pattern you want is  `*$ (<space>*$)`
- Change the matching pattern to the suggestion
- Enter `echo "$(echo '   M e   ' | sed 's/ *$//g')."` in the terminal

Output: `   M e.`

151. That replaced all the spaces at the end of the text. You can use `|` as an `"or"` operator in a matching pattern to replace one pattern or another. Use it to change the matching pattern so it would replace any amount of spaces at the beginning and any amount of spaces at the end of the text.

*How to solve?*

- The previous command was `echo "$(echo '   M e   ' | sed 's/ *$//g')."`
- You want to replace the `^ * (^<space>*)` pattern
- And the  `*$ (<space>*$)` pattern
- The matching pattern should look like this: `'s/^ *| *$//g'`
- Enter `echo "$(echo '   M e   ' | sed 's/^ *| *$//g')."`

Output: `   M e   .`

152. That didn't work. It doesn't like that "or" (`|`) operator for some reason. Check the manual of the `sed` command to see if you can find anything.

153. Somewhere in there is a flag for using extended regular expressions with `sed`. That might work. Add it to the `echo "$(echo '   M e   ' | sed 's/^ *| *$//g')."` command that didn't work to find out.

**Solution:**

- Find the flag in the terminal output for using extended regular expressions with `sed`
- It's the `-E` flag
- You previously entered `echo "$(echo '   M e   ' | sed 's/^ *| *$//g')."`
- Add the `-E` flag to the sed part of that command
- Enter `echo "$(echo '   M e   ' | sed -E 's/^ *| *$//g')."` in the terminal

Output: `M e.`

154. That trimmed all spaces from the front and end of the text. Back in the last message of your script, place the `CUSTOMER_NAME` variable in a subshell, echo and pipe it into a `sed` command that removes all spaces from the front and back. Use the same method you used in the terminal.

*How to solve?*

- Here's an example: `$(echo $CUSTOMER_NAME | sed ...)`
- `^ *` will match all spaces at the beginning of text, and  `*$` will match spaces at the end
- The previous command was `echo "$(echo '   M e   ' | sed -r 's/^ *| *$//g')."`
- Change the $CUSTOMER_NAME variable in the last message to `$(echo $CUSTOMER_NAME | sed -r 's/^ *| *$//g')`
```sh
# send to main menu
MAIN_MENU "I have put you down for the $BIKE_INFO_FORMATTED Bike, $(echo $CUSTOMER_NAME | sed -r 's/^ *| *$//g')."
```
155. Run the script and rent another bike with the customer whose phone number is 555-5555. When you are done, exit the program.
Output:
```txt
~~~~~ Bike Rental Shop ~~~~~

How may I help you?

1. Rent a bike
2. Return a bike
3. Exit
1

Here are the bikes we have available:
5) 28" Road Bike
6) 29" Road Bike
7) 19" BMX Bike
8) 20" BMX Bike
9) 21" BMX Bike

Which one would you like to rent?
5

What's your phone number?
555-5555

I have put you down for the 28" Road Bike, Me.
How may I help you?

1. Rent a bike
2. Return a bike
3. Exit
2
Return Menu
```
156. Run the script again. Rent another bike, use `000-0000` as the phone number this time, and `Test` as the name to create a new customer. When you are done, exit the program.

Output:
```txt
~~~~~ Bike Rental Shop ~~~~~

How may I help you?

1. Rent a bike
2. Return a bike
3. Exit
1

Here are the bikes we have available:
6) 29" Road Bike
7) 19" BMX Bike
8) 20" BMX Bike
9) 21" BMX Bike

Which one would you like to rent?
6

What's your phone number?
000-0000

What's your name?
Test

I have put you down for the 29" Road Bike, Test.
How may I help you?

1. Rent a bike
2. Return a bike
3. Exit
3

Thank you for stopping in.
```
157. Run the script again. Rent another bike with the customer you just created. When you are done, exit the program.

Output:
```txt
~~~~~ Bike Rental Shop ~~~~~

How may I help you?

1. Rent a bike
2. Return a bike
3. Exit
1

Here are the bikes we have available:
7) 19" BMX Bike
8) 20" BMX Bike
9) 21" BMX Bike

Which one would you like to rent?
7

What's your phone number?
000-0000

I have put you down for the 19" BMX Bike, Test.
How may I help you?

1. Rent a bike
2. Return a bike
3. Exit
3

Thank you for stopping in.
```
158. In the psql prompt, view all the data in your bikes table in order by the `bike_id`.

*How to solve?*

- Use the `SELECT`, `FROM`, and `ORDER BY` keywords with `*` to view all the data
- Enter `SELECT * FROM bikes ORDER BY bike_id;` in the psql prompt

Output:
```txt
+---------+----------+------+-----------+
| bike_id |   type   | size | available |
+---------+----------+------+-----------+
|       1 | Mountain |   27 | f         |
|       2 | Mountain |   28 | f         |
|       3 | Mountain |   29 | f         |
|       4 | Road     |   27 | f         |
|       5 | Road     |   28 | f         |
|       6 | Road     |   29 | f         |
|       7 | BMX      |   19 | f         |
|       8 | BMX      |   20 | t         |
|       9 | BMX      |   21 | t         |
+---------+----------+------+-----------+
(9 rows)
```
159. There should be two bikes left available to rent. Next, look at all the data in the customers table. **Solution**: SELECT * FROM customers;
```txt
+-------------+----------+------+
| customer_id |  phone   | name |
+-------------+----------+------+
|           1 | 555-5555 | Me   |
|           2 | 000-0000 | Test |
+-------------+----------+------+
(2 rows)
```
160. There should two customers in that table now. Lastly, look at all the data in the rentals table. **Solution**: Enter `SELECT * FROM rentals;` in the psql prompt

Output:
```txt
+-----------+-------------+---------+-------------+---------------+
| rental_id | customer_id | bike_id | date_rented | date_returned |
+-----------+-------------+---------+-------------+---------------+
|         1 |           1 |       1 | 2021-05-25  |               |
|         2 |           1 |       2 | 2021-05-25  |               |
|         3 |           1 |       3 | 2021-05-27  |               |
|         4 |           1 |       4 | 2021-05-27  |               |
|         5 |           1 |       5 | 2023-04-20  |               |
|         6 |           2 |       6 | 2023-04-20  |               |
|         7 |           2 |       7 | 2023-04-20  |               |
+-----------+-------------+---------+-------------+---------------+
(7 rows)
```
161. The rent functionality looks like it all works. Delete the `echo Return Menu` line in the `RETURN_MENU` function so you can get started with that.
```sh
RETURN_MENU() {
  
}
```
162. Add three single line comments to the return menu function; `get customer info`, `if not found`, and `send to main menu`, in that order.
```sh
RETURN_MENU() {
  # get customer info

  # if not found

  # send to main menu

}
```
163. Below the `get customer info` comment you just added, print `What's your phone number?` with a new line in front of the sentence.

**Solution**: Add `echo -e "\nWhat's your phone number?"` below the suggested comment
```sh
# get customer info
echo -e "\nWhat's your phone number?"
```
164. Just below that, use `read` to get input into a `PHONE_NUMBER` variable.
```sh
# get customer info
echo -e "\nWhat's your phone number?"
read PHONE_NUMBER
```
165. Just below that, set the `CUSTOMER_ID` variable to a query that gets the customer ID from the database using the phone number they gave you.

*How to solve?*

- Here's an example: `CUSTOMER_ID=$($PSQL "<query_here>")`
- You want to get the `customer_id` column from the customers table using the `PHONE_NUMBER` variable in your condition to get it
- The condition you want is `WHERE phone = '$PHONE_NUMBER'`
- The query looks like this: `SELECT customer_id FROM customers WHERE phone = '$PHONE_NUMBER'`
- Add `CUSTOMER_ID=$($PSQL "SELECT customer_id FROM customers WHERE phone = '$PHONE_NUMBER'")` below the read PHONE_NUMBER line in the RETURN_MENU function
```sh
# get customer info
echo -e "\nWhat's your phone number?"
read PHONE_NUMBER
CUSTOMER_ID=$($PSQL "SELECT customer_id FROM customers WHERE phone = '$PHONE_NUMBER'")
```
166. If they are in the database, the variable will be their `customer_id`. If not, it will be empty. Below the `if not found` comment, add an if statement that checks if it's empty. Put the `send to main menu` comment in the `then` area.

*How to solve?*

- Here's an example:
```sh
if [[ <CONDITION> ]]
then
  <STATEMENTS>
fi
```
- The condition you want is -z $CUSTOMER_ID
- Place the # send to main menu comment in the <STATEMENTS> area
- The if condition should look like this:
```sh
# if not found
if [[ -z $CUSTOMER_ID ]]
then
  # send to main menu
fi
```
167. If the customer isn't found, send them to the main menu with the message `I could not find a record for that phone number.`

**Solution**:

- You want to call the `MAIN_MENU` function with the message as an argument
- Here's an example: `MAIN_MENU "<message_here>"`
- Add `MAIN_MENU "I could not find a record for that phone number."` below the send to main menu comment
```sh
RETURN_MENU() {
  # get customer info
  echo -e "\nWhat's your phone number?"
  read PHONE_NUMBER
  CUSTOMER_ID=$($PSQL "SELECT customer_id FROM customers WHERE phone = '$PHONE_NUMBER'")
  # if not found
  if [[ -z $CUSTOMER_ID ]]
  then
    # send to main menu
    MAIN_MENU "I could not find a record for that phone number."
  fi
}
```
168. Run the script and go to the return menu. Enter a phone number that is not in the database. When you are done, exit the program.
169. Add an else to the if condition for if the phone number is found in the database. Place get customer's rentals, if no rentals, and send to main menu in the else area as single line comments.

*How to solve?*

- Here's an example of a single line comment: # <comment_here>
- Make sure the comments are in the same order listed
- The comments should be in the else area of the if [[ -z CUSTOMER_ID ]] statement
- An if/else statement looks like this:

```sh
if [[ <CONDITION> ]]
then
  <STATEMENTS>
else
  <STATEMENTS>
fi
```
- The else area should look like this:
```sh
else
  # get customer's rentals

  # if no rentals

  # send to main menu

fi
```
- The whole if should look like this:
```sh
if [[ -z $CUSTOMER_ID  ]]
then
  # send to main menu
  MAIN_MENU "I could not find a record for that phone number."
else
  # get customer's rentals

  # if no rentals

  # send to main menu

fi
```
170. You want to find out what rentals a customer has using their phone number and display them. You will need to join all the tables. Start by using the psql prompt to view all the data in the `bikes` table.
```txt
+---------+----------+------+-----------+
| bike_id |   type   | size | available |
+---------+----------+------+-----------+
|       9 | BMX      |   21 | t         |
|       1 | Mountain |   27 | f         |
|       2 | Mountain |   28 | f         |
|       3 | Mountain |   29 | f         |
|       4 | Road     |   27 | f         |
|       5 | Road     |   28 | f         |
|       6 | Road     |   29 | f         |
|       7 | BMX      |   19 | f         |
|       8 | BMX      |   20 | f         |
+---------+----------+------+-----------+
(9 rows)
```
171. Next, use a LEFT JOIN with bikes as the left table to join the bikes and rentals tables. Use the USING keyword to join the two tables. **Solution**: Enter `SELECT * FROM bikes LEFT JOIN rentals USING(bike_id);` in the psql prompt
```txt
+---------+----------+------+-----------+-----------+-------------+-------------+---------------+
| bike_id |   type   | size | available | rental_id | customer_id | date_rented | date_returned |
+---------+----------+------+-----------+-----------+-------------+-------------+---------------+
|       9 | BMX      |   21 | t         |           |             |             |               |
|       1 | Mountain |   27 | f         |         1 |           1 | 2021-05-25  |               |
|       2 | Mountain |   28 | f         |         2 |           1 | 2021-05-25  |               |
|       3 | Mountain |   29 | f         |         3 |           1 | 2021-05-27  |               |
|       4 | Road     |   27 | f         |         4 |           1 | 2021-05-27  |               |
|       5 | Road     |   28 | f         |         5 |           1 | 2023-04-20  |               |
|       6 | Road     |   29 | f         |         6 |           2 | 2023-04-20  |               |
|       7 | BMX      |   19 | f         |         7 |           2 | 2023-04-20  |               |
|       8 | BMX      |   20 | f         |         8 |           3 | 2023-04-20  |               |
+---------+----------+------+-----------+-----------+-------------+-------------+---------------+
(9 rows)
```
172. You only need the bikes that are being rented. Use an inner join with the same two tables to only get those. Use the `USING` keyword again. **Solution**: `SELECT * FROM bikes INNER JOIN rentals USING(bike_id);`
```txt
+---------+----------+------+-----------+-----------+-------------+-------------+---------------+
| bike_id |   type   | size | available | rental_id | customer_id | date_rented | date_returned |
+---------+----------+------+-----------+-----------+-------------+-------------+---------------+
|       1 | Mountain |   27 | f         |         1 |           1 | 2021-05-25  |               |
|       2 | Mountain |   28 | f         |         2 |           1 | 2021-05-25  |               |
|       3 | Mountain |   29 | f         |         3 |           1 | 2021-05-27  |               |
|       4 | Road     |   27 | f         |         4 |           1 | 2021-05-27  |               |
|       5 | Road     |   28 | f         |         5 |           1 | 2023-04-20  |               |
|       6 | Road     |   29 | f         |         6 |           2 | 2023-04-20  |               |
|       7 | BMX      |   19 | f         |         7 |           2 | 2023-04-20  |               |
|       8 | BMX      |   20 | f         |         8 |           3 | 2023-04-20  |               |
+---------+----------+------+-----------+-----------+-------------+-------------+---------------+
(8 rows)
```
173. Add a join to the previous command that joins the last table so you can get the customer information. Use an INNER JOIN and the USING keyword again.

**Solution**: Enter `SELECT * FROM bikes INNER JOIN rentals USING(bike_id) INNER JOIN customers USING(customer_id);` in the psql prompt

Output:
```txt
+-------------+---------+----------+------+-----------+-----------+-------------+---------------+----------+------+
| customer_id | bike_id |   type   | size | available | rental_id | date_rented | date_returned |  phone   | name |
+-------------+---------+----------+------+-----------+-----------+-------------+---------------+----------+------+
|           1 |       1 | Mountain |   27 | f         |         1 | 2021-05-25  |               | 555-5555 | Me   |
|           1 |       2 | Mountain |   28 | f         |         2 | 2021-05-25  |               | 555-5555 | Me   |
|           1 |       3 | Mountain |   29 | f         |         3 | 2021-05-27  |               | 555-5555 | Me   |
|           1 |       4 | Road     |   27 | f         |         4 | 2021-05-27  |               | 555-5555 | Me   |
|           1 |       5 | Road     |   28 | f         |         5 | 2021-05-27  |               | 555-5555 | Me   |
|           2 |       6 | Road     |   29 | f         |         6 | 2021-05-27  |               | 000-0000 | Test |
|           2 |       7 | BMX      |   19 | f         |         7 | 2021-05-27  |               | 000-0000 | Test |
+-------------+---------+----------+------+-----------+-----------+-------------+---------------+----------+------+
(7 rows)
```
174. Add two conditions to the last query to narrow down the results to the bikes that are currently being rented by customer with 555-5555 as their phone number. The second condition should check the `date_returned` column

**Solution**:

- The previous query was `SELECT * FROM bikes INNER JOIN rentals USING(bike_id) INNER JOIN customers USING(customer_id);`
- You want to add a `WHERE <condition_1> AND <condition_2>` to the last query
- Use the `IS NULL` keyword to check the `date_returned` in one of the conditions
- The two conditions are `WHERE phone = '555-5555' AND date_returned IS NULL`
- Enter `SELECT * FROM bikes INNER JOIN rentals USING(bike_id) INNER JOIN customers USING(customer_id) WHERE phone = '555-5555' AND date_returned IS NULL;` in the psql prompt
- You can type `psql --username=freecodecamp --dbname=bikes` into the terminal to log in to psql if you aren't logged in.

Output:
```txt
+-------------+---------+----------+------+-----------+-----------+-------------+---------------+----------+------+
| customer_id | bike_id |   type   | size | available | rental_id | date_rented | date_returned |  phone   | name |
+-------------+---------+----------+------+-----------+-----------+-------------+---------------+----------+------+
|           1 |       1 | Mountain |   27 | f         |         1 | 2021-05-25  |               | 555-5555 | Me   |
|           1 |       2 | Mountain |   28 | f         |         2 | 2021-05-25  |               | 555-5555 | Me   |
|           1 |       3 | Mountain |   29 | f         |         3 | 2021-05-27  |               | 555-5555 | Me   |
|           1 |       4 | Road     |   27 | f         |         4 | 2021-05-27  |               | 555-5555 | Me   |
|           1 |       5 | Road     |   28 | f         |         5 | 2021-05-27  |               | 555-5555 | Me   |
+-------------+---------+----------+------+-----------+-----------+-------------+---------------+----------+------+
(5 rows)
```
175. Now you have all the rentals for one specific customer. Only get the columns you need to display the bike information to them. They are the same three columns you used to display the list of available bikes.

*How to solve?*

- The previous query was `SELECT * FROM bikes INNER JOIN rentals USING(bike_id) INNER JOIN customers USING(customer_id) WHERE phone = '555-5555' AND date_returned IS NULL;`
- The three columns you want are `bike_id`, `type`, and `size`
- Enter `SELECT bike_id, type, size FROM bikes INNER JOIN rentals USING(bike_id) INNER JOIN customers USING(customer_id) WHERE phone = '555-5555' AND date_returned IS NULL;` in the psql prompt
- You can type `psql --username=freecodecamp --dbname=bikes` into the terminal to log in to psql if you aren't logged in.

Output:
```txt
+---------+----------+------+
| bike_id |   type   | size |
+---------+----------+------+
|       1 | Mountain |   27 |
|       2 | Mountain |   28 |
|       3 | Mountain |   29 |
|       4 | Road     |   27 |
|       5 | Road     |   28 |
+---------+----------+------+
(5 rows)
```
176. One more thing, order the results of the last query by their `bike_id` column.

*How to solve?*

- The previous query was `SELECT bike_id, type, size FROM bikes INNER JOIN rentals USING(bike_id) INNER JOIN customers USING(customer_id) WHERE phone = '555-5555' AND date_returned IS NULL;`
- Add `ORDER BY bike_id` to the end of the last query
- Enter `SELECT bike_id, type, size FROM bikes INNER JOIN rentals USING(bike_id) INNER JOIN customers USING(customer_id) WHERE phone = '555-5555' AND date_returned IS NULL ORDER BY bike_id;` in the psql prompt
- You can type `psql --username=freecodecamp --dbname=bikes` into the terminal to log in to psql if you aren't logged in.

Output:
```txt
+---------+----------+------+
| bike_id |   type   | size |
+---------+----------+------+
|       1 | Mountain |   27 |
|       2 | Mountain |   28 |
|       3 | Mountain |   29 |
|       4 | Road     |   27 |
|       5 | Road     |   28 |
+---------+----------+------+
(5 rows)
```
177. That's the query you will need to use to get the bikes a customer is renting. In your script below the `get customer's rentals` comment. Create a `CUSTOMER_RENTALS` variable that gets the rentals for the customer. Use the `PHONE_NUMBER` variable to get them.

*How to solve?*

- Here's an example: `CUSTOMER_RENTALS=$($PSQL "<query_here>")`
- You previously entered `SELECT bike_id, type, size FROM bikes INNER JOIN rentals USING(bike_id) INNER JOIN customers USING(customer_id) WHERE phone = '555-5555' AND date_returned IS NULL ORDER BY bike_id;` in the psql prompt
- All the columns and tables should be in the same order as in the above query
- The query looks like this: `SELECT bike_id, type, size FROM bikes INNER JOIN rentals USING(bike_id) INNER JOIN customers USING(customer_id) WHERE phone = '$PHONE_NUMBER' AND date_returned IS NULL ORDER BY bike_id`
- Add `CUSTOMER_RENTALS=$($PSQL "SELECT bike_id, type, size FROM bikes INNER JOIN rentals USING(bike_id) INNER JOIN customers USING(customer_id) WHERE phone = '$PHONE_NUMBER' AND date_returned IS NULL ORDER BY bike_id")` below the `get customer's rentals` comment
```sh
RETURN_MENU() {
  # get customer info
  echo -e "\nWhat's your phone number?"
  read PHONE_NUMBER

  CUSTOMER_ID=$($PSQL "SELECT customer_id FROM customers WHERE phone = '$PHONE_NUMBER'")

  # if not found
  if [[ -z $CUSTOMER_ID  ]]
  then
    # send to main menu
    MAIN_MENU "I could not find a record for that phone number."
  else
    # get customer's rentals
    CUSTOMER_RENTALS=$($PSQL "SELECT bike_id, type, size FROM bikes INNER JOIN rentals USING(bike_id) INNER JOIN customers USING(customer_id) WHERE phone = '$PHONE_NUMBER' AND date_returned IS NULL ORDER BY bike_id")
    # if no rentals

    # send to main menu

  fi
}
```
178. Below the variable you just created, use echo to print it. Make sure to put double quotes around it.

**Hint**: Add `echo "$CUSTOMER_RENTALS"` to the suggested area

179. Run the script and go to the return menu. Enter 555-5555 for the phone number to see the rentals for Me.
```txt
~~~~~ Bike Rental Shop ~~~~~

How may I help you?

1. Rent a bike
2. Return a bike
3. Exit
1

Here are the bikes we have available:
8) 20" BMX Bike
9) 21" BMX Bike

Which one would you like to rent?
8

What's your phone number?
555-5555

I have put you down for the 20" BMX Bike, Me.
How may I help you?

1. Rent a bike
2. Return a bike
3. Exit
3

Thank you for stopping in.
```
180. The query is working. If the customer has no rentals, the variable will be empty. Below the `if no rentals` comment, add an if condition that checks if it's empty. Put the `send to main` menu comment in the then area again.

*How to solve?*

- Here's an example:
```sh
if [[ <CONDITION> ]]
then
  <STATEMENTS>
fi
```
- The condition you want is `-z $CUSTOMER_RENTALS`
- Place the `# send to main menu` comment in the `<STATEMENTS>` area
- The `if` condition should look like this:
```sh
# if no rentals
if [[ -z $CUSTOMER_RENTALS ]]
then
  # send to main menu
fi
```
181. If the customer has no rentals, send them to the main menu with the message `You do not have any bikes rented.` Add the code below the next comment.

**Hint**:

- You want to call the `MAIN_MENU` function with the message as an argument
- Here's an example: `MAIN_MENU "<message_here>"`
- Add `MAIN_MENU "You do not have any bikes rented."` below the `send to main menu` comment

182. Add an `else` to the condition for when the customer does have rentals. Place four single line comments in it; `display rented bikes`, `ask for bike to return`, `if not a number`, and `send to main menu`.

**Solution:**

- Here's an example of a single line comment: `# <comment_here>`
- Make sure the comments are in the same order listed
- The comments should be in the `else` area of the `if [[ -z CUSTOMER_RENTALS ]]` statement
- The `else` area should look like this:
```sh
else
  # display rented bikes

  # ask for bike to return

  # if not a number

  # send to main menu

fi
```
- The whole `if` should look like this:
```sh
if [[ -z $CUSTOMER_RENTALS  ]]
then
  # send to main menu
  MAIN_MENU "You do not have any bikes rented."
else
  # display rented bikes

  # ask for bike to return

  # if not a number

  # send to main menu

fi
```
183. Below the display rented bikes comment, print `Here are your rentals:` with a new line in front of it.

*How to solve?*

- Use `echo` with the `-e` flag and the new line character (`\n`) to print the suggested message
- Use double quotes around the message
- Here's an example: `echo -e "\n<message_here>"`
- Add `echo -e "\nHere are your rentals:"` below the suggested comment

184. Move the `echo $CUSTOMER_RENTALS` line to below the line you just printed.

*How to solve?*

- Move the suggested code below where you print `Here are your rentals:`
- You should only print the variable in that one spot
- Place the `echo "$CUSTOMER_RENTALS"` line in the suggested spot
```sh
RETURN_MENU() {
  # get customer info
  echo -e "\nWhat's your phone number?"
  read PHONE_NUMBER

  CUSTOMER_ID=$($PSQL "SELECT customer_id FROM customers WHERE phone = '$PHONE_NUMBER'")

  # if not found
  if [[ -z $CUSTOMER_ID  ]]
  then
    # send to main menu
    MAIN_MENU "I could not find a record for that phone number."
  else
    # get customer's rentals
    CUSTOMER_RENTALS=$($PSQL "SELECT bike_id, type, size FROM bikes INNER JOIN rentals USING(bike_id) INNER JOIN customers USING(customer_id) WHERE phone = '$PHONE_NUMBER' AND date_returned IS NULL ORDER BY bike_id")
    # if no rentals
    if [[ -z $CUSTOMER_RENTALS ]]
    then
      # send to main menu
      MAIN_MENU "You do not have any bikes rented."
    else
      # display rented bikes
      echo -e "\nHere are your rentals:"
      echo "$CUSTOMER_RENTALS"
      # ask for bike to return

      # if not a number

      # send to main menu
    fi
  fi
}
```
185. Run the script and go to the return menu. Enter `555-5555` for the phone number to see the rented bikes.
```txt
What's your phone number?
555-5555

Here are your rentals:
       1 | Mountain |   27
       2 | Mountain |   28
       3 | Mountain |   29
       4 | Road     |   27
       5 | Road     |   28
```
186. Where you print the list of rented bikes, pipe the command into a `while` loop that reads the data. You should read the data into `BIKE_ID`, `BAR`, `TYPE`, `BAR`, and `SIZE` variables. Make it print each rented bike in the same fashion as the list of available bikes.

**Solution:**

- Here's an example:
```sh
echo "$CUSTOMER_RENTALS" | while read <VARIABLES>
do
  echo <RENTED_BIKE_INFORMATION>
done
```
- The first line should look like this: `echo "$CUSTOMER_RENTALS" | while read BIKE_ID BAR TYPE BAR SIZE`
- The loop should print `1) 27" Mountain Bike` for each bike with the appropriate bike info
- The whole thing looks like this:
```sh
echo "$CUSTOMER_RENTALS" | while read BIKE_ID BAR TYPE BAR SIZE
do
  echo "$BIKE_ID) $SIZE\" $TYPE Bike"
done
```
187. Run the script and go to the return menu. Enter the same phone number again to make sure the list is showing up correctly.

Output:
```txt
~~~~~ Bike Rental Shop ~~~~~

How may I help you?

1. Rent a bike
2. Return a bike
3. Exit
1

Sorry, we don't have any bikes available right now.
How may I help you?

1. Rent a bike
2. Return a bike
3. Exit
2

What's your phone number?
555-5555

Here are your rentals:
1) 27" Mountain Bike
2) 28" Mountain Bike
3) 29" Mountain Bike
4) 27" Road Bike
5) 28" Road Bike
8) 20" BMX Bike
9) 21" BMX Bike
```
188. Below the `ask for bike to return` comment, print `Which one would you like to return?` with a new line in front of it.

*How to solve?*

- Use `echo` with the `-e` flag and the new line character (`\n`) to print the suggested message
- Use double quotes around the message
- Here's an example: `echo -e "\n<message_here>"`
- Add `echo -e "\nWhich one would you like to return?"` below the suggested comment
```sh
# ask for bike to return
echo -e "\nWhich one would you like to return?"
```
189. Below the line you just printed, read input into a `BIKE_ID_TO_RETURN` variable.

*How to solve?*

- Here's an example: `read <VARIABLE_NAME>`
- Add `read BIKE_ID_TO_RETURN` to the suggested area
- Add it below where you print `Which one would you like to return?`

190. Below the `if not a number` comment, check if the input for the bike ID to return is a number using the same method you did earlier. Place the `send to main menu` comment in the statement.

*How to solve?*

- Here's an example:
```sh
if [[ <CONDITION> ]]
then
  <STATEMENTS>
fi
```
- The condition should check that the `$BIKE_ID_TO_RETURN` variable is not a number using the pattern matching operator (`=~`) and the pattern `^[0-9]+$`
- The condition you want is `[[ ! $BIKE_ID_TO_RETURN =~ ^[0-9]+$ ]]`
- Place the `# send to main menu` comment in the `<STATEMENTS>` area
- The `if` condition should look like this:
```sh
if [[ ! $BIKE_ID_TO_RETURN =~ ^[0-9]+$ ]]
then
  # send to main menu

fi
```
191. If they don't input a number, send them to the main menu with `That is not a valid bike number.` as the message.

*How to solve?*

- You want to call the `MAIN_MENU` function with the message as an argument
- Here's an example: `MAIN_MENU "<message_here>"`
- Add `MAIN_MENU "That is not a valid bike number."` below the `send to main menu` comment

192. Add an `else` for when they do input a number. Place `check if input is rented`, `if input not rented`, and `send to main menu` single line comments in it.
```sh
else
  # check if input is rented

  # if input not rented

  # send to main menu
fi
```
193. You need to check if the input is a `bike_id` rented by the customer so you can return it. In the psql prompt, join the `rentals` and `customers` tables with an `INNER JOIN` using the `USING` keyword.

*How to solve?*

- You need the `SELECT`, `FROM`, `INNER JOIN`, and `USING` keywords
- Here's an example: `SELECT <column> FROM <table_1> INNER JOIN <table_2> USING(<foreign_key>)`
- Enter `\d rentals` or `\d customers` in the psql prompt to view the details of the table and find the foreign key column
- It's the `customer_id` column
- Enter `SELECT * FROM rentals INNER JOIN customers USING(customer_id);` in the psql prompt
- You can type `psql --username=freecodecamp --dbname=bikes` into the terminal to log in to psql if you aren't logged in.

Output:
```txt
+-------------+-----------+---------+-------------+---------------+----------+------+
| customer_id | rental_id | bike_id | date_rented | date_returned |  phone   | name |
+-------------+-----------+---------+-------------+---------------+----------+------+
|           1 |         1 |       1 | 2021-05-25  |               | 555-5555 | Me   |
|           1 |         2 |       2 | 2021-05-25  |               | 555-5555 | Me   |
|           1 |         3 |       3 | 2021-05-27  |               | 555-5555 | Me   |
|           1 |         4 |       4 | 2021-05-27  |               | 555-5555 | Me   |
|           1 |         5 |       5 | 2021-05-27  |               | 555-5555 | Me   |
|           2 |         6 |       6 | 2021-05-27  |               | 000-0000 | Test |
|           2 |         7 |       7 | 2021-05-27  |               | 000-0000 | Test |
|           1 |         8 |       8 | 2023-04-20  |               | 555-5555 | Me   |
|           1 |         9 |       9 | 2023-04-20  |               | 555-5555 | Me   |
+-------------+-----------+---------+-------------+---------------+----------+------+
(9 rows)
```
194. Add three conditions to the previous query. Check the `phone`, `bike_id`, and `date_returned` columns to narrow the results to the first bike you rented with `Me`.

*How to solve?*

- The previous query was `SELECT * FROM rentals INNER JOIN customers USING(customer_id);`
- You want to add a `WHERE <condition_1> AND <condition_2> AND <condition_3>` to the last query
- Use the `IS NULL` keyword to check the `date_returned` in one of the conditions
- The other two conditions should check the `phone` and `bike_id` of the first rental
- The three conditions are `WHERE phone = '555-5555' AND bike_id = 1 AND date_returned IS NULL`
- Enter `SELECT * FROM rentals INNER JOIN customers USING(customer_id) WHERE phone = '555-5555' AND bike_id = 1 AND date_returned IS NULL;` in the psql prompt
- You can type `psql --username=freecodecamp --dbname=bikes` into the terminal to log in to psql if you aren't logged in.

Output:
```txt
+-------------+-----------+---------+-------------+---------------+----------+------+
| customer_id | rental_id | bike_id | date_rented | date_returned |  phone   | name |
+-------------+-----------+---------+-------------+---------------+----------+------+
|           1 |         1 |       1 | 2021-05-25  |               | 555-5555 | Me   |
+-------------+-----------+---------+-------------+---------------+----------+------+
(1 row)
```
195. You only need to know what bike is going to be returned. Narrow the columns from the last query to only get the one column you would need for returning a bike.

*How to solve?*

- The previous query was `SELECT * FROM rentals INNER JOIN customers USING(customer_id) WHERE phone = '555-5555' AND bike_id = 1 AND date_returned IS NULL;`
- Only column you need is the `rental_id` column
- Enter `SELECT rental_id FROM rentals INNER JOIN customers USING(customer_id) WHERE phone = '555-5555' AND bike_id = 1 AND date_returned IS NULL;` in the psql prompt
- You can type `psql --username=freecodecamp --dbname=bikes` into the terminal to log in to psql if you aren't logged in.

Output:
```txt
+-----------+
| rental_id |
+-----------+
|         1 |
+-----------+
(1 row)
```
196. Back in the script, below the `check if input is rented` comment, create a `RENTAL_ID` variable that gets the rental ID of the bike that was input.

Hint: 

- The input is the `BIKE_ID_TO_RETURN` variable
- Here's an example: `RENTAL_ID=$($PSQL "<query_here>")`
- You previously entered `SELECT rental_id FROM rentals INNER JOIN customers USING(customer_id) WHERE phone = '555-5555' AND bike_id = 1 AND date_returned IS NULL;` in the psql prompt
- Be sure to use the same columns from the above query for the conditions with the `PHONE_NUMBER` and `BIKE_ID_TO_RETURN` variables
- Add `RENTAL_ID=$($PSQL "SELECT rental_id FROM rentals INNER JOIN customers USING(customer_id) WHERE phone = '$PHONE_NUMBER' AND bike_id = $BIKE_ID_TO_RETURN AND date_returned IS NULL")` below the check if input is rented comment

197. Below the `if input not rented` comment, add an `if` that checks if the `RENTAL_ID` variable is empty. Place the `send to main menu` comment in the then area.

Hint:

```sh
if [[ -z $RENTAL_ID ]]
then
  # send to main menu

fi
```
198. If the input isn't rented by the given customer, send them to the main menu with `You do not have that bike rented.` as the message.

Hint: `MAIN_MENU "You do not have that bike rented."`

199. Add an else to the if condition you just added. Use `echo` to print `Rental ID $RENTAL_ID found` in it so you can see if it's all working.

Hint:
```sh
if [[ -z $RENTAL_ID ]]
then
  # send to main menu
  MAIN_MENU "You do not have that bike rented."
else
  echo "Rental ID $RENTAL_ID found"
fi
```
200. Run the script and go to the return menu. Enter 555-5555 to see the rented bikes. Input a bike that isn't on the list, then go to the menu again and input a bike that is on the list.

Output:
```txt

How may I help you?

1. Rent a bike
2. Return a bike
3. Exit
2

What's your phone number?
555-5555

Here are your rentals:
1) 27" Mountain Bike
2) 28" Mountain Bike
3) 29" Mountain Bike
4) 27" Road Bike
5) 28" Road Bike

Which one would you like to return?
1
Rental ID          1 founds
```
201. Looks like it works. Delete the line where you print the rental ID. Hint: Delete: `echo "Rental ID $RENTAL_ID found"`
202. Add three single line comments in the else area; `update date_returned`, `set bike availability to true`, and `send to main menu`.

Hint:
```sh
else
  # update date_returned

  # set bike availability to true

  # send to main menu
  
fi
```
203. After a person picks a bike to return and you know that it's a bike they have rented, you need to update all the info in the database to return it. Below the `update date_returned` comment, create a `RETURN_BIKE_RESULT` variable that sets the `date_returned` column to `NOW()` for the bike rented. Use the `RENTAL_ID` to figure out which row to update.
```sh
# update date_returned
RETURN_BIKE_RESULT=$($PSQL "UPDATE rentals SET date_returned = NOW() WHERE rental_id = $RENTAL_ID")
```
204. That should update the rentals table. Lastly, you need to make the bike available again. Below the `set bike availability to true` comment, create a `SET_TO_TRUE_RESULT` variable that makes the bike available again.

Hint:
```sh
# set bike availability to true
SET_TO_TRUE_RESULT=$($PSQL "UPDATE bikes SET available = true WHERE bike_id = $BIKE_ID_TO_RETURN")
```
205. After all that is done, send them to the main menu with `Thank you for returning your bike.` as the message.
```sh
# send to main menu
MAIN_MENU "Thank you for returning your bike."
```
206. Run the script and return one of the bikes that `Me` has rented out. When you are done, exit the program.
207. In the psql prompt, view all the data in the `rentals` table.

Output:
```txt
+-----------+-------------+---------+-------------+---------------+
| rental_id | customer_id | bike_id | date_rented | date_returned |
+-----------+-------------+---------+-------------+---------------+
|         4 |           1 |       4 | 2023-04-27  |               |
|         5 |           1 |       5 | 2023-04-27  |               |
|         6 |           2 |       6 | 2023-04-27  |               |
|         7 |           2 |       7 | 2023-04-27  |               |
|         8 |           3 |       8 | 2023-04-27  |               |
|         1 |           1 |       1 | 2023-04-27  | 2023-04-27    |
|         2 |           1 |       2 | 2023-04-27  | 2023-04-27    |
|         3 |           1 |       3 | 2023-04-27  | 2023-04-27    |
+-----------+-------------+---------+-------------+---------------+
(8 rows)
```
208. Now the rental has been returned. View all the data in the `bikes` table in order by their `bike_id`.

Output:
```txt
bikes=> SELECT * FROM bikes ORDER BY bike_id;
bikes=>                      
+---------+----------+------+-----------+
| bike_id |   type   | size | available |
+---------+----------+------+-----------+
|       1 | Mountain |   27 | t         |
|       2 | Mountain |   28 | t         |
|       3 | Mountain |   29 | t         |
|       4 | Road     |   27 | f         |
|       5 | Road     |   28 | f         |
|       6 | Road     |   29 | f         |
|       7 | BMX      |   19 | f         |
|       8 | BMX      |   20 | f         |
|       9 | BMX      |   21 | t         |
+---------+----------+------+-----------+
(9 rows)
```
209. And the bike is available again. This is the last step. Run the script once more. Feel free to play around, rent and return some bikes. When you are ready to be done, return all the bikes you rented and exit the program.

Here is my full source code:
```sh
#!/bin/bash

PSQL="psql -X --username=freecodecamp --dbname=bikes --tuples-only -c"

echo -e "\n~~~~~ Bike Rental Shop ~~~~~\n"

MAIN_MENU() {
  if [[ $1 ]]
  then
    echo -e "\n$1"
  fi

  echo "How may I help you?" 
  echo -e "\n1. Rent a bike\n2. Return a bike\n3. Exit"
  read MAIN_MENU_SELECTION

  case $MAIN_MENU_SELECTION in
    1) RENT_MENU ;;
    2) RETURN_MENU ;;
    3) EXIT ;;
    *) MAIN_MENU "Please enter a valid option." ;;
  esac
}

RENT_MENU() {
  # get available bikes
  AVAILABLE_BIKES=$($PSQL "SELECT bike_id, type, size FROM bikes WHERE available = true ORDER BY bike_id")

  # if no bikes available
  if [[ -z $AVAILABLE_BIKES ]]
  then
    # send to main menu
    MAIN_MENU "Sorry, we don't have any bikes available right now."
  else
    # display available bikes
    echo -e "\nHere are the bikes we have available:"
    echo "$AVAILABLE_BIKES" | while read BIKE_ID BAR TYPE BAR SIZE
    do
      echo "$BIKE_ID) $SIZE\" $TYPE Bike"
    done

    # ask for bike to rent
    echo -e "\nWhich one would you like to rent?"
    read BIKE_ID_TO_RENT

    # if input is not a number
    if [[ ! $BIKE_ID_TO_RENT =~ ^[0-9]+$ ]]
    then
      # send to main menu
      MAIN_MENU "That is not a valid bike number."
    else
      # get bike availability
      BIKE_AVAILABILITY=$($PSQL "SELECT available FROM bikes WHERE bike_id = $BIKE_ID_TO_RENT AND available = true")

      # if not available
      if [[ -z $BIKE_AVAILABILITY ]]
      then
        # send to main menu
        MAIN_MENU "That bike is not available."
      else
        # get customer info
        echo -e "\nWhat's your phone number?"
        read PHONE_NUMBER

        CUSTOMER_NAME=$($PSQL "SELECT name FROM customers WHERE phone = '$PHONE_NUMBER'")

        # if customer doesn't exist
        if [[ -z $CUSTOMER_NAME ]]
        then
          # get new customer name
          echo -e "\nWhat's your name?"
          read CUSTOMER_NAME

          # insert new customer
          INSERT_CUSTOMER_RESULT=$($PSQL "INSERT INTO customers(name, phone) VALUES('$CUSTOMER_NAME', '$PHONE_NUMBER')") 
        fi

        # get customer_id
        CUSTOMER_ID=$($PSQL "SELECT customer_id FROM customers WHERE phone='$PHONE_NUMBER'")

        # insert bike rental
        INSERT_RENTAL_RESULT=$($PSQL "INSERT INTO rentals(customer_id, bike_id) VALUES($CUSTOMER_ID, $BIKE_ID_TO_RENT)")

        # set bike availability to false
        SET_TO_FALSE_RESULT=$($PSQL "UPDATE bikes SET available = false WHERE bike_id = $BIKE_ID_TO_RENT")

        # get bike info
        BIKE_INFO=$($PSQL "SELECT size, type FROM bikes WHERE bike_id = $BIKE_ID_TO_RENT")
        BIKE_INFO_FORMATTED=$(echo $BIKE_INFO | sed 's/ |/"/')
        
        # send to main menu
        MAIN_MENU "I have put you down for the $BIKE_INFO_FORMATTED Bike, $(echo $CUSTOMER_NAME | sed -r 's/^ *| *$//g')."
      fi
    fi
  fi
}

RETURN_MENU() {
  # get customer info
  echo -e "\nWhat's your phone number?"
  read PHONE_NUMBER

  CUSTOMER_ID=$($PSQL "SELECT customer_id FROM customers WHERE phone = '$PHONE_NUMBER'")

  # if not found
  if [[ -z $CUSTOMER_ID  ]]
  then
    # send to main menu
    MAIN_MENU "I could not find a record for that phone number."
  else
    # get customer's rentals
    CUSTOMER_RENTALS=$($PSQL "SELECT bike_id, type, size FROM bikes INNER JOIN rentals USING(bike_id) INNER JOIN customers USING(customer_id) WHERE phone = '$PHONE_NUMBER' AND date_returned IS NULL ORDER BY bike_id")

    # if no rentals
    if [[ -z $CUSTOMER_RENTALS  ]]
    then
      # send to main menu
      MAIN_MENU "You do not have any bikes rented."
    else
      # display rented bikes
      echo -e "\nHere are your rentals:"
      echo "$CUSTOMER_RENTALS" | while read BIKE_ID BAR TYPE BAR SIZE
      do
        echo "$BIKE_ID) $SIZE\" $TYPE Bike"
      done

      # ask for bike to return
      echo -e "\nWhich one would you like to return?"
      read BIKE_ID_TO_RETURN

      # if not a number
      if [[ ! $BIKE_ID_TO_RETURN =~ ^[0-9]+$ ]]
      then
        # send to main menu
        MAIN_MENU "That is not a valid bike number."
      else
        # check if input is rented
        RENTAL_ID=$($PSQL "SELECT rental_id FROM rentals INNER JOIN customers USING(customer_id) WHERE phone = '$PHONE_NUMBER' AND bike_id = $BIKE_ID_TO_RETURN AND date_returned IS NULL")

        # if input not rented
        if [[ -z $RENTAL_ID ]]
        then
          # send to main menu
          MAIN_MENU "You do not have that bike rented."
        else
          # update date_returned
          RETURN_BIKE_RESULT=$($PSQL "UPDATE rentals SET date_returned = NOW() WHERE rental_id = $RENTAL_ID")
          
          # set bike availability to true
          SET_TO_TRUE_RESULT=$($PSQL "UPDATE bikes SET available = true WHERE bike_id = $BIKE_ID_TO_RETURN")
          
          # send to main menu
          MAIN_MENU "Thank you for returning your bike."
        fi
      fi
    fi
  fi
}

EXIT() {
  echo -e "\nThank you for stopping in.\n"
}

MAIN_MENU
```
