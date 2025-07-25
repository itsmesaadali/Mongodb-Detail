
# 📘 MongoDB Operators Cheat Sheet

## 📂 Table of Contents
- [1. MongoDB Query Operators](#1-mongodb-query-operators)
- [2. MongoDB Update Operators](#2-mongodb-update-operators)
- [3. MongoDB Aggregation Operators](#3-mongodb-aggregation-operators)
- [4. MongoDB `$expr` Operator](#4-mongodb-expr-operator)
- [5. Advantages of MongoDB Operators](#5-advantages-of-mongodb-operators)
- [6. Disadvantages](#6-disadvantages)
- [7. Real-World Use Cases](#7-real-world-use-cases)

---

## 1. 📌 MongoDB Query Operators

Used to **filter documents** based on conditions in `.find()`, `$match`, etc.

### 🔍 Comparison Operators
| Operator | Description                            | Example                            |
|---------|----------------------------------------|------------------------------------|
| `$eq`   | Equal to                               | `{ age: { $eq: 25 } }`             |
| `$ne`   | Not equal to                           | `{ status: { $ne: "pending" } }`   |
| `$gt`   | Greater than                           | `{ price: { $gt: 100 } }`          |
| `$gte`  | Greater than or equal to               | `{ price: { $gte: 50 } }`          |
| `$lt`   | Less than                              | `{ quantity: { $lt: 20 } }`        |
| `$lte`  | Less than or equal to                  | `{ quantity: { $lte: 100 } }`      |

### 📘 Logical Operators
| Operator | Description                             |
|---------|-----------------------------------------|
| `$and`  | Matches documents that satisfy all conditions |
| `$or`   | Matches documents that satisfy any condition |
| `$not`  | Inverts a condition                     |
| `$nor`  | Matches documents that fail all conditions |

### 🧮 Element Operators
| Operator     | Description                           |
|--------------|----------------------------------------|
| `$exists`    | Checks if a field exists               |
| `$type`      | Checks the BSON data type of a field   |

### 📚 Array Operators
| Operator     | Description                                   |
|--------------|-----------------------------------------------|
| `$all`       | Matches arrays that contain all specified values |
| `$size`      | Matches arrays of a specified length          |
| `$elemMatch` | Matches documents that contain array elements matching specified conditions |

---

## 2. 🛠️ MongoDB Update Operators

Used with `.updateOne()`, `.updateMany()`, or `$set` in aggregation.

### 🔄 Field Operators
| Operator | Description                          |
|----------|--------------------------------------|
| `$set`   | Sets the value of a field            |
| `$unset` | Removes a field                      |
| `$inc`   | Increments a numeric field           |
| `$mul`   | Multiplies a numeric field           |
| `$rename`| Renames a field                      |

### 📅 Date Operators
| Operator  | Description                                 |
|-----------|---------------------------------------------|
| `$currentDate` | Sets the value of a field to current date |

### 🧰 Array Update Operators
| Operator     | Description                               |
|--------------|--------------------------------------------|
| `$push`      | Appends a value to an array                |
| `$pop`       | Removes first or last element from array   |
| `$pull`      | Removes elements that match a condition    |
| `$addToSet`  | Adds a value only if it doesn’t exist      |

---

## 3. 🔄 MongoDB Aggregation Operators

Used within the **aggregation pipeline** to transform or compute data.

### 🏗️ Pipeline Stages
| Stage         | Purpose                                    |
|---------------|--------------------------------------------|
| `$match`      | Filters documents                          |
| `$group`      | Groups by specified key                    |
| `$project`    | Selects or transforms fields               |
| `$sort`       | Sorts the result                          |
| `$limit`      | Limits the number of results               |
| `$skip`       | Skips the first N documents                |
| `$lookup`     | Joins documents from another collection    |
| `$unwind`     | Deconstructs an array                      |

### 🧠 Expression Operators
| Type         | Examples                                |
|--------------|-----------------------------------------|
| Arithmetic   | `$add`, `$subtract`, `$multiply`, `$divide`, `$mod` |
| Comparison   | `$eq`, `$gt`, `$lt`, `$gte`, `$lte`, `$ne`           |
| String       | `$concat`, `$toLower`, `$toUpper`, `$substr`        |
| Array        | `$size`, `$in`, `$indexOfArray`, `$filter`          |
| Conditional  | `$cond`, `$ifNull`, `$switch`                       |
| Date         | `$year`, `$month`, `$dayOfWeek`, `$dateDiff`       |

---

## 4. 🧩 MongoDB `$expr` Operator

Allows the use of **aggregation expressions inside query** clauses like `.find()` or `$match`.

### ✅ Example: Compare Two Fields

```js
db.orders.find({
  $expr: {
    $gt: ["$totalPrice", "$discount"]
  }
})
```

### ✅ Example: Conditional Logic in Query

```js
db.users.find({
  $expr: {
    $cond: [
      { $gt: ["$age", 18] },
      true,
      false
    ]
  }
})
```

---

## 5. ✅ Advantages of MongoDB Operators

- **Flexibility**: You can build complex queries and transformations.
- **Aggregation Power**: Can analyze large datasets on the database side.
- **Rich Query Language**: Combines both simple and complex filters.
- **NoSQL Friendly**: Ideal for semi-structured or nested data.
- **Real-Time Data Processing**: Can calculate values on the fly using `$expr` and aggregation stages.

---

## 6. ⚠️ Disadvantages

- ❌ **Performance Overhead**: Complex operators like `$expr`, `$lookup`, and `$unwind` can impact performance.
- ❌ **Index Limitations**: Aggregation expressions and `$expr` can **bypass indexes**, leading to slower queries.
- ❌ **Learning Curve**: Aggregation framework is more complex than simple CRUD.
- ❌ **Less Transparent Execution Plan**: Sometimes hard to debug slow queries without using `.explain()`.

---

## 7. 🌐 Real-World Use Cases

| Use Case | Description |
|----------|-------------|
| E-Commerce | Use `$expr` to check if stock < threshold |
| Analytics | Use `$group` and `$sum` to aggregate sales |
| Social Media | Use `$lookup` to join users with posts |
| Date-Based Queries | Use `$dateDiff` to find overdue tasks |
| Inventory | Use `$cond` to mark items as "low stock" |

---

### 📎 Tip:
Use `.explain("executionStats")` to check how MongoDB is using indexes and optimizing your queries.


## 5. ✅ Advantages of MongoDB Operators

- **Flexibility**: You can build complex queries and transformations.
- **Aggregation Power**: Can analyze large datasets on the database side.
- **Rich Query Language**: Combines both simple and complex filters.
- **NoSQL Friendly**: Ideal for semi-structured or nested data.
- **Real-Time Data Processing**: Can calculate values on the fly using `$expr` and aggregation stages.

---

## 6. ⚠️ Disadvantages

- ❌ **Performance Overhead**: Complex operators like `$expr`, `$lookup`, and `$unwind` can impact performance.
- ❌ **Index Limitations**: Aggregation expressions and `$expr` can bypass indexes, leading to slower queries.
- ❌ **Learning Curve**: Aggregation framework is more complex than simple CRUD.
- ❌ **Less Transparent Execution Plan**: Sometimes hard to debug slow queries without using `.explain()`.

---

## 7. 🌐 Real-World Use Cases

| Use Case           | Description                                      |
|--------------------|--------------------------------------------------|
| E-Commerce         | Use `$expr` to check if stock < threshold        |
| Analytics          | Use `$group` and `$sum` to aggregate sales       |
| Social Media       | Use `$lookup` to join users with posts           |
| Date-Based Queries | Use `$dateDiff` to find overdue tasks            |
| Inventory          | Use `$cond` to mark items as "low stock"         |


---
