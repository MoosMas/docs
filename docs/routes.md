---
title: Routes
layout: page
nav_order: 3
---

# Routes
{: .no_toc }

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
- TOC
{:toc}
</details>

## Introductie
Routes zijn er om aan te geven waar verzoeken naartoe moeten gaan. Bij een route wordt aangegeven naar welke controller het verzoek gestuurd moet worden, en welke methode in die controller het af gaat handelen. Routes staan in de `routes/web.php`.

## Route aanmaken
Om een GET route aan te maken (om een pagina op te vragen), kan je de volgende regel als voorbeeld gebruiken:

```php
Route::get('/item/{id}', [ItemController::class, 'show'])->name('items.show');
```

- `'/item'` is de URL in de browser waar deze route naar 'luistert'
- `/{id}` is een parameter waarmee je kan aangeven welk item er opgehaald moet worden
- `ItemController` wijst naar de controller van de route
- `'index'` geeft aan welke methode het af gaat handelen
- `name()` is de naam van de route, zodat je hem later makkelijk kunt gebruiken in bijvoorbeeld een redirect

Je kan ook in één regel alle routes voor een resource maken:
```php
Route::resource('items', ItemController::class);
```

## Route berschermen
Om te zorgen dat alleen ingelogde gebruikers een route kunnen bezoeken, kan je gebruik maken van middleware.

```php
Route::get('/items', [ItemController::class, 'index'])->middleware('auth');
```

Om meerdere routes te beschermen kan je een group maken:

```php
Route::middleware('auth')->group(function () {
    Route::get('/item/{id}', [ItemController::class, 'show'])->name('items.show');
    Route::get('/items', [ItemController::class, 'index'])->name('items.index');
    // Of een resource
    Route::resource('items', ItemController::class);
});
```

## Cheatsheet
<table>
    <thead>
        <th></th>
        <th>Omschrijving</th>
        <th>Soort request</th>
        <th>URL van route</th>
        <th>Methode in controller</th>
        <th>Naam van route</th>
    </thead>
    <tbody>
        <tr>
            <td rowspan="2" width="10%"><b>C</b>reate</td>
            <td>Toon nieuw-formulier</td>
            <td>GET</td>
            <td>/photos/create</td>
            <td><a href="./controllers.html#create-get">create()</a></td>
            <td>photos.create</td>
        </tr>
        <tr>
            <td>Opslaan nieuw item</td>
            <td>POST</td>
            <td>/photos</td>
            <td><a href="./controllers.html#store-post">store()</a></td>
            <td>photos.store</td>
        </tr>
        <tr>
            <td rowspan="2"><b>R</b>ead</td>
            <td>Toon alle items</td>
            <td>GET</td>
            <td>/photos</td>
            <td><a href="./controllers.html#index-get">index()</a></td>
            <td>photos.index</td>
        </tr>
        <tr>
            <td>Toon één item</td>
            <td>GET</td>
            <td>/photos/{photo}</td>
            <td><a href="./controllers.html#show-get">show()</a></td>
            <td>photos.show</td>
        </tr>
        <tr>
            <td rowspan="2"><b>U</b>pdate</td>
            <td>Toon edit-formulier</td>
            <td>GET</td>
            <td>/photos/{photo}/edit</td>
            <td><a href="./controllers.html#edit-get">edit()</a></td>
            <td>photos.edit</td>
        </tr>
        <tr>
            <td>Opslaan aangepast item</td>
            <td>PUT</td>
            <td>/photos/{photo}</td>
            <td><a href="./controllers.html#update-put">update()</a></td>
            <td>photos.update</td>
        </tr>
        <tr>
            <td rowspan="2"><b>D</b>elete</td>
            <td>Verwijderen item</td>
            <td>DELETE</td>
            <td>/photos/{photo}</td>
            <td><a href="./controllers.html#destroy-delete">destroy()</a></td>
            <td>photos.destroy</td>
        </tr>
    </tbody>
</table>
