- `db.employees.find()`

- `db.employees.find({ "age": {$gt: 33} })`

- `db.employees.find().sort({ "salary": -1 })`

- ```js
    db.employees.find(
        {}, 
        { 
            "_id": 0, 
            "name": 1, 
            "job": 1 
        }
    )
    ````

- ```js
    db.employees.aggregate( [
        {
            $group: {
                _id: "$job",
                employees: {
                    $count: {}
                }
            }
        }
    ] )
    ```
    
- ```js
    db.employees.updateMany(
        { job: { $eq: "Developer" } },
        { $set: { "salary" : 80000 } }
    )
    ```