# Command-line CRUD Application

In this pre-reading, you'll be building an app that helps motivate people to go outside and seek out nature. The person will go outside, try to (safely) find as many animals as possible, then record them. Rarer animals (fauna) will be worth more points.

## Lesson Objectives

By the end of this lesson

- Develop a list of minimal features
- Create an app that uses user input to
- Create data
- Read data
- Delete data
- Update data

## Getting started

With coding, there is always a temptation to jump into coding and solve whatever comes along. However, it's essential to take a few steps back. When you code without a plan, you can create features that no one asked for, make your code too complex, wholly misunderstand what you are building, or try to build something impossible within the time and technology constraints.

Building an app that lets users look for animals in NYC can conjure a lot of cool features. The list uses a particular pattern that usually starts with `A user can` - writing out features this way can be helpful because a non-technical person can understand what the feature should do and a technical person can understand what functionality they need to build.

- A user can add a map location where the animal was seen.
- A user can see a list of animals.
- A user can see a more detailed view of an animal, including a picture and description of each animal.
- Create a checking system to ensure users are not making up what they've seen.
- Allow a user to take a photo and let AI determine what animal it is.
- If an animal is found, add a pin to a map location and store that for the user.
- Call a wildlife center if an animal is dangerous or sick.
- Allow users to participate in a high scores daily board.
- Allow users to participate in an all-time high scores board.
- Allow users to compete against friends.

Suddenly, a "simple" app has grown quite complex and would require numerous technologies. Most business ideas start with something called `Minimum Viable Product`. It is the most basic form of the app for users to use. For example, when eBay started, there was no payment system. People had to mail each other checks or cash. When building your apps, figuring out the minimum functionality required is crucial. Most of the time, the app will be underwhelming and clunky in places. The user experience will be less than ideal. Let's whittle down the above list into something you can build today.

- A user can have a list of animals they've seen
- A user can create a new animal
- A user can see the details of a new animal
- A user can delete an animal
- A user can update an animal
- A user can see their score

You can either read or code along.

- `mkdir fauna-go`
- `cd fauna-go`
- `touch .gitignore` (and add appropriate files and folders)
- `touch index.js`
- `mkdir src`
- `touch src/helpers.js`
- `npm init -y`

Based on the user stories above, create scripts that would run the following (`Rsl_` represents a unique id for an example animal):

```
npm run index
npm run create bat
npm run show Rsl_
npm run update Rsl_ "red fox"
npm run destroy Rsl_
npm run score
```

`package.json`:

```json
 "scripts":{
 "index": "node index.js index",
 "create": "node index.js create",
 "show": "node index.js show",
 "update": "node index.js update",
 "destroy": "node index.js destroy",
 "score": "node index.js score"
}
```

In the `index.js` file, create a `run` function that will handle the scripts.

Additionally, `console.log` will serve two purposes, to `inform` your user about something or for you (the developer) to debug. To help clarify which console log does what, you can give `console.log` an alias:

```js
// give console.log an alias
// When providing user feedback use `inform`
// When developing/debugging use `console.log`
const inform = console.log;

function run() {
  const action = process.argv[2];
  const animal = process.argv[3];
  switch (action) {
    case "index":
      inform(action);
      break;
    case "create":
      inform(action, animal);
      break;
    case "show":
      inform(action, animal);
      break;
    case "update":
      inform(action, animal);
      break;
    case "destroy":
      inform(action, animal);
      break;
    case "score":
      inform(action);
      break;
    default:
      inform("There was an error.");
  }
}
run();
```

Test each script to be sure things work as expected:

```
npm run index
npm run create bat
npm run show Rsl_
npm run update Rsl_ "red fox"
npm run destroy Rsl_
npm run score
npm run oops
```

### Index

- `mkdir data`
- `touch data/animals.json`

In the `helpers.js` file, create the same functionality from the previous lesson:

```js
const { readFileSync, writeFileSync } = require("node:fs");

function readJSONFile(path, fileName) {
  const collection = readFileSync(`${path}/${fileName}`, "utf8");
  return collection ? JSON.parse(collection) : [];
}

function writeJSONFile(path, fileName, data) {
  data = JSON.stringify(data);
  return writeFileSync(`${path}/${fileName}`, data, { encoding: "utf-8" });
}

module.exports = {
  readJSONFile,
  writeJSONFile,
};
```

