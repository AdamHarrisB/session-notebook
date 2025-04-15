Next.js Dynamic Routes

Concept of Dynamic Routes

If your app have many possible routes with repeating patterns it would be hard to impossible to create a JavaScript file per route.

Using dynamic routes you can turn the path into dynamic parameters using square brackets. If the URL matches the path, Next.js will make the dynamic query parameters available using the useRouter hook.

movies/category/[categorySlug]/page/[pageNumber].js

movies/category/romance/page/12

Movies() {
    const router = useRouter();
    const {
        categorySlug,
        pageNumber
    } = router.query;
}

Implementing Dynamic Routes

To create a dynamic route, you can add square brackets around file or folder names in the pages directory respectively: pages/movies/[categorySlug]/page/[pageNumber].js

The following paths map to this example:

    movies/romance/page/12
        categorySlug is "romance"
        pageNumber is "12"

    movies/action/page/1
        categorySlug is "action"
        pageNumber is "1"

    movies/comedy/page/3
        categorySlug is "comedy"
        pageNumber is "3"

To access the query parameters in a component use the useRouter hook, imported from next/router:

// pages/movies/categories/[categorySlug]/page/[pageNumber].js
import { useRouter } from "next/router";

export default function CategoryPage() {
  const router = useRouter();
  const { categorySlug, pageNumber } = router.query;

  return (
    <div>
      <p>Category Slug: {categorySlug}</p>
      <p>Page Number: {pageNumber}</p>
    </div>
  );
}

Linking to Dynamic Routes

You can use the Link component to link to dynamic paths. Use string interpolation with a template string to insert the dynamic query parameters into the path.

Considering a Movies component which renders a list of all links to all movies, interpolate the slug into the path as a query parameter:

import Link from "next/link";

export default function Movies({ movies }) {
  return (
    <ul>
      {movies.map(({ id, slug, title }) => (
        <li key={id}>
          <Link href={`/movies/${slug}`}>{title}</Link>
        </li>
      ))}
    </ul>
  );
}

Imperative Routing

Using <Link> is the best option whenever the user navigates through the app on their own. There are situations where you cannot use a link component as you want to navigate to a page programmatically. One example of non-direct user interaction is changing the page after submitting a form:

import { useRouter } from "next/router";

export default function Form() {
  const router = useRouter();

  function handleSubmit(event) {
    // some data handling … ✨

    router.push("/home");
  }

  return <form onSubmit={handleSubmit}>…</form>;
}

Next/Head Component

Next.js comes with a built-in <head> component for appending elements to the head of the page. This way you can modify the metadata of the page such as the <title> HTML tag:

import Head from "next/head";

export default function Movies() {
  return (
    <>
      <Head>
        <title>Movies</title>
        <meta name="viewport" content="initial-scale=1.0, width=device-width" />
      </Head>
      <ul>…</ul>
    </>
  );
}


