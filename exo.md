1) ```js
    db.salles.find(
        { 
            smac: { 
                $exists: true, 
                $eq: true 
            } 
        }, 
        {
            nom: 1
        }
    )
    ```

2) ```js
    db.salles.find(
        { 
            capacite: { 
                $gt: 1000, 
            } 
        }, 
        {
            _id: 0,
            nom: 1
        }
    )
    ```

3) ```js
    db.salles.find(
        { 
            "adresse.numero": { 
                $exists: false 
            }
        }, 
        { 
            _id: 1 
        }
    )
    ```

4) ```js
    db.salles.find(
        { 
            avis: { 
                $exists: true, 
                $size: 1 
            }
        }, 
        { 
            nom: 1
        }
    )
    ```

5) ```js
    db.salles.find(
        { 
            styles: "blues"
        }, 
        { 
            _id: 0, 
            styles: 1 
        }
    )
    ```

6) ```js
    db.salles.find(
        {
            "styles.0": "blues"
        },
        {
            _id: 0,
            styles: 1
        }
    )
    ```

7) ```js
    db.salles.find(
        {
            "adresse.codePostal": { $regex: /^84.*/ },
            capacite: { $lt: 500 }
        },
        {
            _id: 0,
            "adresse.ville": 1
        }
    )
    ```

8) ```js
    db.salles.find(
        {
            $or: [
                { _id: { $mod: [2, 0] } },
                { avis: { $exists: false } }
            ]
        },
        {
            _id: 1
        }
    )
    ```

9) ```js
    db.salles.find(
        {
            "avis.note": { $gte: 8, $lte: 10 }
        },
        {
            _id: 0,
            nom: 1
        }
    )
    ```

10) ```js
    db.salles.find(
        {
            "avis.date": { $gt: new Date("15/11/2019") }
        },
        {
            _id: 0,
            nom: 1
        }
    )
    ```

11) ```js
    db.salles.find(
        {
            $expr: {
                $gt: [
                    {$multiply: ["$_id", 100]},
					"$capacite"
                ]
            }
        },
        {
            _id: 0,
            nom: 1,
            capacite: 1
        }
    )
    ```

13) ```js
    db.salles.distinct('adresse.codePostal')
    ```

14) ```js
    db.salles.updateMany(
        {},
        { $inc: { capacite: 100 } }
    )
    ````

15) ```js
    db.salles.updateMany(
        {
            styles: {
                $ne: "jazz"
            }
        },
        {
            $push: {
                styles: "jazz"
            }
        }
    )
    ```

16) ```js
    db.salles.updateMany(
        {
            _id: { $nin: [2,3] }
        },
        {
            $pull: {
                styles: "funk"
            }
        }
    )
    ```

17) ```js
    db.salles.updateOne(
        {
            _id: 3
        }, 
        { 
            $addToSet: { 
                styles: {
                    $each: ["techno", "reggae"] 
                } 
            }
        }
    )
    ```

18) ```js
    db.salles.updateMany(
        {
            nom: { $regex: /^P.*/i },
        },
        {
            $inc: {
                capacite: 150
            },
            $push: {
                contact: {
                    telephone: "04 11 94 00 10"
                }
            }
        }
    )

19) ```js
    db.salles.updateMany(
        {
            nom: { $regex: /[^aeiou]+$/ },
        }
    )