React Data Fetching

Up until now we've used the useEffect hook to fetch data. This has meant that we've had to take care of:

    Caching fetched data
    Refetching programmatically
    Implementing an error and loading state
    Fetching on interval

A fetching library (like SWR - https://swr.vercel.app/#features) provides us with shortcuts

How to SWR

Basic Fetching

To use the useSWR hook, you have to create a fetcher function, which is a wrapper of the native fetch. It looks like this:

const fetcher = (...args) => fetch(...args).then((response) => response.json());

You can then import the useSWR hook and pass it to two arguments: the url you want to fetch, and the fetcher function. useSWR returns a data object you can use in your JSX.

import useSWR from "swr";

const fetcher = (...args) => fetch(...args).then((response) => response.json());

function Character() {
  const { data } = useSWR("https://swapi.py4e.com/api/people/1", fetcher);

  // render data
  return <div>Hello {data.name}!</div>; // Hello Luke Skywalker!
}

*useSWR returns an object which you destructure data from. You therefore cannot simply call the data object, but instead have to rename it according to "destructuring rules" : { data: person }. (what are these): https://swr.vercel.app/docs/getting-started

The fetcher function above uses .then syntax for handling the fetch and .json promises. You can also rewrite this code with more familiar syntax

async function fetcher(url) {
  const response = await fetch(url);
  return await response.json();
}

Configuring SWR

An application-wide configuration for SWR. You do this by passing a config object to the SWRConfig component in your App. In Next.js that's pages/_app.js

The below example sets an application wide fetcher function and an application wide refreshInterval:

import { SWRConfig } from "swr";

async function fetcher(url) {
  const response = await fetch(url);
  return await response.json();
}

function App() {
  return (
    <SWRConfig
      value={{
        fetcher,
        refreshInterval: 1000,
      }}
    >
      {/* … your app */}
    </SWRConfig>
  );
}

This is convenient if we want to use this function in many places.

Loading and Error State

The useSWR hook provides us with an error, isLoading and isValidating state you can use to create the respective UI output.

You can destruct them, as with the data object, and use them to conditionally return JSX:

function Character() {
  const { data, error, isLoading, isValidating } = useSWR(
    "https://swapi.py4e.com/api/people/1"
  );

  if (error) return <div>failed to load</div>;
  if (isLoading) return <div>loading...</div>;

  // render data
  return (
    <div>
      <span role="img" aria-label={isValidating ? "Validating" : "Ready"}>
        {isValidating ? "🔄" : "✅"}
      </span>
      Hello {data.name}!
    </div>
  );
}

The above fetcher function does not "throw" an Error object for non-ok responses. Throwing is required for a SWR to recognise an error property of the object returned by the hook.

You can customize the fetcher to throw an Error with additional information:

async function fetcher(url) {
  const response = await fetch(url);

  // If the status code is not in the range 200-299,
  // we still try to parse and throw it.
  if (!response.ok) {
    const error = new Error("An error occurred while fetching the data.");
    // Attach extra info to the error object.
    error.info = await response.json();
    error.status = response.status;
    throw error;
  }

  return response.json();
}

The above function throws an error with the keys info and status if the status code of the response is not in the range of 200-299.

You can use the error object to display a more detailed error message (message is the string from new Error()):

function Character() {
  const { data, error, isLoading } = useSWR(
    "https://swapi.py4e.com/api/people/1"
  );

  if (error) return <div>{error.message}</div>;
  if (isLoading) return <div>loading...</div>;

  // render data
  return <div>Hello {data.name}!</div>;
}

Fetch on Interval and Button Click

To refetch the API on interval, pass a refreshInterval value inside of an option object as an additional argument to the useSWR hook. In this example SWR will refetch the API every second:

useSWR("https://swapi.py4e.com/api/people/1", { refreshInterval: 1000 });

To fetch data programmatically you can use the mutate function provided by the useSWR hook.

function Character() {
  const { data, mutate } = useSWR("https://swapi.py4e.com/api/people/1");

  return <RefetchButton onRefetch={() => mutate()}>Refetch data</RefetchButton>;
}

function RefetchButton({ children, onRefetch }) {
  return (
    <button type="button" onClick={onRefetch}>
      {children}
    </button>
  );
}

Data is Cached

SWR will cache the fetched data in the browser's memory. This means if you fetch the same date twice the second time it will be loaded from the cache instead of the network. This means that you can use the useSWR hook multiple times in your app without having to worry about fetching the same data multiple times.

function CharacterName() {
  const { data } = useSWR("https://swapi.py4e.com/api/people/1");
  return <div>Hello {data.name}!</div>; // Hello Luke Skywalker!
}

function CharacterHairColor() {
  const { data } = useSWR("https://swapi.py4e.com/api/people/1");
  return <div>His hair color is {data.hair_color}.</div>; // His hair color is blond.
}

function CharacterHeight() {
  const { data } = useSWR("https://swapi.py4e.com/api/people/1");
  return <div>He is {data.height} cm tall.</div>; // He is 172 cm tall.
}

function App() {
  return (
    <>
      <CharacterName />
      <CharacterHairColor />
      <CharacterHeight />
    </>
  );
}

This application will fetch the data only once, even though the hook is used three times.

Additionally if you were to manually mutate date, the cache would be updated and the data would be available to all components using the useSWR hook with the same key (url).

This is true even if you were to call mutate from yet another component, as long as it has the same key (URL):

function RevalidateButton() {
  const { mutate } = useSWR("https://swapi.py4e.com/api/people/1");
  return (
    <button type="button" onClick={() => mutate()}>
      Revalidate
    </button>
  );
}

// … other components

function App() {
  return (
    <>
      <CharacterName />
      <CharacterHairColor />
      <CharacterHeight />
      <RevalidateButton />
    </>
  );
}

SWR Response API

The useSWR hook returns an SWR response object with the following properties:

response property 	description
data 	            The data fetched for the given key (URL)
error 	            An error object if the fetcher function threw an error
isLoading 	        true if the data is being loaded for the first time
isValidating 	    true if there is any request or revalidation  loading
mutate 	            A function to mutate the data

Combine Fetched Data with Local State

With SWR you don't control the data fetched yourself. This means you can't modify the state directly. This is good.

If you want to enrich server data fetched with local state (isFavorite property added to a movie), you can use the useSWR hook to fetch the date and the useState hook to manage the local state. The individual pairs of local data and server data should be connected via a unique identifier (like id or slug)

In the end you have two arrays of data: one fetched from the server and one local:

// fetched Data
[
  {
    id: 1,
    title: "Star Wars",
    year: 1977,
  },
  {
    id: 2,
    title: "The Empire Strikes Back",
    year: 1980,
  },
  //...
  {
    id: 57,
    title: "The Big Lebowsky",
    year: 1995,
  },
];

//local data
[
  {
    id: 1,
    isFavorite: true,
  },
  {
    id: 2,
    isFavorite: false,
  },
];

We can then match the data via the unique identifier:

// data for id 1:
{
	id: 1,
	title: "Star Wars",
	year: 1977,
},
{
	id: 1,
	isFavorite: true,
}

// data for id 2:
{
	id: 2,
	title: "The Empire Strikes Back",
	year: 1980,
},
{
	id: 2,
	isFavorite: false,
}

// data for id 57:
{
	id: 57,
	title: "The Big Lebowsky",
	year: 1995,
}
//no local data saved yet!

In our application this might look something like this:

function Movies() {
  const { data: moviesData } = useSWR("/api/movies");

  // initialize the local state with an empty array
  const [moviesInfo, setMoviesInfo] = useState([]);

  function handleToggleFavorite(id) {
    setMoviesInfo((moviesInfo) => {
      // find the movie in the state
      const info = moviesInfo.find((info) => info.id === id);

      // if the movie is already in the state, toggle the isFavorite property
      if (info) {
        return moviesInfo.map((info) =>
          info.id === id ? { ...info, isFavorite: !info.isFavorite } : info
        );
      }

      // if the movie is not in the state, add it with isFavorite set to true
      return [...moviesInfo, { id, isFavorite: true }];
    });
  }

  return (
    <ul>
      {moviesData.map(({ id, title, year }) => {
        // find the movie in the state and destructure the isFavorite property
        // if it is not in the state, default isFavorite to false
        const { isFavorite } = moviesInfo.find((info) => info.id === id) ?? {
          isFavorite: false,
        };

        return (
          <li key={id}>
            {title} ({year})
            <button type="button" onClick={handleToggleFavorite(id)}>
              {isFavorite ? "Remove from favorites" : "Add to favorites"}
            </button>
          </li>
        );
      })}
    </ul>
  );
}