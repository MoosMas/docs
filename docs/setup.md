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

## Nieuw project aanmaken
Om een nieuw project aan te maken voer je onderstaande stappen uit:

1. Ga naar de map waarin je het project wil hebben
2. Run `laravel new name` waar `name` de naam van je project is
3. Open de map in een editor
4. Kopieer de .env.example naar .env

    {: .important }
    Hernoem de .env.example niet, maar kopieer hem. Hij moet namelijk ook voor toekomstige gebruikers beschikbaar blijven als .env.example.

5. Run `composer install`
6. Run `php artisan key:generate`
7. Run `php artisan migrate` (kies voor yes als hij vraagt of je de database aan wil maken)
8. Run `npm install`
9. Run `npm run dev`

Klik nu in de terminal op de URL om hem in de browser te openen.

## Bestaand project gebruiken
Om een bestaand project te clonen zodat je er lokaal aan kunt werken, voer je onderstaande stappen uit:

1. Ga naar de repository op github.com
2. Klik op de groene knop `<> Code`
3. Klik op `Open with GitHub Desktop`
4. Selecteer de map waar je hem in wil hebben (bijvoorbeeld `C:\laragon\www`) en clone hem
5. Open de map in een editor
6. Kopieer de .env.example naar .env

    {: .important }
    Hernoem de .env.example niet, maar kopieer hem. Hij moet namelijk ook voor toekomstige gebruikers beschikbaar blijven als .env.example.
    
7. Run `composer install`
8. Run `php artisan key:generate`
9. Run `php artisan migrate` (kies voor yes als hij vraagt of je de database aan wil maken)
10. Run `npm install`
11. Run `npm run dev`
   
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

## Livewire
Om Livewire te installeren run je de volgende commando's:
1. `composer require livewire/livewire`
2. Kies één van onderstaande opties en voeg deze toe in de layout van de webapp (bijvoorbeeld `resources/views/welcome.blade.php`):

### Directive
Voeg onderstaande regel toe in de `<head>` tag:
```php
@livewireStyles
```
en onderstaande regel onderaan in de `<body>`:
```php
@livewireScripts
```

### Tags
Voeg onderstaande regel toe in de `<head>` tag:
```html
<livewire:styles />
```
en onderstaande regel onderaan in de `<body>`:
```html
<livewire:scripts />
```

{: .important }
Als de `@` syntax (directive) niet werkt, kan je ook de tag syntag gebruiken. Dit werkt dan vaak wel.

{::options parse_block_html="true" /}
<details><summary markdown="span">Het bestand ziet er dan ongeveer zo uit</summary>
```html
<html>
<head>
    ...
    @livewireStyles / <livewire:styles />
</head>
<body>
    ...
    @livewireScripts / <livewire:scripts />
</body>
</html>
```
</details>
{::options parse_block_html="false" /}


