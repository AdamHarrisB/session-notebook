What is the difference between a Library and a Framework

Next.js is a React FRAMEWORK. Built on top of the React library.

A library and a framework are both reusable code written by someone else. They help us solve common problems simply.

A library lets you use the code as and when you like.

A framework is Next.js is more rigid: you have limited choices as to where and how you use the code.

The tradeoff of these limitations is that the framework does a lot of work behind the scenes.

What is Next.js

Next.js is a React framework that gives you building blocks to create fast web applications (And perhaps create these fast too).

The building blocks it contains provide pre-built solutions for the main concepts, like user interface, routing, data fetching, infrastructure, etc.

Which Features of Next.js will we use in the Bootcamp?

    A template as a starting point
    A bundler, transpiler and development server
    Routing: navigation between pages
    Auto optimized images
    API Routes

How to Next.js: Basics

Differences to Vite

Here you can see a comparison of some relevant differences between Next.js and Vite:
	                    Next.js (new) 	                Vite (old)
Root component 	        _app.js 	                    App.jsx
Document 	            _document.js 	                /index.html
Default styling 	    CSS Modules* 	                CSS*
Rendering 	            Server and Client Side 	        Client Side
Route definition 	    file structure in pages folder 	n/a
Client side links 	    <Link> component 	            n/a
Image optimization 	    <Image> component 	            n/a
Modifying <head> 	    <Head> component 	            n/a
Font loading 	        @next/font package 	            n/a
API routes 	            pages/api folder 	            n/a
ESLint 	                Next.js specific rules 	        Vite specific rules
Bundler + transpiler 	Webpack/Turbopack + SWC 	    esbuild / Rollup

Server-Side Rendering

Vite sends the browser an almost empty HTML document (/index.html) whereas your React code is executed in the browser.

Next.js has a feature called "server-side rendering" which executes your React components on the server to send a complete HTML document to the client. On the client the React code is executed agai.

This allows for a lot of optimization techniques, but has one important implication:

Since the code is executed in a server environment you need to be aware that browser APIs, like window or document, will break the app on the server. When using browser APIs you need to insure that your code is only executed on the client, useEffect or onClick are suitable.

useEffect(() => {
  console.log(window.innerWidth);
}, []);

return <button onClick={() => console.log(window.innerWidth)}>Click me</button>;

Routing

Until now our React applications have only displayed a single page. The process of conditionally rendering different pages based on the URL and navigating between these is called routing.

Since a good routing solution is not easy to make, almost all react developers rely on an external routing library, like react-router

Next.js bases routing on the file system in the pages folder:

pages/index.js -> / (index.js always implies the root route of a folder)
pages/about.js -> /about

To support more complex routes you can create the appropriate nested folder structure:

pages/about/me.js -> /about/me
pages/about/all-others.js -> /about/all-others
pages/about/some/long/route.js -> /about/some/long/route

*You can define dynamic routes as well (routes that have dynamic parameters)

<Link> Component

For client-side transition between routes, use the <Link> component provided by next/link. Given a pages directory with

pages/index.js
pages/about.js
pages/about/me.js

You can link to each in the following way: 

            THIS IS IMPORTANT TO RECAP PROJECT 5

import Link from "next/link";

export default function Navigation() {
  return (
    <ul>
      <li>
        <Link href="/">Home</Link>
      </li>
      <li>
        <Link href="/about">About</Link>
      </li>
      <li>
        <Link href="/about/me">Me</Link>
      </li>
    </ul>
  );
}

Image Optimization with next/image

Next.js comes with automatic image optimization - the next/image component. This feature, for example, avoids shipping large images to devices with a smaller viewport and images are lazy-loaded by default.

Using <Image> comes with some default styling.

Here's some sample implementation. Note that the height and width props should be desired rendering size, with an aspect ratio identical to the source image.

            THIS IS ALSO IMPORTANT TO RECAP PROJECT

import Image from "next/image";

export default function AnimalImage() {
  <Image
    src="/images/a_small_dog.jpg"
    height={144}
    width={144}
    alt="A picture of a small dog"
  />;
}

When using images from an external domain you need to configure the allowed remote patterns in the next.config.js file:

const nextConfig = {
  reactStrictMode: true,

  images: {
    remotePatterns: [
      {
        protocol: "https",
        hostname: "images.unsplash.com",
        port: "",
      },
    ],
  },
};