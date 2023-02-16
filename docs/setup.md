---
title: Setup
layout: page
nav_order: 2
---

# Setup
{: .no_toc}

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
- TOC
{:toc}
</details>

## Creating new project

Om een nieuw project aan te maken ga je naar de map waarin je het project wil hebben. Daar open je de terminal en voer je het volgende commando uit: `laravel new name`, waar `name` de naam van je project is. Daarna open je de map in een editor. Kopieer de .env.example. Hernoem hem niet, maar kopieer hem.

Run daarna de volgende commando's in een terminal:

1. `composer install`
2. `php artisan key:generate`
3. `php artisan migrate`
>Als hij vraagt of je de database aan wil maken, kies dan voor yes.
1. `npm install`
2. `npm run dev`

Klik nu in de terminal op de URL om hem in de browser te openen.

## Tailwind
Om Tailwind te installeren doe je het volgende:

1. Run `npm install -D tailwindcss postcss autoprefixer`
2. Run `npx tailwindcss init -p`
3. Open de `tailwind.config.js`
4. Voeg in het object onderstaand blok toe:
```javascript
  content: [
    "./resources/**/*.blade.php",
    "./resources/**/*.js",
    "./resources/**/*.vue",
  ],
```
5. In `resources/css/app.css`, voeg onderstaande imports toe:
```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```
6. Run `npm run dev`
7. In de layout van de webapp (bijvoorbeeld `resources/views/welcome.blade.php`), voeg onderstaande regel toe in de `<head>`:
```php
@vite(['resources/css/app.css', 'resources/js/app.js'])
```

{::options parse_block_html="true" /}
<details><summary markdown="span">De hele tailwind.config.js:</summary>

```javascript
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: [
    "./resources/**/*.blade.php",
    "./resources/**/*.js",
    "./resources/**/*.vue",
  ],
  theme: {
    extend: {},
  },
  plugins: [],
}

```
</details>
{::options parse_block_html="false" /}


## Bootstrap
Om Bootstrap te installeren doe je het volgende:

1. Run `composer require laravel/ui`
2. Run `php artisan ui bootstrap`
3. Run `npm install`
4. Run `npm install path`
5. Open de `vite.config.js`
6. Voeg bovenaan toe:
```javascript
import path from 'path';
```
7. Voeg in het object onderstaand blok toe:
```javascript
    resolve: {
        alias: {
            '~bootstrap': path.resolve(__dirname, 'node_modules/bootstrap')
        }
    }
```
8. In `resources/js/bootstrap.js`, voeg onderstaande imports toe:
```javascript
import '../sass/app.scss';
import 'bootstrap';
```
9. In de layout van de webapp (bijvoorbeeld `resources/views/welcome.blade.php`), voeg onderstaande regel toe in de `<head>`:
```php
@vite(['resources/css/app.css', 'resources/js/app.js'])
```

{::options parse_block_html="true" /}
<details><summary markdown="span">De hele vite.config.js:</summary>

```javascript
import { defineConfig } from 'vite';
import laravel from 'laravel-vite-plugin';
import path from 'path';

export default defineConfig({
    plugins: [
        laravel({
            input: [
                'resources/sass/app.scss',
                'resources/js/app.js',
            ],
            refresh: true,
        }),
    ],
    resolve: {
        alias: {
            '~bootstrap': path.resolve(__dirname, 'node_modules/bootstrap')
        }
    }
});
```
</details>
{::options parse_block_html="false" /}

## Breeze
Om Breeze te installeren run je de volgende commando's:

1. `composer require laravel/breeze --dev`
2. `php artisan breeze:install`
3. `php artisan migrate`
4. `npm install`
5. `npm run dev`

