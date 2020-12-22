# Getting Started with tailwindcss

This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app).

## Create React App (CRA) Setup

This setup uses the TypeScript template and `npm` as the package manager. If you prefer not to use TypeScript, simply leave out the flag. Similarly, if you prefer to stick to `yarn` as your package manager then remove `--use-npm`.

Otherwise, just run this command calling your project whatever you want

`npx create-react-app [PROJECTNAME] --template typescript --use-npm`

Once your project has been set up feel free to delete any unwanted files that CRA generates for you.

## Tailwind Setup

These instructions are taken from the official tailwindcss documentation, which you can access [here](https://tailwindcss.com/docs/installation).

### Step 1

This project uses CRA v4.0.1 which doesn't yet support PostCSS 8. Therefore, the following compatibility build is necessary:

`npm i tailwindcss@npm:@tailwindcss/postcss7-compat @tailwindcss/postcss7-compat postcss@^7 autoprefixer@^9`

### Step 2

Since CRA doesn't let you override the PostCSS configuration natively, you also need to install CRACO to be able to configure Tailwind:

`npm i @craco/craco`

Replace the `start`, `build` and `test` scripts inside `package.json`:

```json
{
    // ...
    "scripts": {
        "start": "craco start",
        "build": "craco build",
        "test": "craco test",
        "eject": "react-scripts eject"
    }
}
```

Find out more about CRACO [here](https://github.com/gsoft-inc/craco).

### Step 3

Next, create a `craco.config.js` at the root of your project and add the tailwindcss and autoprefixer as PostCSS plugins:

```javascript
// craco.config.js
module.exports = {
    style: {
        postcss: {
            plugins: [require('tailwindcss'), require('autoprefixer')],
        },
    },
}
```

### Step 4

Next, generate your `tailwind.config.js` file by running `npx tailwindcss init`

### Step 5

In your newly generated `tailwind.config.js` configure the purge option with the paths to all of your components so Tailwind can tree-shake unused styles in production builds. Your file should look like this:

```javascript
// tailwind.config.js
module.exports = {
    purge: ['./src/**/*.{js,jsx,ts,tsx}', './public/index.html'],
    darkMode: false, // or 'media' or 'class'
    theme: {
        extend: {},
    },
    variants: {
        extend: {},
    },
    plugins: [],
}
```

### Step 6

Open the `./src/index.css` file that CRA generates for you by default and use the @tailwind directive to include Tailwind's base, components, and utilities styles, replacing the original file contents:

```css
/* ./src/index.css */
@tailwind base;
@tailwind components;
@tailwind utilities;
```

### Step 7

Finally, ensure your CSS file is being imported in your `./src/index.js` file:

```javascript
// src/index.js
import React from 'react'
import ReactDOM from 'react-dom'
import './index.css'
import App from './App'
import reportWebVitals from './reportWebVitals'

ReactDOM.render(
    <React.StrictMode>
        <App />
    </React.StrictMode>,
    document.getElementById('root')
)

// ...
```

## Setup complete!

That's it! You can now start your app with `npm run start`.
