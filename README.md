#### Design Files

<details>
<summary>Figma Designs</summary>

- You can check the **Design Files** for different devices <a href="https://www.figma.com/file/T8BdpViEZL6DhFxu0HlEPY/Book-Hub?node-id=0%3A1" target="_blank">here</a>.

</details>

### Set Up Instructions

<details>

<summary>Click to view</summary>

- Download dependencies by running `npm install`
- Start up the app using `npm start`

</details>

### Instructions

<details>

<summary>Functionalities added</summary>
<br/>
The website has the following functionalities

- **Login Route**

  - When the invalid username and password are provided and the **Login** button is clicked, then the respective error message received from the response should be displayed
  - When the valid username and password are provided and the **Login** button is clicked, then the page should be navigated to the Home Route
  - When an _unauthenticated_ user tries to access the Home, Bookshelves and Book Details Route, then the page should be navigated to the Login Route
  - When an _authenticated_ user tries to access the Home, Bookshelves and Book Details Route, then the page should be navigated to the respective route
  - When an _authenticated_ user tries to access the Login Route, then the page should be navigated to the Home Route

- **Home Route**

  - When an _authenticated_ user opens the Home Route,

    - An HTTP GET request should be made to **Top Rated Books API URL** with `jwt_token` in the Cookies

      - **_Loader_** should be displayed while fetching the data
      - After the data is fetched successfully, display the list of top rated books received from the response
      - If the HTTP GET request made is unsuccessful, then the failure view given in the **Figma** screens should be displayed

        - When the **Try Again** button is clicked, an HTTP GET request should be made to **Top Rated Books API URL**

      - When the **Find Books** button is clicked, then the page should be navigated to the Bookshelves Route
      - When a **book item** is clicked, then the page should be navigated to the Book Details Route

    - **Header**  
    
      - When the **Book Hub logo** in the header is clicked, then the page should be navigated to the Home Route
      - When the **Home** link in the header is clicked, then the page should be navigated to the Home Route
      - When the **Bookshelves** link in the header is clicked, then the page should be navigated to the Bookshelves Route
      - When the **Logout** button in the header is clicked, then the page should be navigated to the Login Route

- **Bookshelves Route**

  - When an _authenticated_ user opens the Bookshelves Route

    - An HTTP GET request should be made to **Books API URL** with `jwt_token` in the Cookies and query parameters `shelf` and `search` with initial values as `ALL` and empty string respectively

      - The page should initially consist of **All Books** heading
      - **_Loader_** should be displayed while fetching the data
      - After the data is fetched successfully, display the list of books received from the response
      - If the HTTP GET request made is unsuccessful, then the failure view given in the **Figma** screens should be displayed

        - When the **Try Again** button is clicked, an HTTP GET request should be made to **Books API URL**

      - When a button in the **bookshelves** is clicked (Use the bookshelvesList data provided in the App.js to render Bookshelves),

        - The **All Books** heading changed to **{bookshelf name} Books**. Here the bookshelf name refers to the clicked bookshelf label from the provided `bookshelvesList`
        - Make an HTTP GET request to the **Books API URL**  with `jwt_token` in the Cookies and query parameter `shelf` with value as the value of the clicked bookshelf from the provided `bookshelvesList`
        - **_Loader_** should be displayed while fetching the data
        - After the data is fetched successfully, display the list of books received from the response

      - When a non-empty value is provided in the search input and the search icon button is clicked

        - Make an HTTP GET request to the **Books API URL** with `jwt_token` in the Cookies and query parameter `search` with value as the text provided in the search input
        - **_Loader_** should be displayed while fetching the data
        - After the data is fetched successfully, display the list of books received from the response

      - When the HTTP GET request made to the **Books API URL** returns an empty list for books, then the **No Books View** should be displayed as shown in the Figma

  - When multiple filters are applied, then the HTTP GET request should be made with all the filters that are applied

    - For example: When the **Read** bookshelf is clicked and search input value is **Speak**, then the **Books API URL** will be as follows

      ```js
      const apiUrl = 'https://apis.ccbp.in/book-hub/books?shelf=READ&search=Speak'
      ```

  - When a **book** item is clicked, then the page should be navigated to the Book Details Route
  - All the header functionalities mentioned in the Home Route should work in this route accordingly

