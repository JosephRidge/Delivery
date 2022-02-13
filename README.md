# Vue 3 + Vite

This template should help get you started developing with Vue 3 in Vite. The template uses Vue 3 `<script setup>` SFCs, check out the [script setup docs](https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup) to learn more.

## Recommended IDE Setup

- [VSCode](https://code.visualstudio.com/) + [Volar](https://marketplace.visualstudio.com/items?itemName=johnsoncodehk.volar)


## Adding firebase to Appplication 

```npm install firebase```

## Tailwind

```npm install -D tailwindcss postcss autoprefixer && npx tailwindcss init -p```


in the `tailwind.config.js` file alter it to this: 
module.exports = {
  content: [
    "./index.html",
    "./src/**/*.{vue,js,ts,jsx,tsx}",
  ],
  theme: {
    extend: {},
  },
  plugins: [],
}

Create the css file in your src/style directory then add : 
```
@tailwind base;
@tailwind components;
@tailwind utilities; ```

import it in your Main.js

```
import './style/index.css'```