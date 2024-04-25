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
   "dictionaryCode":"ES",
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

## Algorithms

### Calculate Each Word's Score Values

Online:

- Before starting the game, the servers calculate the average value of "timesUsed" and the average length of the words in the dictionary from the database. We store these values until the end of the game so they do not have to be recalculated again.
- When a word is recognized as a real one, we calculate the value based on the rarity of the letters it is made of. For instance, each "z" adds 10 points, while each "a" adds just 1 point and so on.
- We retrieve the "timesUsed" attribute of the word. If it is lower than the (average + 1), we add an additional +3 points.
- We then calculate the length of the word. If it is greater than the average, we multiply the total value by x1.4.

Offline:
- Each word adds +10 points; no other variables are taken into consideration.

### Calculate the Letters to be Used In-Game
- Online: The number of letters is calculated from the average length multiplied by a random value between x0.7 and x1.3.
- Offline: The number of letters is 10 multiplied by a random value between x0.7 and x1.3.

**When choosing the letters to be featured, we follow these instructions:**

- We have three different groups/lists of letters: vowels, frequently used consonants, and rarely used consonants.
- In any case, we choose at least two vowels from the list.
- The next letters are chosen following a percentage: 70% chance of being a frequently used consonant, 20% chance of being a rarely used consonant, and 10% chance of being another vowel. We get a random letter from the selected group.
- We follow these instructions until we have the desired amount of words. Each time we select a letter, it is removed from the list so it cannot be selected again.
