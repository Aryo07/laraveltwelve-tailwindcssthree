<p align="center">
  <a href="https://laravel.com" target="_blank">
    <img src="https://raw.githubusercontent.com/laravel/art/master/logo-lockup/5%20SVG/2%20CMYK/1%20Full%20Color/laravel-logolockup-cmyk-red.svg" width="400" alt="Laravel Logo">
  </a>
</p>

<h1 align="center">Integrating TailwindCSS v3 with Laravel 12</h1>

This guide describes how to configure **TailwindCSS v3** in a fresh **Laravel 12** project.  
By default, Laravel ships with Vite, so we will configure TailwindCSS properly to work with it.

---

## Step 1 – Remove the Tailwind Vite plugin
If `@tailwindcss/vite` is already installed, uninstall it first:

```bash
npm remove @tailwindcss/vite
```

---

## Step 2 – Configure Vite
Update your `vite.config.js` so it only loads Laravel’s plugin:

```js
import { defineConfig } from 'vite';
import laravel from 'laravel-vite-plugin';

export default defineConfig({
    plugins: [
        laravel({
            input: ['resources/css/app.css', 'resources/js/app.js'],
            refresh: true,
        }),
    ],
});
```

---

## Step 3 – Install TailwindCSS v3
Uninstall any existing TailwindCSS version, then install **TailwindCSS v3** along with the forms plugin:

```bash
npm remove tailwindcss
npm install -D tailwindcss@3 @tailwindcss/forms
npx tailwindcss init
```

---

## Step 4 – Tailwind Configuration
Update `tailwind.config.js` to scan Blade, Vue, and JS files:

```js
import defaultTheme from 'tailwindcss/defaultTheme';
import forms from '@tailwindcss/forms';

/** @type {import('tailwindcss').Config} */
export default {
    content: [
        './vendor/laravel/framework/src/Illuminate/Pagination/resources/views/*.blade.php',
        './storage/framework/views/*.php',
        './resources/**/*.blade.php',
        './resources/**/*.js',
        './resources/**/*.vue',
    ],
    theme: {
        extend: {
            fontFamily: {
                sans: ['Figtree', ...defaultTheme.fontFamily.sans],
            },
        },
    },
    plugins: [forms],
};
```

---

## Step 5 – PostCSS & Autoprefixer
Install PostCSS and Autoprefixer:

```bash
npm install -D postcss autoprefixer
```

Then create a `postcss.config.js` file in the root of your project:

```js
export default {
    plugins: {
        tailwindcss: {},
        autoprefixer: {},
    },
};
```

---

## Step 6 – Add Tailwind Directives to CSS
Inside your main CSS file (usually `resources/css/app.css`), add:

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

---

## Step 7 – Build Your Assets
Finally, build your assets:

```bash
npm run build
```

TailwindCSS v3 is now ready to use with Laravel 12 🎉

---

## Optional – Try TailwindCSS v4 (Experimental)

### Step 1 – Remove the Tailwind Vite plugin
If `@tailwindcss/vite` is already installed, uninstall it:

```bash
npm remove @tailwindcss/vite
```

### Step 2 – Configure Vite
Update `vite.config.js` so it only loads Laravel’s plugin:

```js
import { defineConfig } from 'vite';
import laravel from 'laravel-vite-plugin';

export default defineConfig({
    plugins: [
        laravel({
            input: ['resources/css/app.css', 'resources/js/app.js'],
            refresh: true,
        }),
    ],
});
```

### Step 3 – Install TailwindCSS v4
If you want to experiment with TailwindCSS v4 and PostCSS:

```bash
npm install -D @tailwindcss/postcss
```

### Step 4 – PostCSS Configuration
Update your `postcss.config.js`:

```js
export default {
    plugins: {
        '@tailwindcss/postcss': {},
    },
};
```

> Note: Tailwind v4 introduces a CSS-based configuration model and does not use `tailwind.config.js`.

---
