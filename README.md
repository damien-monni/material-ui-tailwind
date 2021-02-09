# Using Tailwind CSS theme with Material-UI

This is POC of using Tailwind CSS with Material-UI.

The idea is to sync MUI theme with Tailwind CSS theme.
To do that, we need to get tailwind theme from the MUI theme
creation function to inject Tailwind value into the MUI theme
properties.

- Install MUI
- Follow the Tailwind install guide for Create React App using Craco
- `tailwind.config.js` needs to be in the `./src` folder to be imported
  into the React App and MUI theme. To do that, edit `craco.config.js` to:

```js
module.exports = {
  style: {
    postcss: {
      plugins: [
        require("tailwindcss")("./src/tailwind.config.js"),
        require("autoprefixer"),
      ],
    },
  },
};
```

⚠️ Notice the tailwind.config.js path after requiring tailwindcss.

- Use tailwind resolveConfig utility to get the entire tailwind theme
  and inject it into MUI:

```js
// ./src/App.js
const tailwindConfig = resolveConfig(tailwindConfigModule);

const theme = createMuiTheme({
  palette: {
    primary: {
      main: tailwindConfig.theme.colors.primary.main,
    },
  },
});
```
