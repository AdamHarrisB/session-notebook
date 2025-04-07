Avoiding State Mutation

However complex the state in your application is, you must always treat state as immutable. This means you shouldn't "mutate" the state by reassigning a new value to it.

To avoid this:

Create a new object / array (or make a copy of the existing one)
Then use the setter function with the newly created/copied one to trigger a re-render.

Updating Objects in State

To make a copy of an object and change only some properties, use the spread syntax:

const [person, setPerson] = useState({
  firstName: "John",
  lastName: "Doe",
});

//this bit is presumably the "spread syntax"
function handleChangeFirstName(firstName) {
  setPerson({ ...person, firstName });
}

// Somewhere else:
handleChangeFirstName("Jane");

*If you assigned a new value directly, you'd mutate the state. Doing this can lead to hard to find bugs. This is bad.

// ⚠️ NEVER DO THIS
function handleChangeFirstName(firstName) {
  person.firstName = firstName;
  setPerson(person);
}

Updating Array in State

There are several ways to update arrays, but many of them mutate the state. Avoid using push, unshift, pop, shift, splice, arr[i]=..., reverse or sort.

Instead

    To add, use [...arr] (spread syntax)

    To remove, use filter

    To replace, use map

    To sort, copy the array first.

Adding to an array

To add an element to an array, again, we use the spread synax, as below:

const [numbers, setNumbers] = useState([0, 1, 2]);

function handleAppendNumber(number) {
  setNumbers([...numbers, number]);
}

// Somewhere else:
handleAppendNumber(3);

function handlePrependNumber(number) {
  setNumbers([number, ...numbers]);
}

// Somewhere else:
handlePrependNumber(-1);

Removing from an Array

To remove, use filter:

const [numbers, setNumbers] = useState([0, 1, 2]);

function handleRemoveNumber(numberToRemove) {
  setNumbers(numbers.filter((number) => number !== numberToRemove));
}

// Somewhere else:
handleRemoveNumber(1);

Replacing an Array Element

Replace an Array Element with map:

const [numbers, setNumbers] = useState([0, 1, 2]);

function handleReplaceNumber(oldNumber, newNumber) {
  setNumbers(
    numbers.map((number) => {
      if (number === oldNumber) return newNumber;
      return number;
    })
  );
}

// Somewhere else:
handleReplaceNumber(1, 1337);

Updating Arrays of Objects in State

Most of the time we encounter arrays of objects in our states.

Adding a new object

We can add a new object to the state array by using spread syntax:

const [trees, setTrees] = useState([
  { id: 0, name: "Oak", height 7.5},
  { id: 1, name: "Beech", height 6},
  { id: 2, name: "Pine", height 10}
]);

function handleAddTree(tree) {
  setTrees([...trees, tree]);
}

// Somewhere else:
handleAddTree({id: 3, name: "Spruce", height: 13})

Remove an Object

Again, you can use filter to find a unique identifier in the array. In most cases this identifier is in scope because the relevant object is rendered via map.

const [trees, setTrees] = useState([
  { id: 0, name: "Oak", height 7.5},
  { id: 1, name: "Beech", height 6},
  { id: 2, name: "Pine", height 10}
]);

function handleRemoveTree(idToRemove) {
  setTrees(trees.filter((tree) => tree.id !== idToRemove));
}

// Somewhere else:
handleRemoveTree(0);

Replacing an Object

To replace an Object, we can use map to create a new array with the updated object. Remember to create the copy of the object first, otherwise you will mutate the state

const [trees, setTrees] = useState([
  { id: 0, name: "Oak", height 7.5},
  { id: 1, name: "Beech", height 6},
  { id: 2, name: "Pine", height 10}
]);

function handleSetNewHeightForTree(id, height) {
  setTrees(
    trees.map((tree) => {
      if (tree.id === id) return { ...tree, height };
      return tree;
    })
  );
}

// Somewhere else:
handleSetNewHeightForTree(0, 8);

Sorting an Array of Objects

To sort an array of object, use sort on a copy of the array with a custom compare function. This compare function returns a number, which is used to determine the order of the elements

const [trees, setTrees] = useState([
  { id: 0, name: "Oak", height 7.5},
  { id: 1, name: "Beech", height 6},
  { id: 2, name: "Pine", height 10}
]);

function handleSortTreesByHeight() {
  setTrees([...trees].sort((a, b) => a.height - b.height));
}

Choosing State Structure

Some things to bear in mind when choosing your state structure:

Group Related State

// ❌ MEH
const [userName, setUserName] = useState("Alex");
const [userAge, setUserAge] = useState(28);

// ✅ BETTER
const [user, setUser] = useState({ name: "Alex", age: 28 });

Avoid Redundant State

// ❌ BAD
const [user, setUser] = useState({ name: "Alex", age: 28 });
const [isAdult, setIsAdult] = useState(user.age >= 18);

// ✅ GOOD
const [user, setUser] = useState({ name: "Alex", age: 28 });
const isAdult = user.age >= 18;

Avoid Duplication in State

// ❌ BAD
const [trees, setTrees] = useState([
  { id: 0, name: "Oak", height 7.5},
  { id: 1, name: "Beech", height 6},
  { id: 2, name: "Pine", height 10}
]);

const [selectedTree, setSelectedTree] = useState(trees.find((tree) => tree.id === 0));

// Somewhere else:
setSelectedTree(trees.find((tree) => tree.id === 2));


// ✅ GOOD
const [trees, setTrees] = useState([
  { id: 0, name: "Oak", height 7.5},
  { id: 1, name: "Beech", height 6},
  { id: 2, name: "Pine", height 10}
]);

const [selectedTreeId, setSelectedTreeId] = useState(0);

const selectedTree = trees.find((tree) => tree.id === selectedTreeId);

// Somewhere else:
setSelectedTreeId(2);

Avoid Having Duplicate Lists in State

// ❌ BAD
const [trees, setTrees] = useState([
  { id: 0, name: "Oak", height 7.5},
  { id: 1, name: "Beech", height 6},
  { id: 2, name: "Pine", height 10}
]);

const [filteredTrees, setFilteredTrees] = useState(trees.filter((tree) => tree.height > 7));

// Somewhere else:
setFilteredTrees(trees.filter((tree) => tree.height > 9));

// ✅ GOOD
const [trees, setTrees] = useState([
  { id: 0, name: "Oak", height 7.5},
  { id: 1, name: "Beech", height 6},
  { id: 2, name: "Pine", height 10}
]);

const [minHeight, setMinHeight] = useState(7);

const filteredTrees = trees.filter((tree) => tree.height > minHeight);

// Somewhere else:
setMinHeight(9);