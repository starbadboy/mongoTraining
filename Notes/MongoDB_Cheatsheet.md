# MongoDB Command Cheat Sheet

## Connection

```bash
# Connect to local MongoDB
mongo

# Connect to remote MongoDB
mongo "mongodb://hostname:port"

# Connect with authentication
mongo "mongodb://hostname:port" --username username --password password

# Connect to MongoDB Atlas
mongo "mongodb+srv://cluster-name.mongodb.net/database" --username username
```

## Database Operations

```javascript
// Show all databases
show dbs

// Create or switch to a database
use databaseName

// Show current database
db

// Drop database
db.dropDatabase()

// Show stats
db.stats()

// Show status
db.serverStatus()
```

## Collection Operations

```javascript
// Show collections in current database
show collections

// Create collection
db.createCollection("collectionName")

// Create collection with options
db.createCollection("collectionName", {
  capped: true,
  size: 10000000,
  max: 1000
})

// Drop collection
db.collectionName.drop()
```

## CRUD Operations

### Create (Insert)

```javascript
// Insert one document
db.collectionName.insertOne({ 
  name: "John", 
  age: 30 
})

// Insert multiple documents
db.collectionName.insertMany([
  { name: "John", age: 30 },
  { name: "Jane", age: 25 }
])
```

### Read (Query)

```javascript
// Find all documents
db.collectionName.find()

// Pretty print results
db.collectionName.find().pretty()

// Find with condition
db.collectionName.find({ age: 30 })

// Find with multiple conditions (AND)
db.collectionName.find({ age: 30, name: "John" })

// Find with OR condition
db.collectionName.find({
  $or: [
    { age: 30 },
    { name: "Jane" }
  ]
})

// Find with comparison operators
db.collectionName.find({ age: { $gt: 25 } })  // greater than
db.collectionName.find({ age: { $gte: 25 } }) // greater than or equal
db.collectionName.find({ age: { $lt: 30 } })  // less than
db.collectionName.find({ age: { $lte: 30 } }) // less than or equal
db.collectionName.find({ age: { $ne: 30 } })  // not equal
db.collectionName.find({ age: { $in: [25, 30] } }) // in array
db.collectionName.find({ age: { $nin: [25, 30] } }) // not in array

// Find one document
db.collectionName.findOne({ name: "John" })

// Limit results
db.collectionName.find().limit(5)

// Skip results
db.collectionName.find().skip(5)

// Count documents
db.collectionName.countDocuments({ age: { $gt: 25 } })

// Sort results (1 for ascending, -1 for descending)
db.collectionName.find().sort({ age: 1, name: -1 })

// Projection (include only specific fields)
db.collectionName.find({}, { name: 1, age: 1, _id: 0 })
```

### Update

```javascript
// Update one document
db.collectionName.updateOne(
  { name: "John" },
  { $set: { age: 31 } }
)

// Update many documents
db.collectionName.updateMany(
  { age: { $lt: 30 } },
  { $inc: { age: 1 } }
)

// Replace entire document
db.collectionName.replaceOne(
  { name: "John" },
  { name: "John Doe", age: 31 }
)

// Upsert (insert if not exists)
db.collectionName.updateOne(
  { name: "John" },
  { $set: { age: 31 } },
  { upsert: true }
)

// Update operators
$set     // Set field value
$unset   // Remove field
$inc     // Increment field value
$mul     // Multiply field value
$min     // Update if new value is less than current
$max     // Update if new value is greater than current
$rename  // Rename field
$push    // Add element to array
$pop     // Remove first (-1) or last (1) element from array
$pull    // Remove elements from array that match condition
$addToSet // Add element to array if not exists
```

### Delete

```javascript
// Delete one document
db.collectionName.deleteOne({ name: "John" })

// Delete many documents
db.collectionName.deleteMany({ age: { $lt: 25 } })

// Delete all documents
db.collectionName.deleteMany({})
```

## Indexes

```javascript
// Create single field index
db.collectionName.createIndex({ field: 1 }) // 1 for ascending, -1 for descending

// Create compound index
db.collectionName.createIndex({ field1: 1, field2: -1 })

// Create unique index
db.collectionName.createIndex({ email: 1 }, { unique: true })

// Create text index
db.collectionName.createIndex({ content: "text" })

// Create geospatial index
db.collectionName.createIndex({ location: "2dsphere" })

// Create TTL index (documents expire after 3600 seconds)
db.collectionName.createIndex({ createdAt: 1 }, { expireAfterSeconds: 3600 })

// List all indexes
db.collectionName.getIndexes()

// Drop index
db.collectionName.dropIndex({ field: 1 })

// Drop all indexes
db.collectionName.dropIndexes()
```

## Aggregation

```javascript
// Basic aggregation pipeline
db.collectionName.aggregate([
  { $match: { age: { $gt: 25 } } },
  { $group: { _id: "$city", count: { $sum: 1 } } },
  { $sort: { count: -1 } }
])

// Common aggregation operators
$match   // Filter documents
$group   // Group documents
$project // Reshape documents
$sort    // Sort documents
$limit   // Limit results
$skip    // Skip results
$unwind  // Deconstruct array field
$lookup  // Join with another collection

// Example: Calculate average age by city
db.collectionName.aggregate([
  { $group: { 
      _id: "$city", 
      avgAge: { $avg: "$age" }, 
      count: { $sum: 1 } 
    } 
  },
  { $sort: { avgAge: -1 } }
])

// Example: Join collections
db.orders.aggregate([
  { $lookup: {
      from: "customers",
      localField: "customerId",
      foreignField: "_id",
      as: "customerDetails"
    }
  }
])
```

## Performance Analysis

```javascript
// Explain query plan
db.collectionName.find({ age: { $gt: 25 } }).explain()

// Detailed execution stats
db.collectionName.find({ age: { $gt: 25 } }).explain("executionStats")

// All plans execution
db.collectionName.find({ age: { $gt: 25 } }).explain("allPlansExecution")

// Index usage stats
db.collectionName.aggregate([{ $indexStats: {} }])

// Collection stats
db.collectionName.stats()

// Current operations
db.currentOp()

// Kill operation
db.killOp(opId)

// Set profiling level
db.setProfilingLevel(1, { slowms: 100 }) // Profile queries slower than 100ms

// View profiling data
db.system.profile.find().sort({ ts: -1 }).limit(10)
```

## MongoDB Atlas Search

```javascript
// Basic text search
db.collectionName.aggregate([
  {
    $search: {
      "text": {
        "query": "mongodb",
        "path": "description"
      }
    }
  }
])

// Fuzzy search
db.collectionName.aggregate([
  {
    $search: {
      "text": {
        "query": "monggodb",
        "path": "description",
        "fuzzy": {
          "maxEdits": 1
        }
      }
    }
  }
])

// Vector search
db.collectionName.aggregate([
  {
    $vectorSearch: {
      "index": "vector_index",
      "path": "embedding",
      "queryVector": [0.1, 0.2, ..., 0.7],
      "numCandidates": 100,
      "limit": 10
    }
  }
])
```

## MongoDB Monitoring Tools

```bash
# Monitor read/write activity by collection
mongotop --host mongodb://localhost:27017 5

# Monitor MongoDB server statistics
mongostat --host mongodb://localhost:27017 5
``` 