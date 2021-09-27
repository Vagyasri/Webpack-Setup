# Webpack-Setup
Setting up the Web-pack for the future Projects

Steps:

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
-     