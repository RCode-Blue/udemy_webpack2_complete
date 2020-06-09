<h1>Create React from Scratch Using WebPack</h1>

<h2>Basic Setup:</h2>

<h3>0. Summary Info</h3>

| file / folder         | description |
| --------------------- | ----------- |
| webpack output folder | build       |
| webpack output file   | bundle.js   |
| code folder           | src         |

<br/><br/>
<h3>1. Initialise the project using the `npm init` command</h3>

   * creates a package.json file




<br/><br/>
<h3>2. Create files and folders</h3>
   
   Create a folder named `public`
   * Handles any static assets
   

   Create a folder named `src`
   * This is where your code is located


   Create the HTML file
   * Inside the `src` folder, create a file named `index.html`. [sample](#HtmlSample)
   * Inside the `index.html`, include the output js file in the `<script>` section:
     
     `<script src="../dist/bundle.js"></script>`


<br/><br/>
<h3>3. Setup Babel for the development environment</h3>
<h4>3.1  Install Babel</h4>

  Type the following commands:

`npm install --save-dev @babel/core@7.1.0`<br/>
`npm install --save-dev @babel/cli@7.1.0 `<br/>
`npm install --save-dev @babel/preset-env@7.1.0`<br/>
`npm install --save-dev @babel/preset-react@7.0.0`<br/>
  

Where:

| Package        | Usage                                                       |
| -------------- | ----------------------------------------------------------- |
| `babel-core`   | The main babel package                                      |
| `babel-cli`    | Allows you to compiule files from the command line          |
| `preset-env`   | Allows us to transform ES6 to traditional javascript        |
| `preset-react` | Allows transformation of JSX to traditional javascript code |



<h4>3.2  In the project root, create the `.babelrc` configuration file.</h4>




<br/><br/>
<h3>4. Install  Webpack</h3>
<h4>4.1 Install the following:</h4>

  `npm install --save-dev webpack@4.19.1`<br/>
  `npm install --save-dev webpack-cli@3.1.1`<br/>
  `npm install --save-dev webpack-dev-server@3.1.8`<br/>
  `npm install --save-dev style-loader@0.23.0`<br/>
  `npm install --save-dev css-loader@1.0.0`<br/>
  `npm install --save-dev babel-loader@8.0.2`<br/>

<h4>4.2 Create the webpack configuration file</h4>

In the project root, create a file called `webpack.config.js`.

<br/><br/>
<h3>5. Configure Webpack</h3>
   
<h4>5.1 Set up basic configuration:</h4>

Add the following in the `webpack.config.js` file:

  ```
  const config = {

  };
  module.exports = config;
  ```

<h4>5.2 Entry point:</h4>

  ```
const config = {
  entry: './src/index.js',
  ```
<h4>5.3 Output property:</h4>

```
output: {
    path: path.resolve(__dirname, "dist/"),
    publicPath: "/dist/",
    filename: "bundle.js"
}
```


<br/><br/>

<h3>6. Include webpack in the package.json file</h3>

In the `package.json` file, add a scripts section and add webpack to it:

```
"scripts":{
  "build": "webpack"
}
```


<br/><br/>
<h3>7. Run Webpack to Test</h3>

`npm run build`

You will see the resulting `bundle.js` file in the `/dist` folder


<br/><br/>
<h2>Babel Setup for Development Environment</h2>

<br/><br/>
<h3>8. Install Babel</h3>

`npm install --save-dev babel-loader`
`npm install --save-dev babel-core`
`npm install --save-dev babel-preset-env`

| Loader           | Notes                                                                    |
| ---------------- | ------------------------------------------------------------------------ |
| babel-loader     | Teaches babel how to work with webpack                                   |
| babel-core       | Core babel library. Parses code, generates output files                  |
| babel-preset-env | Ruleset for telling babel what to look for and how to change to ES5 code |


<br/><br/>
<h3>9. Configure webpack module for Babel</h3>

In `webpack.config.js`, add a module section:

```
module: {
  rules: [
    {
      use: 'babel-loader',
      test: /\.js$/        // apply babel only to *.js files
    }
  ]
}
```

<br/><br/>
<h3>10. Configure Babel</h3>

In the project root, create a file called `.babelrc`.

Edit the file as follows:

```
{
  "presets": ["babel-preset-env"]
}
```



<br/><br/>
<h3>11. Test Babel configuration</h3>

run `npm run build`

Check that the code works.



<br/><br/>
<h3>12. CSS Loader</h3>

`npm install --save-dev style-loader`<br/>
`npm install --save-dev css-loader`



In `webpack.config.js` file, add another node to the `rules` section:

```
{
  use: ['style-loader, 'css-loader'],
  test: /\.css$/
}
```

run `npm run build` to confirm it's working


<br/><br/>
<h3></h3>


<br/><br/>
<h3></h3>


<br/><br/><br/><br/>
---------------------------------------

<h2>References</h2>


1. Sample <a id="HtmlSample">`index.html`</a> file

```
<!DOCTYPE html>
<html>

<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
  <title>React Starter</title>
</head>

<body>
  <div id="root"></div>
  <noscript>
    You need to enable JavaScript to run this app.
  </noscript>
  <script src="../dist/bundle.js"></script>
</body>

</html>
```

2. Sample `.babelrc` file:
```
{
  "presets": ["@babel/env", "@babel/preset-react"]
}
```

3. Sample `webpack.config.js` file:
```
const path = require("path");
const webpack = require("webpack");

module.exports = {
  entry: "./src/index.js",
  mode: "development",
  module: {
    rules: [
      {
        test: /\.(js|jsx)$/,
        exclude: /(node_modules|bower_components)/,
        loader: "babel-loader",
        options: { presets: ["@babel/env"] }
      },
      {
        test: /\.css$/,
        use: ["style-loader", "css-loader"]
      }
    ]
  },
  resolve: { extensions: ["*", ".js", ".jsx"] },
  output: {
    path: path.resolve(__dirname, "dist/"),
    publicPath: "/dist/",
    filename: "bundle.js"
  },
  devServer: {
    contentBase: path.join(__dirname, "public/"),
    port: 3000,
    publicPath: "http://localhost:3000/dist/",
    hotOnly: true
  },
  plugins: [new webpack.HotModuleReplacementPlugin()]
};
```