- **Book Details Route**

  - When an _authenticated_ user opens the Book Details Route

    - An HTTP GET request should be made to **Book Details API URL** with `jwt_token` in the Cookies and book `id` as path parameter
      - **_Loader_** should be displayed while fetching the data
      - After the data is fetched successfully, book details received from the response should be displayed
    - If the HTTP GET request made is unsuccessful, then the failure view given in the **Figma** screens should be displayed
      - When the **Try Again** button is clicked, an HTTP GET request should be made to **Book Details API URL**

  - All the header functionalities mentioned in the Home Route should work in this route accordingly

- **Not Found Route**

  - When a random path is provided as the URL path, then the page should be navigated to the Not Found Route

- Users should be able to view the website responsively in mobile view, tablet view as well

- The App is provided with `bookshelvesList`. It consists of a list of bookshelf objects with the following properties in each bookshelf object

  |  Key  | Data Type |
  | :---: | :-------: |
  |  id   |  String   |
  | value |  String   |
  | label |  String   |

</details>

### Quick Tips

<details>

<summary>Tips</summary>

- Third party packages to be used to achieve the design or functionality

  - React Slick

    - React Slick <a href="https://react-slick.neostack.com/docs/get-started" target="_blank">Documentation</a>
    - React Slick implementation <a href="https://codesandbox.io/s/react-slick-demo-iz90x?file=/src/components/ReactSlick/index.js" target="_blank">CodeSandbox</a>
    - Update the CSS accordingly to style the React Slider and arrow buttons, you can check the <a href="https://codesandbox.io/s/react-slick-demo-iz90x?file=/src/components/ReactSlick/index.css" target="_blank">CodeSandbox</a>
    - Add the below CDN links in your `public > index.html` file for CSS and Font, you can check the <a href="https://codesandbox.io/s/react-slick-demo-iz90x?file=/public/index.html" target="_blank">CodeSandbox</a> for adding below lines

    ```jsx
    <link rel="stylesheet" type="text/css" charset="UTF-8" href="https://cdnjs.cloudflare.com/ajax/libs/slick-carousel/1.6.0/slick.min.css" />
    <link rel="stylesheet" type="text/css" href="https://cdnjs.cloudflare.com/ajax/libs/slick-carousel/1.6.0/slick-theme.min.css" />
    ```

</details>

### Important Note

<details>
<summary>Routes</summary>

- **Routes**

  - Render `Login` Route component when the path in URL matches `/login`
  - Render `Home` Route component when the path in URL matches `/`
  - Render `Bookshelves` Route component when the path in URL matches `/shelf`
  - Render `Book Details` Route component when the path in URL matches `/books/:id`

- Wrap the `Loader` component with an HTML container element and add the `testid` attribute value as **loader** to it

  ```jsx
  <div className="loader-container" testid="loader">
    <Loader type="TailSpin" color="#0284C7" height={50} width={50} />
  </div>
  ```

- **Bookshelves Route**
  - `BsSearch` icon from react-icons should be used for the **Search Icon** button
  - `BsFillStarFill` icon from react-icons should be used for the **star** image
  
- **BookDetails Route**

  - `BsFillStarFill` icon from react-icons should be used for the **star** image

- **Footer**

  - `FaGoogle` icon from react-icons should be used for the **Google Icon** button in Footer
  - `FaTwitter` icon from react-icons should be used for the **Twitter Icon** button in Footer
  - `FaInstagram` icon from react-icons should be used for the **Instagram Icon** button in Footer
  - `FaYoutube` icon from react-icons should be used for the **Youtube Icon** button in Footer

</details>

### Resources

<details>
<summary>Data fetch URLs</summary>

- **Note:** Use the below sample code snippet to make a POST request on Login using valid username and password.

  ```js
  const options = {
    method: 'POST',
    body: JSON.stringify(userDetails),
  }
  ```

**Login API**

