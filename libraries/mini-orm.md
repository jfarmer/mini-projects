# Mini-ORM

A common tool when interacting with a database is an [object-relational mapper](https://en.wikipedia.org/wiki/Object-relational_mapping) or ORM.

This project assumes you're comfortable with basic SQL and know how to interact with a SQL database.

Popular ORMs include:

- [Sequelize](http://docs.sequelizejs.com/) (JavaScript)
- [TypeORM](https://typeorm.io/#/) (TypeScript)
- [ActiveRecord](https://guides.rubyonrails.org/active_record_basics.html) (Ruby)
- [SQLAlchemy](https://www.sqlalchemy.org/) (Python)
- [Hibernate](http://hibernate.org/orm/) (Java)
- [Doctrine](https://www.doctrine-project.org/) (PHP)

The idea is that rather than write code like this:

```javascript
const sqlite3 = require('sqlite3');

let db = new sqlite3.Database('sample.db')
db.run('INSERT INTO users(name, age) VALUES (?, ?)', ['Jesse', 35]);
db.run('UPDATE users SET age = ? WHERE name = ?', [36, 'Jesse']);
db.close();
```

We can write code like this:

```javascript
const user = User.create({name: 'Jesse', age: 35});
user.setAttribute('age', 36);
user.save();
```

Every table in the database will have a corresponding class in our application and every row will be an instance of that class.  For example, if we have a `users` table we will have a `User` class and each row in the `users` table will be an instance of the `User` class.

Let's write a miniature version of this ourselves.

## Iterations

### Users Table

Using SQLite3, create a database with a table called `users` with a primary key `id`.  Add some fields like `first_name`, `last_name`, and `email`.

Create a class called `User` that supports the following behavior:

- `User.find` that returns the first matching row, e.g., `User.find(id: 12)` returns the object representing the row in the `users` table whose `id` field is `12`.
- `User.findAll` that returns all users matching the conditions given, e.g., `User.findAll({first_name: 'Maria'})` returns all users whose first name is Maria.
- Methods to get and set attributes on an instance
- Methods to save a record to the database

### Groups Table

Let's say a user can belong to a group.  Create a `groups` table with fields `id` and `name`.  Add a `group_id` field to the `users` table, which specifies which group a user belongs to.

Create a `Group` class that behaves like the `User` class above.

### Refactor Out a Base Class

The `User` and `Group` class share a lot of code.  Create a base class called `DatabaseModel` and make `User` and `Group` inherit from it.  Factor out the above methods into the `DatabaseModel` class.  Modify `User` and `Group` so that they only contain the user-specific and group-specific information necessary for `DatabaseModel` to do its work.

For example, the `User` model knows that a its associated with the `users` table and that a user's attributes are `id`, `first_name`, `last_name`, and `email`.  The `DatabaseModel` class needs to know what table and attributes a subclass is concerned with to create the necessary SQL.
