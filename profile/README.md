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
   "date":"12-12-12 14:54:22",
   "players":[
      "UUID1",
      "UUID2..."
   ]
}
```

### Actions Log
Here are documented all the different actions, data log.

```json
{
   "associated":"Entity UUID",
   "type":"MOVEMENT",
   "date":"12-12-12 14:54:22",
   "data":{
      "x":"56.6"
   }
}
```
