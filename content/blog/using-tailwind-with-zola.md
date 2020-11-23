+++
title = "Using Tailwind CSS with Zola"
date = 2020-11-22
+++

This post is written listening to [Népal](https://fr.wikipedia.org/wiki/Népal_(rappeur)).

Our website at [clic2000](https://clic2000.fr) is pure handcoding in HTML/SASS/JS, no
[CMS](https://en.wikipedia.org/wiki/Content_management_system), no static site generator. We like it, it is easy
to understand, secure and fast. We just need to pull the content on our server and compile the SASS files *et
voilà*. However we have to admit that editing HTML while adding content is not ideal.
In recent discussions we decided to give a try to static site generators.

In a near future we would like to
add a blog to our website. Also one redondant task is to had words about our recents works on our references
page. Keeping editing HTML and managing files would be painfull and time consuming. We use markdown on a daily
basis on our notes, our internal doc and GitHub, using it for our website would be a real plus. We
also like the idea to separate structure from content. 

[Mathilde](https://mental.af) uses
it for her personal homepage and [this article](https://blog.gelez.xyz/presentation-zola/) made us decide to
use [Zola](https://www.getzola.org). It is written in Rust, it comes in a single binary and has nice features
like Sass compilation or syntax highlighting. It uses [Tera](https://tera.netlify.app) template engine, which
I haven't tried to the fullest but the `include` feature is something we miss in our actual website.

Before working on clic2000 website I decided to build this little piece of internet and 
this is how I managed configuring Zola using [Tailwind
CSS](https://tailwindcss.com). It is based on [this great post](https://tailwindcss.com) exept it uses
`postcss-cli` instead of `parcel` to compile the styles of the website.

You need Zola and npm installed on your computer and you are ready to go.

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

Add this content to your `styles.css` file :

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

Now configure PostCSS to compile your CSS files. In `package.json` : 

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

You can now work on your theme, just run `zola serve` and `npm run watch:css` in two terminal tabs.

Run `npm run build:css` before production.

