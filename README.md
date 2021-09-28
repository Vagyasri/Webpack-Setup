![](https://img.shields.io/badge/Microverse-blueviolet)

# Webpack-Setup
Setting up the Web-pack for the future Projects

- The "source" code is the code that we'll write and edit. The "distribution" code is the minimized and optimized output of our build process that will eventually be loaded in the browser.

## Built With

- HTML
- CSS
- JavaScipt
- Webpack

## Author

👤 **Bhagyashree Patra**

- GitHub: [@Vagyasri](https://github.com/Vagyasri)
- Twitter: [@Vagyasri](https://twitter.com/Vagyasri)
- LinkedIn: [Bhagyashree Patra](https://www.linkedin.com/in/bhagyashree-patra-029bb059/)

## Getting Started

### Prerequisites:

- Web browser
- Code Editor (VS Code)
- Live Server Extension

### Cloning the repo to your local system (If you already have git, installed in your system):

- [Copy this link](https://github.com/Vagyasri/Webpack-Setup.git)
- Open your terminal or command line
- Run "git clone [Paste this link](https://github.com/Vagyasri/Webpack-Setup.git)"
- Open the folder with your code editor
- Now You can edit the code and check the changes in the browser using Live Server

## Steps:

### Basic Setup:

- Initialize `npm`: Run `npm init -y`
- Install `webpack` and  `webpack-cli` locally: Run `npm install webpack webpack-cli --save-dev`
- Run `touch index.html && mkdir src && cd src && touch index.js && cd ..`
- Update `index.html`:

    ```html
    <!DOCTYPE html>
    <html>
    <head>
        <meta charset="utf-8" />
        <title>Getting Started</title>
        <script src="https://unpkg.com/lodash@4.17.20"></script>
    </head>
    <body>
        <script src="./src/index.js"></script>
    </body>
    </html>
    ```

- Update `index.js`:

    ```js
    function component() {
        const element = document.createElement('div');
    
        // Lodash, currently included via a script, is required for this line to work
        element.innerHTML = _.join(['Hello', 'webpack'], ' ');
    
        return element;
    }
    
    document.body.appendChild(component());
    ```

- Update package.json:

    ```diff
    - "main": "index.js",
    + "private": true,
    ```
### Creating a Bundle

- Run `mkdir dist && mv index.html dist`
- Move `dist` out of `gitignore`:
  
  ```diff
  # Nuxt.js build / generate output
    .nuxt
  - dist
  ```

- To bundle the lodash dependency with index.js, install the library locally: Run `npm install --save lodash`
- Import lodash in our script `index.js`:
  
  ```diff
  + import _ from 'lodash';
      ......
  - // Lodash, currently included via a script, is required for this line to work
  + // Lodash, now imported by this script
  ```

- Update `index.html`:
  
  ```diff
  - <script src="https://unpkg.com/lodash@4.17.20"></script>
    </head>
    <body>
  - <script src="./src/index.js"></script>
  + <script src="main.js"></script>
  ```

- For taking our script at `src/index.js` as the entry point, and will generate `dist/main.js` as the output: Run `npx webpack`

### Modules:

- Create and update a configuration File `webpack.config.js`
- Run the build again but instead using our new configuration file: Run `npx webpack --config webpack.config.js`

### NPM Scripts:

- Adjust `package.json` by adding an npm script:

    ```diff
    "scripts": {
    - "test": "echo \"Error: no test specified\" && exit 1"
    + "test": "echo \"Error: no test specified\" && exit 1",
    + "build": "webpack"
    ```
- Check if your script alias works: Run `npm run build`

### Setting up HtmlWebpackPlugin:
  HtmlWebpackPlugin automatically create the index.html file in the /dist directory inorder to avoid the risk of overwritting in the manual creation.

- Install the plugin: Run `npm install --save-dev html-webpack-plugin`
- Adjust the `webpack.config.js` file:

    ```diff
    const path = require('path');
    + const HtmlWebpackPlugin = require('html-webpack-plugin');
    module.exports = {
        entry: {
            index: './src/index.js',
            print: './src/print.js',
        },
    +   plugins: [
    +       new HtmlWebpackPlugin({
    +           title: 'Output Management',
    +       }),
    +   ],
    ```

- Check if your script alias works: Delete all the files from the `/dist directory` and Run:
`npm run build`

### HTML template:

- Run `cd src && touch index.html && cd ..`
- Modify `webpack.config.js` to point HtmlWebpackPlugin towards the template file:
  
  ```diff
    plugins: [
    new HtmlWebpackPlugin({
  -   title: 'Output Management',
  +   template: './src/index.html',
    }),
    ],
  ```
- To update `/dist/index.html`: Run `npm run build`

### Add CSS:
  In order to import a CSS file from within a JavaScript module, you need to install and add the `style-loader` and `css-loader` to your module configuration.

- Install: Run `npm install --save-dev style-loader css-loader`

- Add:

    ```diff
        plugins: [
        new HtmlWebpackPlugin({
        template: './src/index.html',
        }),
    ],
    
    + module: {
    +    rules: [
    +    {
    +        test: /\.css$/i,
    +        use: ['style-loader', 'css-loader'],
    +    },
    +    ],
    + },
    ```

- Create CSS file in the Source dir: Run `cd src && touch style.css && cd ..`
- Import `style.css` into the `index.js`:
  
  ```diff
  + import './style.css';
  ```

- Implement the changes into the distribution dir: Run `npm run build`
  
### Setup local dev server:

- Install Web-pack-dev-server in your local system: Run `npm install --save-dev webpack-dev-server`
- Change your configuration file to tell the dev server where to look for files:

    ```diff
    +    mode: 'development',
        entry: './src/index.js',
    +    devServer: {
    +        static: './dist',
    +    },
        plugins: [
            new HtmlWebpackPlugin({
            template: './src/index.html',
            }),
        ],
        output: {
            filename: 'main.js',
            path: path.resolve(__dirname, 'dist'),
        },
        module: {
    ```

- Add a script to `package.json` in order to run the dev server easily:
  
  ```diff
    "scripts": {
        "test": "echo \"Error: no test specified\" && exit 1",
  +     "start": "webpack serve --open",
        "build": "webpack"
  ```

### Get Live View in Localhost:

- Run: `npm start`

### Check linter errors:

- Install npm
- For HTML: Run npx hint .
- For CSS: Run npx stylelint "**/*.{css,scss}"
- For JS: Run npx eslint .

## 🤝 Contributing

Contributions, issues, and feature requests are welcome!

Start by:

- Forking the project
- Cloning the project to your local machine
- cd into the Youtube-Replica project directory
- Run git checkout -b your-branch-name
- Make your contributions
- Push your branch up to your forked repository
- Open a Pull Request with a detailed description to the development branch of the original project for a review

Feel free to check the [issues page](https://github.com/Vagyasri/Webpack-Setup/issues), contribute to the Project by creating an issue.


## Show your support
Give a ⭐️ if you like this project!
