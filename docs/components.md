---
title: Components
layout: page
nav_order: 6
---

# Components
{: .no_toc }

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
- TOC
{:toc}
</details>

## Aanmaken
Om een component aan te maken kan je het volgende commando gebruiken:
```
php artisan make:component NewItem
```
waar `NewItem` de naam van je component is. Dit maakt ook een class voor je component aan, maar dit is niet altijd nodig. Om een 'anoniem' component te maken (zonder class) kun je de `--view` optie toevoegen:
```
php artisan make:component NewItem --view
```

## Attributen mergen
Om een component in te laden en meegegeven attributen te mergen met attributen die al ingesteld zijn, kan je het volgende gebruiken:
```php
$attributes->merge(['class' => 'alert alert-'.$type])
```

Als je het component dan als volgt inlaadt...
```php
<x-alert type="error" :message="$message" class="mb-4"/>
```

is dit het resultaat:
```php
<div class="alert alert-error mb-4">
    <!-- Contents of the $message variable -->
</div>
```

### Classes en andere default attributen
Om classes te mergen met andere attributen kan je ook de classes los specificeren:
{% raw %}
```php
<button {{ $attributes->class(['p-4'])->merge(['type' => 'button']) }}>
    {{ $slot }}
</button>
```
{% endraw %}

Hier wordt de `type="button"` attribuut ook toegevoegd, naast de class `p-4`.

### Classes en meegegeven attributen
Als er geen andere attributen standaard toegevoegd hoeven te worden, kan je ook een lege `merge()` gebruiken om alleen de attributen te mergen die je zelf meegeeft aan het component.

{% raw %}
```php
<button {{ $attributes->class(['p-4'])->merge() }}>
    {{ $slot }}
</button>
```
{% endraw %}

### Conditionele styling
In een component kan je conditionele styling gebruiken om je component een andere styling te geven als er aan bepaalde voorwaarden voldaan wordt. Zo hoef je geen aparte varianten te maken. Dit kan met de `class` methode.

Je pakt alle meegegeven attributen en maakt in de `class` methode een array van classes. Hier zet je ook alle 'default' classes neer. Voor alle conditionele classes voer je een object in waarvan de key de classes zijn, en de value de voorwaarde.

{% raw %}
```php
<ul {{$attributes->class([
    'w-full px-4 py-2 text-left border-b border-gray-200 cursor-pointer focus:outline-none focus:ring-2 focus:ring-blue-700 focus:text-blue-700', // Default classes
    'font-bold' => !$message->isReadByUser(auth()->id()) || auth()->user()->hasRole('admin'), // Voorwaarde
    'font-medium' => $message->isReadByUser(auth()->id()) || auth()->user()->hasRole('admin'), // Voorwaarde
    'text-white bg-blue-700' => $selectedMessage == $message, // Voorwaarde
    'hover:bg-gray-100 hover:text-blue-700 focus:ring-2 focus:ring-blue-700 focus:text-blue-700' => !$selectedMessage == $message // Voorwaarde
    ])->merge()}}> // Andere attributen mergen
</ul>
```
{% endraw %}

#### Props
Als je - zoals hierboven - voorwaarden hebt met een langere logica, kan het handig zijn om die bovenaan het bestand te zetten. Dit kan door de `@props` directive te gebruiken.

{% raw %}
```php
@props([
    'message' => $message,
    'read' => $message->isReadByUser(auth()->id()) || auth()->user()->hasRole('admin'),
    'selected' => $selectedMessage == $message
])

<ul {{$attributes->class([
    'w-full px-4 py-2 text-left border-b border-gray-200 cursor-pointer focus:outline-none focus:ring-2 focus:ring-blue-700 focus:text-blue-700',
    'font-bold' => !$read,
    'font-medium' => $read,
    'text-white bg-blue-700' => $selected,
    'hover:bg-gray-100 hover:text-blue-700 focus:ring-2 focus:ring-blue-700 focus:text-blue-700' => !$selected])->merge()}}>
</ul>
```
{% endraw %}

Bovenstaande code geeft hetzelfde resultaat als de code daarboven. Alleen wordt hier de logica in de `@props` directive verwerkt. Hierdoor hoef je alleen boolean in de value van de class te zetten, waardoor de code en stuk leesbaarder wordt.

## Voorbeeldcode componenten
### Flash message
Om een bericht te tonen na bijvoorbeeld het aanmaken van een resource of een foutmelding, kan je flash messages gebruiken. Deze message verdwijnt na het verversen en is dus handig om een tijdelijk bericht te laten zien.

Voorbeeldcode voor component:
{% raw %}
```php
@if ($message = Session::get('success'))
	<div class="alert alert-success alert-block">
		<strong>{{ $message }}</strong>
	</div>
@endif

@if ($message = Session::get('error'))
	<div class="alert alert-danger alert-block">
		<strong>{{ $message }}</strong>
	</div>
@endif

@if ($message = Session::get('warning'))
	<div class="alert alert-warning alert-block">
		<strong>{{ $message }}</strong>
	</div>
@endif

@if ($message = Session::get('info'))
	<div class="alert alert-info alert-block">
		<strong>{{ $message }}</strong>
	</div>
@endif

@if ($errors->any())
	<div class="alert alert-danger">
		<ul>
			@foreach($errors->all() as $error)
				<li>{{$error}}</li>
			@endforeach
		</ul>
	</div>
@endif
```
{% endraw %}

En om dan een bericht mee te sturen vanuit een controller:
```php
return redirect()
    ->route('items.index')
    ->with('success', 'Item succesvol aangemaakt');
```

'Success' kan je ook vervangen voor een andere optie uit de component code, bijvoorbeeld 'info'.
