+++
title = "Using Tailwind CSS with Zola"
date = 2020-11-22
+++

This article is written listening to [Népal](https://fr.wikipedia.org/wiki/Népal_(rappeur))

## Setup

Create the directory structure of Zola :

```bash
zola init
```

Create `package.json` file and install packages : 

```bash
npm init
npm install tailwindcss postcss postcss-cli autoprefixer
```

Create `styles` folder and `styles.css` file :

```bash
mkdir styles
cd styles
touch styles.css
```

Add this content to our `styles.css` file :

```bash
@tailwind base;
@tailwind components;
@tailwind utilities;
```

Configure PostCSS to use Tailwind plugin. Add this content at the root of the project in `postcss.config.js` file :

```bash
module.exports = {
  plugins: {
    tailwindcss: {},
    autoprefixer: {},
  }
}
```

Now configure PostCSS to compile our CSS files. In `package.json` : 

```bash
"scripts": {
  "watch:css": "postcss styles/styles.css -o static/styles.css -w",
  "build:css": "postcss styles/styles.css -o static/style.css"
}
```
## Templates

Add the following to your templates : 

```html
{% block css %}
	      <link rel="stylesheet" href="{{ get_url(path="styles.css", trailing_slash=false) | safe }}">
{% endblock css %}
```

## Run 

You can now run `zola serve` and `npm run watch:css` in two terminal tabs.

Run `npm run build:css` before production.

