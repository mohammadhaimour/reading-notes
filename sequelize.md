## sequelize-normalization:

- Sequelize supports the standard associations: One-To-One, One-To-Many, and Many-To-Many.

- Sequelize provides four types of associations that should be combined to create them:

  1. The HasOne association
  2. The BelongsTo association
  3. The HasMany association
  4. The BelongsToMany association.


### One-To-One relationships:



The main setup to achieve the goal is as follows:
```js
Foo.hasOne(Bar);
Bar.belongsTo(Foo);
```

Since no option was passed, Sequelize will infer what to do from the names of the models. In this case, Sequelize knows that a fooId column must be added to Bar.

This way, calling Bar.sync() after the above will yield the following SQL (on PostgreSQL, for example):

```js
CREATE TABLE IF NOT EXISTS "foos" (
  /* ... */
);
CREATE TABLE IF NOT EXISTS "bars" (
  /* ... */
  "fooId" INTEGER REFERENCES "foos" ("id") ON DELETE SET NULL ON UPDATE CASCADE
  /* ... */
);

```
 ### Customizing the foreign key:

 - Both the hasOne and belongsTo calls shown above will infer that the foreign key to be created should be called fooId. To use a different name, such as myFooId:

 ```js
 // Option 1
Foo.hasOne(Bar, {
  foreignKey: 'myFooId'
});
Bar.belongsTo(Foo);

// Option 2
Foo.hasOne(Bar, {
  foreignKey: {
    name: 'myFooId'
  }
});
Bar.belongsTo(Foo);

// Option 3
Foo.hasOne(Bar);
Bar.belongsTo(Foo, {
  foreignKey: 'myFooId'
});

// Option 4
Foo.hasOne(Bar);
Bar.belongsTo(Foo, {
  foreignKey: {
    name: 'myFooId'
  }
});
 
 ```
For example, to use UUID as the foreign key data type instead of the default (INTEGER), you can simply do:
```js
const { DataTypes } = require("Sequelize");

Foo.hasOne(Bar, {
  foreignKey: {
    // name: 'myFooId'
    type: DataTypes.UUID
  }
});
Bar.belongsTo(Foo);
```

- Mandatory versus optional associations:
```js
Foo.hasOne(Bar, {
  foreignKey: {
    allowNull: false
  }
});
// "fooId" INTEGER NOT NULL REFERENCES "foos" ("id") ON DELETE RESTRICT ON UPDATE RESTRICT
```

## One-To-Many relationships:

- One-To-Many associations are connecting one source with multiple targets, while all these targets are connected only with this single source.
This means that, unlike the One-To-One association, in which we had to choose where the foreign key would be placed, there is only one option in One-To-Many associations.

- Implementation

  The main way to do this is as follows:
```js
Team.hasMany(Player);
Player.belongsTo(Team);
```



For example, in PostgreSQL, the above setup will yield the following SQL upon sync():
```js
CREATE TABLE IF NOT EXISTS "Teams" (
  /* ... */
);
CREATE TABLE IF NOT EXISTS "Players" (
  /* ... */
  "TeamId" INTEGER REFERENCES "Teams" ("id") ON DELETE SET NULL ON UPDATE CASCADE,
  /* ... */
);
```

### Many-To-Many relationships:

- Many-To-Many associations connect one source with multiple targets, while all these targets can in turn be connected to other sources beyond the first. This cannot be represented by adding one foreign key to one of the tables, like the other relationships did. Instead, the concept of a Junction Model is used. This will be an extra model (and extra table in the database) which will have two foreign key columns and will keep track of the associations. The junction table is also sometimes called join table or through table.

- Implementation

  The main way to do this in Sequelize is as follows:

  ```js
  const Movie = sequelize.define('Movie', { name: DataTypes.STRING });
   const Actor = sequelize.define('Actor', { name: DataTypes.STRING });
  Movie.belongsToMany(Actor, { through: 'ActorMovies' });
  Actor.belongsToMany(Movie, { through: 'ActorMovies' });

  ```

  Since a string was given in the through option of the belongsToMany call, Sequelize will automatically create the ActorMovies model which will act as the junction model. For example, in PostgreSQL:
```js
 CREATE TABLE IF NOT EXISTS "ActorMovies" (
  "createdAt" TIMESTAMP WITH TIME ZONE NOT NULL,
  "updatedAt" TIMESTAMP WITH TIME ZONE NOT NULL,
  "MovieId" INTEGER REFERENCES "Movies" ("id") ON DELETE CASCADE ON UPDATE CASCADE,
  "ActorId" INTEGER REFERENCES "Actors" ("id") ON DELETE CASCADE ON UPDATE CASCADE,
  PRIMARY KEY ("MovieId","ActorId")
);
```

   Instead of a string, passing a model directly is also supported, and in that case the given model will be used as the junction model (and no model will be created automatically). For example:

```js
const Movie = sequelize.define('Movie', { name: DataTypes.STRING });
const Actor = sequelize.define('Actor', { name: DataTypes.STRING });
const ActorMovies = sequelize.define('ActorMovies', {
  MovieId: {
    type: DataTypes.INTEGER,
    references: {
      model: Movie, // 'Movies' would also work
      key: 'id'
    }
  },
  ActorId: {
    type: DataTypes.INTEGER,
    references: {
      model: Actor, // 'Actors' would also work
      key: 'id'
    }
  }
});
Movie.belongsToMany(Actor, { through: ActorMovies });
Actor.belongsToMany(Movie, { through: ActorMovies });

```

  The above yields the following SQL in PostgreSQL, which is equivalent to the one shown above:
```js
 CREATE TABLE IF NOT EXISTS "ActorMovies" (
  "MovieId" INTEGER NOT NULL REFERENCES "Movies" ("id") ON DELETE RESTRICT ON UPDATE CASCADE,
  "ActorId" INTEGER NOT NULL REFERENCES "Actors" ("id") ON DELETE RESTRICT ON UPDATE CASCADE,
  "createdAt" TIMESTAMP WITH TIME ZONE NOT NULL,
  "updatedAt" TIMESTAMP WITH TIME ZONE NOT NULL,
  UNIQUE ("MovieId", "ActorId"),     -- Note: Sequelize generated this UNIQUE constraint but
  PRIMARY KEY ("MovieId","ActorId")  -- it is irrelevant since it's also a PRIMARY KEY
);
```


