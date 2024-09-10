# NoSQL

Start databse

```bash
docker run --name kj_mongo -d -p 27017:27017 mongo
docker ps
docker exec -it kj_mongo /bin/bash
mongosh
```

Create Database

```js
// switch(create) database: school
use school
```

Insert

```js
// insert one student
db.students.insertOne({ name: "Spongebob", age: 30, gpa: 3.2 });

// find
db.students.find();

// insert many
db.students.insertMany([
  { name: "Patrick", age: 38, gpa: 1.5 },
  { name: "Sandy", age: 27, gpa: 4.0 },
  { name: "Gary", age: 18, gpa: 2.5 },
]);
```
