1) ```js
    var pipeline = [
        {
            $match: {
                capacite: { $gt: 50 },
            }
        },
        {
            $addFields: {
                grande: {
                    $cond: {
                        if: {
                            $gt: ["$capacite", 1000]
                        },
                        then: true,
                        else: false
                    }
                }
            }
        },
        {
            $project: {
                _id: 0,
                nom: 1,
                grande: 1
            }
        }
    ]

    db.salles.aggregate(pipeline)
    ````

2) ```js
    var pipeline = [
        {
            $addFields: {
                apres_extension: {
                    $sum: ["$capacite", 100]
                },
                avant_extension: "$capacite"
            }
        },
        {
            $project: {
                _id: 0,
                nom: 1,
                avant_extension: 1,
                apres_extension: 1
            }
        }
    ]

    db.salles.aggregate(pipeline)
    ```

3) ```js
    var pipeline = [
        {
            $project: {
                departement: {
                    $substrBytes: ["$adresse.codePostal", 0, 2]
                },
                capacite: 1
            }
        },
        {
            $group: {
                departement: "$departement",
                capaciteTotale: {
                    $sum: "$capacite"
                }
            }
        }
    ]

    db.salles.aggregate(pipeline)
    ```

4) ```js
    var pipeline = [
        {
            $unwind: "$styles"
        },
        {
            $group: {
                style: "$styles",
                nombreDeSalles: {
                    $sum: 1
                }
            }
        },
        {
            $sort: {
                _id: 1
            }
        }
    ]

    db.salles.aggregate(pipeline)
    ```

5) ```js
    var pipeline = [
        {
            $bucket: {
                groupBy: "$capacite",
                boundaries: [100, 500, 5000],
                output: {
                    nombreDeSalles: { $sum: 1 }
                }
            }
        }
    ]

    db.salles.aggregate(pipeline)
    ```

6) ```js
    var pipeline = [
        {
            $match: {
                avis: { $exists: true }
            }
        },
        {
            $project: {
                nom: 1,
                avis_excellents: {
                    $filter: {
                        input: "$avis",
                        as: "item",
                        cond: { $eq: ["$$item.note", 10] }
                    }
                }
            }
        }
    ]

    db.salles.aggregate(pipeline)