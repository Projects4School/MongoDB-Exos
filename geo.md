1) ```js
    var KilometresEnRadians = function(kilometres){ 
        var rayonTerrestreEnKm = 6371; 
        return kilometres / rayonTerrestreEnKm; 
    }; 
    
    var salle = db.salles.findOne({"adresse.ville": "Nîmes"}); 
        
    db.salles.find(
        {
            $and: [
                {
                    styles: {
                        $in: ["blues", "soul"]
                    },
                },
                {
                    "adresse.localisation": {
                        $geoWithin: {
                            $centerSphere: [
                                salle.adresse.localisation.coordinates,
                                KilometresEnRadians(60)
                            ]
                        }
                    }
                }
            ]
        },
        {
            _id: 0,
            nom: 1
        }
    )

2) ```js
    var marseille = {"type": "Point", "coordinates": [43.300000, 5.400000]} 
    
    db.salles.find(
        {
            "adresse.localisation": {
                $nearSphere: {
                    $geometry: marseille,
                    $maxDistance: 100000
                }
            }
        },
        {
            _id: 0,
            ville: "$adresse.ville"
        }
    )
    ```

3) ```js
    var polygone = { 
        "type": "Polygon", 
        "coordinates": [ 
            [ 
                [43.94899, 4.80908], 
                [43.95292, 4.80929], 
                [43.95174, 4.8056], 
                [43.94899, 4.80908] 
            ] 
        ] 
    }

    db.salles.find(
        {
            "adresse.localisation": {
                $geoWithin: {
                    $geometry: polygone
                }
            }
        }, 
        {
            _id: 0, 
            nom: 1
        }
    );