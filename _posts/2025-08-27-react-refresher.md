---
title: "Movie World: A React Refresher with TMDB API & Appwrite"
date: 2025-08-27
categories: [React, Frontend Development, Web Development]
tags: [React 19, Movie App, TMDB API, Appwrite, Pagination]
---

It had been a while since I last worked with **React and Redux**. As a backend developer, most of my time usually goes into APIs, databases, and infrastructure. To refresh my frontend knowledge and get up to speed with **React 19**, I decided to build a small side project: **Movie World**.  

This app lets you **search movies, explore trending picks, and load more results**. It uses the **TMDB API** for fetching data, **Appwrite** for tracking trending searches, and React for building a modular, responsive interface.  

I followed references, tutorials, and community examples to put this together — because the best way to relearn is to **learn by building**.  

## Why I Built Movie World  

- To **refresh my React knowledge** after a long break.  
- To practice **React 19 features** like hooks and cleaner state handling.  
- To rebuild confidence in writing **modular frontend code**.  
- To explore **real API integration** with a touch of backend analytics.  

## Features  

- **Search movies with debounce** → prevents unnecessary API calls.  
- **Trending movies** → powered by Appwrite backend, tracking searches.  
- **Load More button** → fetches the next page of movies on demand.  
- Modular components: `Header`, `TrendingMovies`, `AllMovies`, `MovieCard`, `Search`, `Spinner`.  
- Movie cards open TMDB links in new tabs.  
- Responsive layout using Tailwind CSS.  

## Tech Stack  

- **React 19 + Vite** → fast, modern dev setup.  
- **TMDB API** → for real-time movie data.  
- **Appwrite** → for tracking searches.  
- **Tailwind CSS** → for responsive UI.  

## Key Implementation Details  

### Debounced Search  
Used `useDebounce` so the API is only called after the user pauses typing:  

```js
useDebounce(() => setDebouncedSearchTerm(searchTerm), 1000, [searchTerm]);
```

`useDebounce` can be added in your project by installing below npm module:

```bash
npm install react-use
```

### Load More Functionality

A simple pagination system using a **Load More button**:

```js
const loadPage = useCallback(async (pageToLoad) => {
  await fetchMovies(
    debouncedSearchTerm,
    pageToLoad,
    setMoviesLoading,
    setMoviesErrorMessage,
    setMovieList
  );
  setPage(prev => (prev === pageToLoad ? pageToLoad + 1 : prev));
}, [debouncedSearchTerm]);
```

UI snippet:
```jsx
<button onClick={() => loadPage(page)}>
    Load More
</button>
```

### Trending Movies with Appwrite
To interact with Appwrite, we use its SDK to create a client, which allows us to communicate with the database.

```js
const client = new Client()
    .setEndpoint('https://cloud.appwrite.io/v1')
    .setProject(PROJECT_ID)

const database = new Databases(client);
```

To enable trending movies, we maintain a search count for each unique search term in an Appwrite document. Whenever a user searches for a movie, we update the corresponding search count.

```js
export const updateSearchCount = async (searchTerm, movie) => {
    try {
        const result = await database.listDocuments(DATABASE_ID, COLLECTION_ID, [
            Query.equal('searchTerm', searchTerm),
        ])

        if (result.documents.length > 0) {
            const doc = result.documents[0];
            await database.updateDocument(DATABASE_ID, COLLECTION_ID, doc.$id, {
                count: doc.count + 1,
            })
        } else {
            await database.createDocument(DATABASE_ID, COLLECTION_ID, ID.unique(), {
                searchTerm: searchTerm,
                count: 1,
                movie_id: movie.id,
                poster_url: `https://image.tmdb.org/t/p/w500${movie.poster_path}`,
            })
        }
    } catch (error) {
        console.log(error);
    }
}
```

In the trending movies section, we can query these documents and retrieve them sorted by their search count.

```js
export const getTrendingMovies = async () => {
    const data = await database.listDocuments(DATABASE_ID, COLLECTION_ID, [
        Query.limit(5),
        Query.orderDesc('count'),
    ]);
    return data.documents;
}
```

To install the Appwrite SDK in your React project, simply add it as an npm module.

```bash
npm install appwrite
```

### External Links
Each movie card links directly to its IMDB page in a new tab:

```jsx
<img src={poster_path ? `https://image.tmdb.org/t/p/w500/${poster_path}` : '/no-movie.png'}
     alt={title}
     onClick={async () => window.open(await fetchExternalLink(id), "_blank")}
     style={{ cursor: "pointer" }}
/>
```

## What I Learned
- Splitting the UI into **modular components** makes React projects easier to read and maintain.
- **Debounce** is essential for smooth API-driven search.
- A **Load More button** is a simple, effective way to handle pagination.
- Even a small backend integration like Appwrite can make a frontend project more practical.  

## Project Link  

[Github Repo](https://github.com/mhaider97/movie-world)  
[Live](https://movie-world-rho.vercel.app/)

## Credits
- **[React Infinite Scroll](https://blog.logrocket.com/react-infinite-scroll/)**  
- **[Appwrite Docs](https://appwrite.io/docs)**  
- **[React Refresher](https://www.youtube.com/watch?v=dCLhUialKPQ&t=4980s&ab_channel=JavaScriptMastery)**
- **[TMDB Docs](https://developer.themoviedb.org/reference/intro/getting-started)**
- **[Debounce](https://github.com/streamich/react-use)**
- **[Public APIs](https://github.com/public-apis/public-apis)**

