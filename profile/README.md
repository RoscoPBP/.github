 # Wiki RoscoPBP
 
 ## Collections
### Users
Each document that represents an user will have the next keys and values:

```json
{
   "name":"john",
   "email":"john@gmail.com",
   "phone":"555444333",
   "uuid":"550e8400-e29b-41d4-a716-446655440000",
   "api_key":"AABBF234"
}
```

 ### User images
 Instead of saving each user avatar in the user documents, we will have another collection that only stores the images in base64, it uses the user's UUID to identify who it belongs to.
 
```json
{
   "userUUID":"550e8400-e29b-41d4-a716-446655440000",
   "base64":"iVBORw0KGgoAAAANSUhEUgAAATMAAAEyCAYAAACWBDf7AAAAIG.."
}
```

### Dictionaries
To store the words we will have a different dictionary for each language. In spanish we will have "es_diccionarios", the first two characters follow ISO 3166-1 alpha-2 codes. Here is an example of a document representing a word:

```json
{
   "word":"Alcachofa",
   "position":7,
   "language":"ES",
   "timesUsed":13
}
```

### Games
The documents represent all games that have been played:

```json
{
   "type":"multiplayer",
   "startDate":"12-12-12 14:54:22",
   "endDate":"12-12-12 14:54:22",
   "players":[
      {
         "name":"Juan Jose",
         "uuid":"550e8400-e29b-41d4-a716-446655440000",
         "score":13
      },
      {
         "name":"MariaDB",
         "uuid":"990e8400-e29b-41d4-a716-446655456500",
         "score":43
      }
   ],
   "letters":[
      "a",
      "e",
      "c",
      "s",
      "b",
      "t",
      "r"
   ],
   "words":[
      {
         "word":"tres",
         "wordUUID":"990e8400-e29b-645jk-a716-446655456500"
      },
      {
         "word":"casa",
         "wordUUID":"534k544-e29b-645jk-a716-446655456500"
      },
      {
         "word":"tarta",
         "wordUUID":"999SSS-e29b-645jk-a716-446655456500"
      }
   ]
}
```

### Actions Log
Here are documented all the different actions, data log.

```json
{
   "gameUUID":"760kl9-e29b-41d4-a716-446655440000"
   "playerUUID":"12345-e29b-41d4-a716-348538457385",
   "type":"MOVEMENT",
   "date":"12-12-12 14:54:22",
   "data":{
      "x":"56.6",
      "y":"56.6"
   }
}
```
