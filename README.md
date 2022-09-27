# MongoIntro


1. Insert a new blog into the collection.

db.blogs.insert([{
    "createdAt": new Date () ,
    "title": "A Song of Ice and Fire - A Game of Thrones",
    "text" : "Winter is coming. Such is the stern motto of House Stark, the northernmost of the fiefdoms that owe allegiance to King Robert Baratheon in far-off King’s Landing." ,
    "author": "George R.R. Martin ",
    "lastModified": new Date (),
    "category": ["Fantasy"]
    objectId: 11}])

2. Find one blog by author.

db.blogs.findOne({
    "author" : {$regex : "George R.R. Martin"}
    })

3. Find all blogs whose objectId is greater than 5.
db.blogs.find({objectId: {$gt: 5 }})


4.  Find all blogs whose createdAt is after April 1, 2022.
db.blogs.find({createdAt: {$gt: new Date("2022-04-01")}})

5. Find all blogs where the field lastModified does not exists.
db.blogs.updateMany({lastModified: {$exists: false}},{$set:{lastModified: new Date() }})


6. Find all blogs created after May 2022 and add "lorem" as a new category in the categories array.
db.blogs.updateMany({createdAt: {$gt: new Date("2022-05-01")}, {$addToSet: { categories: "lorem"}, $set: {lastModified: new Date()}}
})

7. Find all blogs that have the category "voluptas" and pull "voluptas" from the categories
db.blogs.updateMany({categories: {$in: ["voluptas"]}}, {$pull:{ categories: "voluptas"}, $set: {lastModified: new Date()})

8. Find all blogs with "corrupti" in the categories and delete those blogs.
db.blogs.deleteMany({ categories: {$in: ["corrupti"]} })