# Webpack-Setup
Setting up the Web-pack for the future Projects

- The "source" code is the code that we'll write and edit. The "distribution" code is the minimized and optimized output of our build process that will eventually be loaded in the browser.

### Steps:

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
    </html>```

- Update `index.js`:

    ```js
    function component() {
        const element = document.createElement('div');
    
        // Lodash, currently included via a script, is required for this line to work
        element.innerHTML = _.join(['Hello', 'webpack'], ' ');
    
        return element;
    }
    
    document.body.appendChild(component());```

- Update package.json:

    ```diff
    - "main": "index.js",
    + "private": true,
    ```

- Run `mkdir dist && mv index.html dist`
- Move `dist` out of `gitignore`:
  
  ```diff
  # Nuxt.js build / generate output
    .nuxt
  - dist
  ```

- To bundle the lodash dependency with index.js, install the library locally: Run `npm install --save lodash`
- Import lodash in our script `index.js`:
  
  ```js
   + import _ from 'lodash';
      ......
   - // Lodash, currently included via a script, is required for this line to work
   + // Lodash, now imported by this script
  ```

- Update `index.html`:
  
  ```html
   - <script src="https://unpkg.com/lodash@4.17.20"></script>
    </head>
    <body>
   - <script src="./src/index.js"></script>
   + <script src="main.js"></script>
  ```

- For taking our script at `src/index.js` as the entry point, and will generate `dist/main.js` as the output: Run `npx webpack`

- Create a configuration File `webpack.config.js`
- 