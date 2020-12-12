# Javascript Notları

### Kullanışlı expressions'lar 

```javascript
// Ask the user to enter a number
const userNumber = Number(window.prompt("Enter a number (1 - 6):"));

// Pick a random number between 1 and 6
const randomNumber = Math.floor(Math.random() * 6 + 1); 

// If the user enters a value that is not a number
if (isNaN(userNumber))

// If the user's number matches the random number
if (userNumber === randomNumber)

// Alert and template literal
alert(`Dice: ${result.randomNumber}: you got ${result.points} points`);
```


On initial fetch() call, only the headers have been read. So, to parse the body as JSON, first the body data has to be read from the incoming stream. And, since reading from the TCP stream is asynchronous, the .json() operation ends up asynchronous. Note: the actual parsing of the JSON itself is not asynchronous. It's just the retrieving of the data from the incoming stream that is asynchronous.
```javascript
const usersResponse = await fetch('https://jsonplaceholder.typicode.com/users')
const userJson = await usersResponse.json();
```


objects
countries.length