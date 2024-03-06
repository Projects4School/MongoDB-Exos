```js
db.achats.aggregate([
    {
        $match: {
            achats: { $exists: true },
            reductions: { $exists: true }
        }
    },
    {
        $addFields: {
            total: {
                $round: {
                    $subtract: [
                        { $sum: "$achats" },
                        { $sum: "$reductions" }
                    ]
                }
            }
        }
    },
    {
        $project: {
            _id: 0,
            nom: 1,
            total: 1
        }
    }
])