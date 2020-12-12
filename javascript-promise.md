# Javascript Promise, Async, Await Notları

### Promise, Then, Catch, Finally (example birthday)

```javascript
const myBirthday = (isSick) => {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      if (!isSick) {
        resolve(2);
      } else {
        reject(new Error("I am sad"));
      }
    }, 2000);
  });
};

myBirthday(false)
  .then((result) => {
    console.log(`I have ${result} cakes`); // In the console: I have 2 cakes  
  })
  .catch((error) => {
    console.log(error); // Does not run
  })
  .finally(() => {
    console.log("Party"); // Shows in the console no matter what: Party
  });
```

### Promise, Async, Await, Try, Catch (Build a guessing game)

```javascript
const enterNumber = () => {
  return new Promise((resolve, reject) => {
    const userNumber = Number(window.prompt("Enter a number (1 - 6):")); // Ask the user to enter a number
    const randomNumber = Math.floor(Math.random() * 6 + 1); // Pick a random number between 1 and 6
    
    // If the user enters a value that is not a number, run reject with an error
    if (isNaN(userNumber)) {
      reject(new Error("Wrong Input Type")); 
    }

    // If the user's number matches the random number, return 2 points
    if (userNumber === randomNumber) { 
      resolve({
        points: 2,
        randomNumber,
      });
    
    // If the user's number is different than the random number by 1, return 1 point
    } else if (userNumber === randomNumber - 1 || userNumber === randomNumber + 1) { 
      resolve({
        points: 1,
        randomNumber,
      });
    
    // Else return 0 points
    } else { 
      resolve({
        points: 0,
        randomNumber,
      });
    }
  });
};

const continueGame = () => {
  return new Promise((resolve) => {
    // Ask if the user want to continue the game with a confirm modal
    if (window.confirm("Do you want to continue?")) { 
      resolve(true);
    } else {
      resolve(false);
    }
  });
};

// option 2
const continueGame = () => {
  return new Promise((resolve) => resolve(window.confirm("Do you want to continue?")));
};

const handleGuess = async () => {
  try {
    const result = await enterNumber(); // Instead of the then method, we can get the result directly by just putting await before the promise

    alert(`Dice: ${result.randomNumber}: you got ${result.points} points`);

    const isContinuing = await continueGame();

    if (isContinuing) {
      handleGuess();
    } else {
      alert("Game ends");
    }
  } catch (error) { // Instead of catch method, we can use the try, catch syntax
    alert(error);
  }
};

handleGuess(); // Run handleGuess function
```

### Async, Await (Fetch country info from an API)

```javascript
const fetchData = async () => {
    // fetch() returns a promise, so we need to wait for it
    const res = await fetch("https://restcountries.eu/rest/v2/alpha/col"); 

    // res is now only an HTTP response, so we need to call res.json()
    const country = await res.json(); 

    console.log(country); // Columbia's data will be logged to the dev console
};

fetchData();
```


### Promise.all Async, Await (Fetch a country's neighboring countries)

```javascript
const fetchCountry = async (alpha3Code) => {
  try {
    const res = await fetch(`https://restcountries.eu/rest/v2/alpha/${alpha3Code}`);
    const data = await res.json();
    return data;
    
  } catch (error) {
    console.log(error);
  }
};

const fetchCountryAndNeigbors = async () => {
  const columbia = await fetchCountry("col");

  const neighbors = await Promise.all(
    columbia.borders.map((border) => fetchCountry(border))
  );

  console.log(neighbors);
};

fetchCountryAndNeigbors();
```
