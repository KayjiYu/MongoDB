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

// datatype
db.students.insertOne({
  name: "Larry",
  age: 32,
  gpa: 2.8,
  fullTime: false,
  registerDate: new Date(),
  graduationDate: null,
  courses: ["Biology", "Chemistry", "Calculus"],
  address: {
    street: "123 Fake St.",
    city: "Bikini Bottom",
    zip: 12345,
  },
});
```

Sorting and limiting

```js
// ascending
db.students.find().sort({ name: 1 });

// decending
db.students.find().sort({ gpa: -1 });

// limiting
db.students.find().limit(3);

// sorting and limiting
db.students.find().sort({ gpa: -1 }).limit(1);
```

Find

```js
db.students.find({ gpa: 4.0, fullTime: false });

// projection
db.students.find({}, { name: true });

db.students.find({}, { _id: false, name: true, gpa: true });
```

Update

```js
//update One
db.students.updateOne({ name: "Spongebob" }, { $set: { fullTime: true } });

// use objectid to avoid duplicate names
db.students.updateOne(
  { _id: ObjectId("66dfd7d25ba05334195e739c") },
  { $set: { fullTime: false } },
);

// remove
db.students.updateOne(
  { _id: ObjectId("66dfd7d25ba05334195e739c") },
  { $unset: { fullTime: "" } },
);

// Update Many
db.students.updateMany({}, { $set: { fullTime: false } });

db.students.updateMany(
  { fullTime: { $exists: true } },
  { $set: { fullTime: true } },
);
```

Export

```js
exit;
```

```bash
cd MongoDB_Resources

# mongoexport
mongoexport --collection=students --db=school --out=students.json

# open json
cat students.json
```

Delete

```js
db.students.deleteOne({ name: "Larry" });

db.students.deleteMany({ fullTime: false });

db.students.deleteMany({ registerDate: { $exists: false } });
```

Import

```js
exit;
```

```bash
cd MongoDB_Resources
mongoimport --collection=students --db=school --type=json student.json
mongosh
```

```js
show dbs
use school
show collections
db.students.find()
```

Comparison

```js
// not equal
db.students.find({ name: { $ne: "Spongebob" } });

// less than (equal)
db.students.find({ age: { $lte: 27 } });

// greater than
db.students.find({ age: { $gte: 20 } });

// between
db.students.find({ gpa: { $gte: 3, $lte: 4 } });

// in array
db.students.find({ name: { $in: ["Spongebob", "Patrick", "Sandy"] } });

// not in array
db.students.find({ name: { $nin: ["Spongebob", "Patrick", "Sandy"] } });
```

Logical Operator

```js
// and
db.students.find({ $and: [{ fullTime: true }, { age: { $lte: 22 } }] });

// or
db.students.find({ $or: [{ fullTime: true }, { age: { $lte: 22 } }] });

// nor
db.students.find({ $nor: [{ fullTime: true }, { age: { $lte: 22 } }] });

// not
db.students.find({ age: { $not: { $gte: 30 } } });
```
