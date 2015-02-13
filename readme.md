# Apartment lab

- Create a database called apartmentlab - create database apartmentlab;
- Using this database, create two tables, one for owners and one for properties
- Keep this relationship in mind when designing your schema:
  + **One owner can have many properties**

###Tables

- The owners table should consist of:
  + owner_id (this should be the primary key as well as a unique number that increments automatically)
  + name
  + age
- The properties table should consist of:
  + property_id (this should be the primary key as well as a unique number that increments automatically)
  + name
  + number of units
  + owner_id
    + There should also be a foreign key that references the owners table

Owners
```CREATE TABLE owners(owner_id SERIAL PRIMARY KEY, name VARCHAR(40), age INTEGER);```

Properties -
```CREATE TABLE properties(property_id SERIAL PRIMARY KEY, name VARCHAR(40), units VARCHAR(10), owner_id INTEGER NOT NULL);```

###Questions
Write down the following sql statements that are required to solve the following tasks.

```
1. Show all the tables.
  \dt
2. Show all the users.
  \du
3. Show all the data in the owners table.
  SELECT * FROM owners;
4. Show the names of all owners.
  SELECT name FROM owners;
5. Show the ages of all of the owners in ascending order.
  SELECT age FROM owners ORDER BY age ASC;
6. Show the name of any owner whose name is Donald.
  SELECT * FROM owners WHERE name = 'Donald';
7. Show the age of all owners who are older than 30.
  SELECT * FROM owners WHERE age > 30;
8. Show the name of all owners whose name starts with an E.
  SELECT * FROM owners WHERE name LIKE 'E%';
9. Add an owner named John who is 33 years old to the owners table.
  INSERT INTO owners (name, age) VALUES ('John',33);
10. Add an owner named Jane who is 43 years old to the owners table.
  INSERT INTO owners (name, age) VALUES ('Jane',43);
11. Change Jane's age to 30.
  UPDATE owners SET age = 30 where name ='Jane';
12. Change Jane's name to Janet.
  UPDATE owners SET name ='Janet' WHERE name ='Jane';
13. Add a property named Archstone that has 20 units.
  INSERT INTO properties (name,units, owner_id) VALUES ('Archstone',20,1);
14. Delete the owner named Janet.
  DELETE FROM owners WHERE name='Janet';
15. Show all of the properties in alphabetical order that are not named Archstone and do not have an id of 3 or 5.
  SELECT * FROM properties WHERE name <> 'Archstone' AND property_id NOT IN (3,5) ORDER BY name ASC;
16. Count the total number of rows in the properties table
  SELECT COUNT (*) FROM properties;
17. Show the highest age
  SELECT MAX(age) FROM owners;
18. Show the names of the first three owners in your owners table.
  SELECT * FROM owners LIMIT 3;
19. Create a foreign key that references the owner_id in the owners table and forces the constraint ON DELETE NO ACTION.
  ALTER TABLE properties ADD CONSTRAINT owner_fk FOREIGN KEY (owner_id) REFERENCES owners (owner_id) ON DELETE NO ACTION;
20. Show all of the owners and the names of the properties they own.
  SELECT owners.name, properties.name FROM owners JOIN properties ON owners.owner_id = properties.owner_id;
```

Bonus (this might require you to look up documentation online)

```
1. In the properties table change the name of the column name to property_name.
  ALTER TABLE properties RENAME COLUMN "name" TO "property_name";
2. Count the total number of properties where the owner_id is between 1 and 3.
  SELECT COUNT(*) FROM properties WHERE owner_id BETWEEN 1 AND 3;
```
