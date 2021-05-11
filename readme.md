# Mongo db commands

## Show databases

```
show dbs
```

---

## To delete database

```
use database name

db.dropDatabase()
```

---

## To create new database

```
use database name
```

---

## To check in which database we are

```
db
```

---

## To create collection

```
db.createCollection('collection name')
```

---

## To see collection

```
show collections
```

---

## Add document, row in collection (Insert)

```
db.name.insert({
    name:'mario',
    address:'paragraph',
    city:'toronto',
    age:3,
    tags:['cricket','football'],
    user:{
    name:'mario',
    status:'author',
    },
    date: Date()
})
```

---

## Add Multiple rows (Insert Multiple)

```
db.name.insertMany([
    {
    name:'max',
    address:'paragraph',
    city:'toronto',
    age:30,
    tags:['cricket','football'],
    date: Date()
    },
    {
    name:'jonas',
    address:'paragraph',
    city:'toronto',
    age:27,
    tags:['cricket','football'],
    date: Date()
    },
    {
    name:'angela',
    address:'paragraph',
    city:'toronto',
    age:25,
    tags:['barbies','soccer'],
    date: Date()
    }
])
```

---

## Find / Query data

```
db.name.find()


/*formatted output*/

db.name.find().pretty()
```

---

## Find / Query specific data

```
db.name.find({age:25})

//return the collection match with condition
```

---

## Sort ascending

```
db.info.find().sort({age:1})
```

---

## Sort descending

```
db.info.find().sort({age:-1})
```

---

## Count

```
db.info.find({tags:"cricket"}).count()

//returns number count
```

## Limit

```
db.info.find().limit(2)

//limit the search results counts
```

---

## Sort with limit

```
db.name.find().sort({age:-1}).limit(2)
```

---

## For each

```
db.name.find().forEach(function(doc){print('blog post:'+doc.name)})
```

---

## Find specific row (we can use find)

```
    db.info.findOne({name:"max"})
```

---

## Update entire row

```
db.info.update({name:"max"},
{
     "name" : "maximilian",
        "address" : "new Germany",
        "city" : "",
        "age" : 35,
        "tags" : [
                "swimming",
                "football"
        ],
        date: Date()
},{
    upsert:true
})

//upsert - if no row found it will create new one , that it is like update and also insert
```

---

## Update (replace only specific fields but keep other)

```
db.name.update({name:'jonas'},{
  $set:{
      city:"Romania",
      age:56
  }
})

$set : updates only specific fields but keep others
```

---

## Increment

```
db.name.update({name:'mario'},{
    $inc:{age:30}
})
```

---

## Rename (To rename field/key)

```
db.name.update({name:'mario'},{
    $rename:{age:"year"}
})
```

---

## Delete document

```
db.info.remove({name:'maximilian'})
```

---

## Sub Document

```
db.name.update({name:'jonas'},{
    $set:{
        comments:[
            {
                user:'yoshi',
                desc:'colleague',
                date:Date()
            },
            {
                user:'chun-li',
                desc:'colleague',
                date:Date()
            }
        ]
    }
})

//Update of a document but actually just an insert/append of a sub-document
```

---

## Find by sub-documents

```
db.name.find({
    comments:{
        $elemMatch:{
            user:'yoshi'
        }
    }
})
```

---

## Create index for Text search (serach by name here)

```
db.name.createIndex({name:'text'})


db.name.find({
    $text:{
        $search:"\"Post T\""
    }
})
```

---

## Greater than equal to

```
Greater than

db.name.find({year:{$gt:3}})


Greater than equal to

db.name.find({year:{$gte:3}})

```
## Less than equal to
```
Les than 

db.name.find({year:{$lt:3}})

Less than equal to
db.name.find({year:{$lte:3}})
```
---