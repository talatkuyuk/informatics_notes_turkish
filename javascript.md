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

// Returns capitalized verison of a parameter.
const capitalize = function (value) {
    return value.charAt(0).toUpperCase() + value.slice(1);
}

// Check the object is empty.
const isEmpty = Object.keys(object).length === 0;
```


On initial fetch() call, only the headers have been read. So, to parse the body as JSON, first the body data has to be read from the incoming stream. And, since reading from the TCP stream is asynchronous, the .json() operation ends up asynchronous. Note: the actual parsing of the JSON itself is not asynchronous. It's just the retrieving of the data from the incoming stream that is asynchronous.
```javascript
const usersResponse = await fetch('https://jsonplaceholder.typicode.com/users')
const userJson = await usersResponse.json();
```


objects
countries.length

```javascript
const doAsyncJobs = async () => {
 try {
   const result1 = await job1();
   const result2 = await job2(result1);
   const result3 = await job3(result2);
   return await job4(result3);
 } catch (error) {
   console.error(error);
 } finally {
   await anywayDoThisJob();
 }
}
```

```javascript
sumTwentyAfterTwoSeconds(10)
  .then(result => console.log('after 2 seconds', result));

async function sumTwentyAfterTwoSeconds(value) {
  const remainder = afterTwoSeconds(20)
  return value + await remainder
}

function afterTwoSeconds(value) {
  return new Promise(resolve => {
    setTimeout(() => { resolve(value) }, 2000);
  });
}
```

```javascript
function delay(ms) {
	return  new Promise(function(resolve, reject) {
		setTimeout(()=>resolve(ms),ms);
	});
}

delay(3000).then((ms)=>console.log("printed after " + ms + " seconds"));
```

```javascript
// syncron
fetch("https://jsonplaceholder.typicode.com/todos/1")
	.then(res => res.json())
	.then(data => console.log(data));

// async
const res = await fetch("https://jsonplaceholder.typicode.com/todos/1");
const data = await res.json();
```

```javascript
function handleData(data) {
	var url = 'https://localhost:5500/response.html';
	var formString = `<form action="${url}" method="POST"><input type="text" name="api_url" value="${JSON.stringify(data)}" target='_blank'></form>`;
	var form = stringToEl(formString)
	document.body.appendChild(form);
	form.submit();
}

function stringToEl(string) {
    var parser = new DOMParser(),
    content = 'text/html',
    DOM = parser.parseFromString(string, content);
    return DOM.body.childNodes[0];
}
```