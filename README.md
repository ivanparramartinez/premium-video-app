# Premium Video

Premium Video is a Vue.js application that allows you to search for movies using the OMDB API. You can add movies to a
shopping cart, specify the date and quantity, and view basic information about each movie, such as the title, year,
type, and poster.

## Features

<ol>
<li>Movie Search: Enter a movie title and retrieve corresponding results from the OMDB API.</li>     
<li>Information Display: Get basic details about each movie, including the title, year, type, and poster.</li>     
<li>Add to Shopping Cart: Select movies for rental or purchase and add them to the shopping cart.</li>
<li>Date and Quantity Customization: Specify the desired date and quantity for each movie in the shopping cart.</li>     
<li>Payment Process: Complete the payment for the selected movies and finalize the transaction.</li>
</ol>

## Recommended IDE Setup

[VSCode](https://code.visualstudio.com/) + [Volar](https://marketplace.visualstudio.com/items?itemName=Vue.volar) (and
disable
Vetur) + [TypeScript Vue Plugin (Volar)](https://marketplace.visualstudio.com/items?itemName=Vue.vscode-typescript-vue-plugin).

## Usage

<ol>
<li>Clone the repository: git clone </li>
<li>Install the dependencies: npm install</li>
<li>Start the application: npm run dev</li>
<li>Open your web browser and go to: http://localhost:5173</li>
<li>Use the search bar to search for movies by title.</li>
<li>Click on a movie to view more details.</li>
<li>Add movies to the shopping cart by specifying the desired date and quantity.</li>
<li>Proceed to the checkout process and finalize the transaction.</li>
</ol>

## Customize configuration

See [Vite Configuration Reference](https://vitejs.dev/config/).

## Project Setup

```sh
npm install
```

### Compile and Hot-Reload for Development

```sh
npm run dev
```

### Compile and Minify for Production

```sh
npm run build
```

### Lint with [ESLint](https://eslint.org/)

```sh
npm run lint
```

## Known Issues

    Sometimes, the OMDB API may return inaccurate or incomplete results due to the quality of the provided data. Please be aware of this limitation when using the application.

## License

The Premium Video project is distributed under the MIT License. See the LICENSE file for more information.
