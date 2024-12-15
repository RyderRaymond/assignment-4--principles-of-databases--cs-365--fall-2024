# Fall 2024 Principles of Databases — Assignment 4

* **Do not start this project until you’ve read and understood these instructions. If something is not clear, ask.**

---

## ❖ Introduction ❖

For this assignment, you will write responses to nine questions based on different topics from our textbook, *Database Systems — The Complete Book* and to one question based on your notes. Reply to each question in the provided region using Markdown syntax.

---

## ❖ Questions ❖

### 1. [2.4] What is the difference between a Cartesian Product, a Natural Join, and Theta-Joins?

A Cartesian Product is the result of choosing each element from the first relation, and for each of these elements, pairing this element with each of the elements of the second relation. In terms of the Cartesian Product for relations with tuples, the pair is a tuple consisting of the attributes of the first tuple, and then the attributes of the second tuple, with any attributes that have the same name in both tuples being preceded by the relation's name.

A Natural Join is a Cartesian Product of the two relations, but the only tuples that remain in the result are the pairs that agree in the values of the attributes that have the same name in both relations. In other words, if attributes B, C, and D appear in both relation R and S, the natural join will be all pairs consisting of a tuple from R and a tuple from S where R.B = S.B, R.C = S.C, and R.D = S.D. Any tuples who do not match with a tuple from the other relation are left out in the result, and the attributes which are common to both relations are listed only once in the result.

A Theta-Join is similar to a Natural Join, but the condition for pairing is not just agreement on the common attributes, but instead can be specified as any condition. The actual underlying operation is first the Cartesian Product of two relations, and secondly the selection of only the resulting pairs that satisfy the stated condition.

### 2. [2.5] What is a Referential Integrity Constraint?

A Referential Integrity Constraint is a constraint that states that some value in one situation must appear as a value in another situation. In terms of relations, a Referential Integrity Constraint means that we can require that if a value appears in an attribute of one relation's tuples, this value must also appear in an attribute of another relation's tuples. For instance, if attribute A of relation R has referential integrity for attribute B of relation S, this expects that for each tuple from R, there must be a tuple in S where R.A = S.B. This is useful for situations where one tuple will rely on the existence of another tuple in another relation, such as a president requiring that the country they are the president of actually exists. Referenital Integrity Constraints are often used with Key Constraints to specify that one and only one tuple from each relation are being related by a relationship.

###  3. [2.5] What is a Key Constraint?

A Key Constraint is the requirement that no two tuples in a relation have the same values for all attributes of the key. In other words, for some relation, if a key is placed on attributes A and B, there must be no two tuples T1 and T2 where T1.A = T2.A and T1.B = T2.B. However, tuples may agree on attributes in the key, so long as there is at least one attribute that the two tuples do not agree on. Key Constraints are useful to ensure the ability to uniquely identify all tuples in the relation. Another relation may also contain attributes that are the key attributes of this relation, which is a way of creating a relationship between the two relations.

### 4. [4.1] What is an Entity/Relationship Model? What purpose does it serve in the process of creating/designing databases?

An Entity/Relationship Model is a model whereby the schema of a database is represented graphically as an entity-relationship diagram. It uses entity sets, attributes, and relationships to portray the schema. Entity sets are displayed as rectangles, and represent a collection of entities that follow the same schema. Entities are some form of object that may exist in the database. From an object-oriented viewpoint, an entity set is like a class for entities. Attributes are like the properties or fields of entities in an entity set, and may be primitive types or compound types like structs from C. Attributes are denoted with an oval. Relationships are the connection between two or more entity sets. This connects the entities of one set to the entities of another entity set, or even more entity sets. The relationship also denotes multiplicity, such as many-many, many-one, one-one. Relationships also denote other constraints, such as Key Constraints and Referential Integrity. Relationships are denoted with a diamond, and may also have associated attributes.

The purpose of an E/R Diagram in creating or designing a database is that it is useful as a visual aid to see how the components of the database will interact. It shows how data will be represented, and physically shows relationships between data using a connecting line, which is not as easily seen in the lines of code of the final database schema. It is also much easier to draw an E/R diagram to fully design the database in an abstract model, than to actually program the database. This allows for prototyping the database, and for ease of modification before implementing the database.

### 5. [4.4] What is a Weak Entity Set?

A Weak Entity Set is an entity set whose key partially or entirely belongs to another entity set, named the supporting entity set. This means that an entity from the weak entity set may not be unique until related to an entity in the supporting entity set. It also means that an entity in the weak entity set relies on the existence of an entity in the supporting entity set. In the E/R diagram, a weak entity set is denoted by a rectangle with a double border, and between it and the supporting entity set is a relationship with a double border diamond.

### 6. [5.2.7; 6.3.8] Explain the concepts of Outerjoin, Natural Right Outer Joins, Natural Left Outer Joins, and Full Outer Joins.

An Outer Join is a Join in which the tuples of one relation which do not match with any tuple of the other relation have the missing attributes padded with NULL or some other filler value. These tuples which do not match are called dangling tuples. The meaning of "match" in this is that the tuple did not satisfy the condition of the join when paired with any other tuple from the other relation. Outer joins may be specified as natural joins, or just as joins "on" a particular condition.