#### URL: `https://apis.ccbp.in/login`

#### Method: `POST`

#### Description:

Returns a response based on the credentials provided

#### Sample request object:

```json
{
  "username": "rahul",
  "password": "rahul@2021"
}
```

#### Sample Success Response

```json
{
  "jwt_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InJhaHVsIiwicm9sZSI6IlBSSU1FX1VTRVIiLCJpYXQiOjE2MTk2Mjg2MTN9. nZDlFsnSWArLKKeF0QbmdVfLgzUbx1BGJsqa2kc_21Y"
}
```

#### Sample Failure Response

```json
{
  "status_code": 404,
  "error_msg": "Username is not found"
}
```

**Top Rated Books API**

#### URL: `https://apis.ccbp.in/book-hub/top-rated-books`

#### Method: `GET`

#### Description:

Returns a response containing the list of 10 top rated books

#### Sample Response

```json
{
  "books": [
    {
      "id": "561d0af9-3cec-426d-9721-35ed8d7e9c3c",
      "author_name": "Chetan Bhagat",
      "cover_pic": "https://assets.ccbp.in/frontend/react-js/half-girlfriend-book.png",
      "title": "Half Girlfriend"
    },
    {
      "id": "5f7fe73a-c4f2-4d58-b4ad-ec88426e26be",
      "author_name": "Robert Kiyosaki",
      "cover_pic": "https://assets.ccbp.in/frontend/react-js/rich-dad-poor-dad-book.png",
      "title": "Rich Dad Poor Dad"
    },
    ...
  ],
  "total": 10
}
```

**Books API**

#### URL: `https://apis.ccbp.in/book-hub/books?shelf={bookshelfName}&search={searchText}`

#### Example: `https://apis.ccbp.in/book-hub/books?shelf=Read&search=Luke`

#### Method: `GET`

#### Description:

Returns a response containing the list of books based on the query parameters

#### Sample Response

```json
{
  "books": [
    {
      "id": "54402549-a4bd-4c99-a176-bd795d47173a",
      "title": "One life one chance",
      "read_status": "Read",
      "rating": 4.2,
      "author_name": "Luke Richmond",
      "cover_pic": "https://assets.ccbp.in/frontend/react-js/one-life-one-chance-book.png"
    },
    ...
  ],
  "total": 10
}
```

**Book Details API**

#### URL: `https://apis.ccbp.in/book-hub/books/{bookId}`

#### Example: `https://apis.ccbp.in/book-hub/books/7850622e-1b70-4396-963d-e68d5a2577d7`

#### Method: `GET`

#### Description:

Returns a response containing book details

#### Sample Response

```json
{
  "book_details": {
    "id": "7850622e-1b70-4396-963d-e68d5a2577d7",
    "author_name": "Ady Barkan",
    "cover_pic": "https://assets.ccbp.in/frontend/react-js/eyes-to-the-wind-book.png",
    "about_book": "Eyes to the Wind is a rousing memoir featuring intertwining storylines about determination, perseverance, and how to live a life filled with purpose and intention.",
    "rating": 4.8,
    "read_status": "READ",
    "title": "Eyes to the Wind",
    "about_author": "Ady Barkan is an American lawyer and liberal activist. He is a co-founder of the Be a Hero PAC and is an organizer for the Center for Popular Democracy, where he led the Fed Up campaign."
  }
}
```

</details>

### User Credentials

<details>
<summary>Click to view user credentials</summary>

<br/>

**You can use any one of the following credentials**

```text
  username: aakash
  password: sky@007
```

```text
  username: agastya
  password: myth#789
```

```text
  username: advika
  password: world@5
```

```text
  username: binita
  password: modest*6
```

```text
  username: chetan
  password: vigor$life
```

```text
  username: deepak
  password: lightstar@1
```

```text
  username: harshad
  password: joy@85
```

```text
  username: kapil
  password: moon$008
```

```text
 username: rahul
 password: rahul@2021
```

```text
  username: shravya
  password: musical#stone
```

```text
  username: saira
  password: princess@9
```

<br/>
</details>