Import these functions to `index.js`.

In the `index.js` file's run function, get the data from the `animals.json` file and update the index case to log the file contents:

```js
let animals = readJSONFile("./data", "animals.json");

//Further down

 case "index":
 inform(action, animals);
```

For now, `animals` should be an empty array.

### Create

The user will run the command `npm run create bat` to create a new animal. A new animal should be a new entry into the user's data. Each animal should have a unique id, a name, and the points associated with it. Then the animal should be added to the end of the animals array.

This functionality controls what happens to the data. Therefore it is a separate concern from the other functionality you've built. Make a new file called `animalController.js` in the `src` folder

```js
function create(animals, animalName) {
  const animal = { name: animalName };
  animals.push(animal);
  return animals;
}
```

To add an id, you need to add an npm package to generate a unique id. Limit the `id` to be 4 characters long, so that there is less for the user to type.

```
npm install nanoid@3
```

Require it and use it in the create function.

```js
// animalController.js
const { nanoid } = require("nanoid");

function create(animals, animalName) {
  const animal = { name: animalName, id: nanoid(4) };
  animals.push(animal);
  return animals;
}
```

Lastly, we need to get the points. Create a new file called `animalPoints.json` and import this data into `animalController.js`

[Resource](https://www.nycgovparks.org/programs/wildlife-management/calendar):

```json
{
  "squirrel": 2,
  "coyote": 40,
  "owl": 10,
  "bald eagle": 100,
  "seal": 30,
  "virginia opossum": 40,
  "osprey": 20,
  "peregrine falcon": 30,
  "piping plover": 20,
  "red-tailed hawk": 50,
  "bat": 30,
  "racoon": 10,
  "spotted salamander": 50,
  "spring peeper": 50,
  "whale": 200,
  "canadian goose": 5,
  "horseshoe crab": 10,
  "painted turtle": 20,
  "white-tailed deer": 20,
  "american bullfrog": 40,
  "diamond-backed terrapin": 20,
  "red-backed salamander": 60,
  "monarch butterfly": 50,
  "red fox": 80
}
```

Access the points by key:

```js
function create(animals, animalName) {
  const animal = {
    name: animalName,
    id: nanoid(4),
    points: animalPoints[animalName],
  };
  animals.push(animal);
  return animals;
}
```

Finally, save the added animal to the file.

Start by adding two variables to the top of the `run` function.

```js
// index.js
function run {
let writeToFile = false;
let updatedAnimals = [];
// Rest of code
```

Update the `create` case.

```js
 case "create":
 updatedAnimals = create(animals, animal);
 writeToFile = true;
 break;
```

Write some logic on whether or not to write to the file after the switch statement.

```js
if (writeToFile) {
  writeJSONFile("./data", "animals.json", updatedAnimals);
}
```

### Minimum Viable Product

You may wonder, what if the user enters `Bat` instead of `bat`? Or what if the user has seen an animal not on the list? What if the user misspells `peregrine` or only knows they saw a `falcon`? Wouldn't it be nice to solve these things?

Yes.

However, look back to your initial plan. None of these features are part of the plan. When working on a team, you will be given features to build, and you should only build those features. If you think you need to make something else, you would talk to your team/manager and decide whether to switch what you are working on or add these features to a list of things to work on in the future.

### Index (again)

Typically, an index is a list of things with limited details. When you think of an online store, you usually see one image, a name, and a price. Then when you click the item, you will see more details.

Finish building out the index view.

```js
// animalsController.js

function index(animals) {
  return animals.map((animal) => animal.id + " " + animal.name).join("\n");
}
```

Be sure to export and then import the function to `index.js`

Update the `index` case in `index.js`:

```js
 case "index":
 const animalsView = index(animals);
 inform(animalsView);
 break;
```

### Show

Thinking about an online store, you also want to see a detailed view of an item. In this case, the user would pass the id to see a detailed view. The sample id shown is `Rsl_`.

```
npm run show Rsl_
```

First, take the entire array of animal objects. Then find the object that has a matching id. Then send back a human-readable view:

```js
// animalController.js
function show(animals, animalId) {
  const animal = animals.find((animal) => animal.id === animalId);
  return animal.id + " " + animal.name + " " + animal.points + " points";
}
```

### Destroy

Destroying an animal object will also require the animal id.

> **Note**: `delete` is a keyword in JavaScript. You cannot name a function of this word. Therefore, the alternative word `destroy` will be used.

```
npm run destroy Rsl_
```

```js
// animalController.js
const inform = console.log;

function destroy(animals, animalId) {
  const index = animals.findIndex((animal) => animal.id === animalId);
  if (index > -1) {
    animals.splice(index, 1);
    inform("Animal successfully removed from collection");
    return animals;
  } else {
    inform("Animal not found. No action taken");
    return animals;
  }
}
```

Export and import this function to `index.js`

Update the `destroy` case in `index.js`

```js
 case "destroy":
 updatedAnimals = destroy(animals, animal);
 writeToFile = true;
 break;
```

### Update

You'll use the `id` for this action as well. Additionally, you'll need to enter the new animal name.

```
npm run update Rsl_ "red fox"
```

```js
// Animals Controller
function edit(animals, animalId, updatedAnimal) {
  const index = animals.findIndex((animal) => animal.id === animalId);
  if (index > -1) {
    animals[index].id = animalId;
    animals[index].name = updatedAnimal;
    animals[index].points = animalPoints[updatedAnimal];
    inform("Animal successfully updated");
    return animals;
  } else {
    inform("Animal not found. No action taken");
    return animals;
  }
}
```

Export and import this function to `index.js`.

Update the `update` case in `index.js`

```js
 case "update":
 updatedAnimals = edit(animals, animal, process.argv[4]);
 writeToFile = true;
 break;
```

### Score

The score will be the sum of the animal points. Update the `score` case in `index.js`

```js
 case "score":
 const score = animals.reduce((acc, current) => acc + current.points, 0);
 inform("Current score", score);
 break;
```

### Future Improvements

You have now built a complete CRUD app. No matter how many features you build, an app is never quite finished. What are the next steps you'd take to improve this app?

## Reference Files

### index.js

```js
const { writeJSONFile, readJSONFile } = require("./src/helpers");
const {
  create,
  destroy,
  edit,
  index,
  show,
} = require("./src/animalController.js");

const inform = console.log;

function run() {
  const action = process.argv[2];
  const animal = process.argv[3];
  let animals = readJSONFile("data", "animals.json");
  let writeToFile = false;
  let updatedAnimals = [];
  switch (action) {
    case "index":
      const animalsView = index(animals);
      inform(animalsView);
      break;
    case "create":
      updatedAnimals = create(animals, animal);
      writeToFile = true;
      break;
    case "show":
      const animalView = show(animals, animal);
      inform(animalView);
      break;
    case "update":
      updatedAnimals = edit(animals, animal, process.argv[4]);
      writeToFile = true;
      break;
    case "destroy":
      updatedAnimals = destroy(animals, animal);
      writeToFile = true;
      break;
    case "score":
      const score = animals.reduce((acc, curr) => acc + curr.points, 0);
      inform("Current score", score);
      break;
    default:
      inform("There was an error.");
  }
  if (writeToFile) {
    writeJSONFile("data", "animals.json", updatedAnimals);
  }
}
run();
```

### animalController.js

```js
const { nanoid } = require("nanoid");
const animalPoints = require("./animalPoints.json");

const inform = console.log;
function create(animals, animalName) {
  const animal = {
    name: animalName,
    id: nanoid(4),
    points: animalPoints[animalName],
  };
  animals.push(animal);
  return animals;
}

function index(animals) {
  return animals.map((animal) => animal.id + " " + animal.name).join("\n");
}

function show(animals, animalId) {
  const animal = animals.find((animal) => animal.id === animalId);
  return animal.id + " " + animal.name + " " + animal.points + " points";
}
function destroy(animals, animalId) {
  const index = animals.findIndex((animal) => animal.id === animalId);
  if (index > -1) {
    animals.splice(index, 1);
    inform("Animal successfully removed from collection");
    return animals;
  } else {
    inform("Animal not found. No action taken");
    return animals;
  }
}

function edit(animals, animalId, updatedAnimal) {
  const index = animals.findIndex((animal) => animal.id === animalId);
  if (index > -1) {
    animals[index].id = animalId;
    animals[index].name = updatedAnimal;
    animals[index].points = animalPoints[updatedAnimal];
    inform("Animal successfully updated");
    return animals;
  } else {
    inform("Animal not found. No action taken");
    return animals;
  }
}

module.exports = { create, destroy, edit, index, show };
```
