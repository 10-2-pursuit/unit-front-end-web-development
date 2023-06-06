# Request-response Cycle & API Calls with Postman

## Learning Objectives

By the end of this lesson you should be able to:

- Identify key components of the internet, including browser, servers, and databases.
- Describe the request-response cycle and how it relates to server architecture.
- Describe what is an API
- Use Postman to make GET requests to a public API.
- Identify the four main parts of an HTTP request.
- Identify the three main parts of an HTTP response.
- Identify different types of data that can be used in a response.

---

## Guiding questions

- What is a software program?

- What does it mean to "run" a program?

- A browser is a program on your computer. What is the job of this program?

- This website is being rendered thanks to HTML, CSS, and JavaScript. Where does that HTML, CSS, and JavaScript come from?

- Your browser makes a request whenever you go to a URL. What is a URL?

- Take a look at the following URL below. Then, describe each part of the URL.

  ```
  https://www.google.com/search?q=pursuit+nyc
  ```

- What is a server's job?

- Whenever a server needs to store or retrieve data, it makes a request to a database. What is the role of the database?

- What is the request-response cycle?

- Describe the different types of request that are made when you order a product on a website. (Feel free to refer to the reading!)

- Based on what you know, make a guess as to the different types of requests that occur when you make a search on Google.

- What is a web API?

- What is JSON?

- What does it mean for a server to be a JSON web API?

- Open up the Postman application. How can you create a new request in Postman?

- Is Postman a client or a server? How do you know?

- What are the four components of an HTTP request? Describe each and identify where they can be found in Postman.

- The [api.citybik.es](http://api.citybik.es/v2/) API is a free API you can access by making a request to the following URL. It will return information about different city bike networks around the world.

  ```
  http://api.citybik.es/v2/networks
  ```

  Try making a request to the API. Was the request successful? How do you know?

- What data type did the server respond with? How do you know?

- What was the status code of the response. How do you know?

- APIs often have multiple URLs that can be accessed. For example, this API allows for request a single network, as opposed to multiple, via the following URL.

  ```
  http://api.citybik.es/v2/networks/{networkId}
  ```

  Replace `{networkId}` with one of the IDs you received from your first request. How does this response differ from the response you received earlier?

- Another API is the free Star Wars API, also known as [SWAPI](https://www.swapi.tech/).

  Some APIs have better documentation than others. Take a bit of time to look through the websites and see if you can make the following requests:

  - Request all films.
  - Request the person with an ID of `11`.
  - Request the starship with an ID of `9`.