A Natural Right Outer Join is a natural join, but only tuples of the relation right of the join operator that do not match with any other tuple have the missing attributes padded with NULL and are added to the result.

A Natural Left Outer Join is a natural join, but only tuples of the relation left of the join operator that do not match with any other tuple have the missing attributes padded with NULL and are added to the result.

A Full Outer Join is a join, but both tuples of the left relation and of the right relation that do not match with any other tuple have the missing attributes padded with NULL and are added to the result. Because this is not specified as natural or not, the meaning of "match" is that the tuple did not satisfy the condition of the join with any other tuple. If this is a natural join, the condition is the same as a regular natural join, being the agreement of the values of the shared attributes.

### 7. [6.6.3] What is the difference between the SQL command `TRANSACTION` and the execution of any statement in SQL?

The difference between the SQL command 'TRANSACTION' and the execution of any statement in SQL is that any statement by default is a transaction, but the 'TRANSACTION' command allows us to group several statements together to become one single transaction. This means that all statements in the transaction must execute atomically and serially together, as if performed as a single transaction, rather than atomically and serially by themselves. The advantage is the ability to state that a sequence of statements must execute and complete from start to finish, or else have none of them execute at all, and that no statements in the sequence can overlap their execution (ensuring serializability). Without the 'TRANSACTION' command, there could be a situation where in a sequence of statements, one statement may fail but the rest continue to execute, resulting in an incorrect outcome.

### 8. [8] What is a Virtual View and what are its advantages?

A Virtual View is a relation that is defined through a query over other relations. These are not stored as regular tables, but rather their definition is stored, and the query processor replaces the name of the view with its definition whenever the view is mentioned in a query. This is equivalent to replacing the view's name with a subquery that is its definition. Once defined, views may be queried just like any table, and if the view is updatable, it may be used to modify the underlying table.

The advantage of a view is that it provides a level of abstraction, similar to functions in most programming languages. In other words, if there is a particular query that is performed very often, rather than retyping the query many times, a view could be made with the query as the definition, and the view could be used instead of the query. Additionally, a view could be defined as the join of two tables, and then queried as if it were one table, simplifying queries that use the two tables. It could also be defined as a subset of a table, such as only movies produced by a particular studio.

### 9. [8.3] What is an *index* and what are its advantages?

An index is a data structure that makes it fast to find tuples that have particular values for the attributes in the index. Specifically, an index is stored as a binary search tree of (key, value) pairs, where the key is a value that the index attribute could store, and the value is the set of locations for tuples that have this value in the index attribute. Indexes are placed on the most queried attributes, which are often the key, or an attribute which is unique or almost unique.

The advantage is that if a query involves checking if the index attribute is equal to some value, the DBMS immediately knows the locations of the tuples it needs, rather than having to scan all tuples of this relation to see if it has that value for this attribute. For instance, if there is a relation "Movies", with an index on the attribute "title", then a query searching for all Movies with title "King Kong" would be very fast, as the DBMS would find the (key, value) pair with the key of "King Kong", and immediately know the tuples it needs.

The disadvantage is that if the index attribute is updated, or a tuple is inserted or deleted, it takes extra disk operations to update the data structures of the index.

### 10. Explain the concept of an MVC, or model, view, controller, framework for designing full stack applications

An MVC framework is a way of ensuring the separation of key components of full stack applications. The components for the MVC are the model, view, and controller.

The model is the stored data for the application, including the database system that manages it. The model is not openly visible to the user, but is instead hidden by the controller. The database serves data to the controller when requested. Common DBMS's for this include MariaDB, MySQL, SQLITE, and MongoDB.

The controller sits between the model and the view. It hides the model from the user, and takes requests from the view for data, contacts the model to retrieve the data, and serves that data back to the view. The controller will also make requests to modify the data in the model. The controller may also update the view if the model changes. The controller is not visible to the end user.

The view is what the end user sees. It is usually HTML, CSS, and JavaScript. The view will send requests to the controller for data from the model. The view may also take in user input to modify the model, which it will send to the controller, or to update the way the data is represented in the view.

MVC ensures separation of tasks so that unwanted interactions are avoided, such as the user being able to interact with the database in an unwanted way.

---

## ❖ Due ❖

Sunday, 15 December 2024, at 10:00 AM.

---

## ❖ Grading ❖

| Item        | Points |
|-------------|:------:|
| Question 1  | `10`   |
| Question 2  | `10`   |
| Question 3  | `10`   |
| Question 4  | `10`   |
| Question 5  | `10`   |
| Question 6  | `10`   |
| Question 7  | `10`   |
| Question 8  | `10`   |
| Question 9  | `10`   |
| Question 10 | `10`   |

---

## ❖ Submission ❖

**NO late submissions will be accepted.**

You will need to issue a pull request back into the original repo, the one from which your fork was created for this project. See the **Issuing Pull Requests** section of [this site](http://code-warrior.github.io/tutorials/git/github/index.html) for help on how to submit your assignment.

**Note**: This assignment may **only** be submitted via GitHub. **No other form of submission will be accepted**.
