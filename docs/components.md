---
title: Components
layout: page
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

## Flash message
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
