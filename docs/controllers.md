---
title: Controllers
layout: page
nav_order: 4
---

# Controllers
{: .no_toc}

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
- TOC
{:toc}
</details>

## Introductie

In controllers worden alle verzoeken voor een resource afgehandeld. Bijvoorbeeld alle data opvragen, maar ook aanmaken, bewerken, verwijderen etc.

## Aanmaken
Om een nieuwe controller - in dit geval voor users - aan te maken gebruik je het volgende commando:
```
php artisan make:controller UserController
```

Dit commando maakt een lege controller, maar vaak is het handig om alle standaard methodes voor een CRUD systeem alvast klaar te hebben staan. Dit kan je doen door aan bovenstaand commando de optie `--resource` toe te voegen:
```
php artisan make:controller UserController --resource
```

## Methodes
In een controller worden meestal onderstaande methodes gebruikt. Dit zijn ook de methodes die de `--resource` optie standaard aanmaakt.

In elk voorbeeld waar data mee teruggestuurd wordt naar de view zijn 2 manieren mogelijk om dit te doen.
De eerste optie is om zelf de variabelen een waarde te geven:
```php
return view('items.index', [
    'items' => $items
]);
```
De tweede optie is door middel van de `compact()` functie:
```php
return view('items.index', compact('items'));
```

### Index (GET)
{: .no_toc }
De index methode wordt meestal gebruikt om alle data van een resource op te halen, bijvoorbeeld voor een overzichtspagina. Deze data wordt dan bijvoorbeeld in een tabel neergezet.

```php
public function index()
{
    $items = Item::all();
    return view('items.index', compact('items'));
}
```

### Create (GET)
{: .no_toc }
De create methode wordt gebruikt om het formulier te laten zien om een nieuw item aan te maken in de database.

```php
public function create()
{
    return view('items.create');
}
```

### Store (POST)
{: .no_toc }
De store methode slaat een nieuw item in de database op.

```php
public function store(Request $request)
{
    $item = new Item();
    $item->name = $request->name;
    $item->description = $request->description;
    $item->save();
    
    return redirect()
        ->route('items.index');
}
```
Je kan ook alle waarden in één regel uit het formulier halen. Dan is het wel belangrijk dat alle formuliervelden dezeflde `name` hebben als de kolommen.
```php
public function store(Request $request)
{
    $item = Item::create($request->except('_token'));
    return redirect()
        ->route('items.index');
}
```

{: .note }
Zie <a href="#mass-assignments">Mass assignments</a> voor meer informatie over hoe je in één regel bewerkingen uit kunt voeren.

### Show (GET)
{: .no_toc }
De show methode wordt gebruikt om één item weer te geven. Dit wordt ook wel de detailpagina genoemd, waar meer/uitgebreidere informatie te vinden is over een item uit de database.

```php
public function show($id)
{
    $item = Item::findOrFail($id);
    return view('items.show', compact('item'));
}
```
Om een link naar een detailpagina te maken moet je het ID of object meegeven aan de URL:
{% raw %}
```html
<a href="{{route('items.show', $item->id)}}"></a>
```
{% endraw %}

### Edit (GET)
{: .no_toc }
De edit methode wordt gebruikt om het formulier te laten zien om een bestaand item aan te passen.

```php
public function edit($id)
{
    $item = Item::findOrFail($id);
    return view('items.edit', compact('item'));
}
```

### Update (PUT)
{: .no_toc }
De update methode wordt gebruikt om een bestaand item aan te passen.

```php
public function update(Request $request, $id)
{
    $item = Item::find($id);
    $item->name = $request->name;
    $item->description = $request->description;
    $item->save();
    
    return redirect()
        ->route('items.index')
}
```

Ook hier is het weer mogelijk om het in één regel te doen. Het is wel belangrijk dat alle formuliervelden dezeflde `name` hebben als de kolommen.
```php
public function update(Request $request, $id)
{
    $item = Item::update($request->except('_token'));
    return redirect()
        ->route('items.index');
}
```

{: .note }
Zie <a href="#mass-assignments">Mass assignments</a> voor meer informatie over hoe je in één regel bewerkingen uit kunt voeren.

Voor het formulier op een edit pagina moet je de PUT methode gebruiken. Dat kan door het formulier een POST `method` te geven en in het formulier de `@method` directive te gebruiken:
{% raw %}
```php
<form action="{{route('items.update', $item->id)}}" method="POST">
    @csrf
    @method('PUT')
    ...
</form>
```
{% endraw %}

### Destroy (DELETE)
{: .no_toc }
De destroy methode wordt gebruikt om items uit de database te verwijderen.

```php
    public function destroy($id)
    {
        Item::destroy($id);
        return redirect()
            ->route('items.index');
    }
```
Voor het formulier op een pagina moet je de DELETE methode gebruiken. Dat kan door het formulier een POST `method` te geven en in het formulier de `@method` directive te gebruiken:
{% raw %}
```php
<form action="{{route('items.destroy', $item->id)}}" method="POST">
    @csrf
    @method('DELETE')
    ...
</form>
```
{% endraw %}

# Troubleshooting

## Mass Assignments
Om in één regel een item aan te maken of te updaten moet je in het model `guarded` of `fillable` aangeven. Dit bepaalt welke velden er in één keer ingevuld kunnen worden.
Onderstaande regel zorgt dat geen enkel veld 'beschermd' is, en dat ze dus allemaal ingevuld kunnen worden.
```php
protected $guarded = [];
```
Om aan te geven dat er maar een paar kolommen ingevuld kunnen worden, kan je onderstaande code gebruiken:

```php
protected $fillable = ['name', 'description'];
```

## 403 Session expired
Waarschijnlijk staat er geen CSRF token in het formulier waardoor je een foutmelding krijgt.
Code:
```php
@csrf
```
