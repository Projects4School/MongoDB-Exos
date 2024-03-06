1) ```js
    db.runCommand( { collMod: "salles",
        validator: {
            $jsonSchema: {
                bsonType: "object",
                required: [ "nom", "capacite", "adresse.codePostal", "adresse.ville" ],
                properties: {
                    nom: {
                        bsonType: "string",
                    },
                    capacite: {
                        bsonType: "int",
                    },
                    "adresse.codePostal": {
                        bsonType: "string"
                    },
                    "adresse.ville": {
                        bsonType: "string"
                    }
                }
            }
        }
    } )
    ```
    Il y'a une erreur lorsqu'on execute la requête d'insersion car il manque le code postal pour valider.

2) ```js
    db.runCommand( { collMod: "salles",
        validator: {
            $jsonSchema: {
                bsonType: "object",
                required: [ "nom", "capacite", "adresse.codePostal", "adresse.ville" ],
                properties: {
                    _id: {
                        bsonType: "string" | "objectId",
                    }
                    nom: {
                        bsonType: "string",
                    },
                    capacite: {
                        bsonType: "int",
                    },
                    "adresse.codePostal": {
                        bsonType: "string"
                    },
                    "adresse.ville": {
                        bsonType: "string"
                    }
                }
            }
        }
    } )
    