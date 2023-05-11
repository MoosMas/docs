---
title: Responses
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

## Redirect

{: .note }
Stukje over redirects nog aanmaken.

### Redirect zonder browsergeschiedenis
Om een gebruiker door te sturen naar een andere pagina zonder dat de redirect URL in de geschiedenis komt, kan je zowel JavaScript gebruiken als de normale HTTP redirect.

{: .important }
Ik heb beide manieren getest in Vivaldi en in Chrome. In Chrome werken allebei de manieren (voor zover ik ze getest heb), maar in Vivaldi komt bij beide manieren de URL wel in de geschiedenis te staan.

#### JavaScript
Om met JavaScript een redirect te maken, maak je een route aan die naar een nieuwe view gaat.

```php
Route::get('/redirect', function() {
    return view('redirect');
})->name('redirect');
```

In die view zet je dan een redirect:

{% raw %}
```html
<script>
	document.location.replace('{{route('target')}}')
</script>
```
{% endraw %}

#### HTTP Redirect
Om met HTTP door te sturen, maak je een route aan die de redirect uitvoert.

```php
Route::get('/redirect', function() {
    return redirect('testview');
})->name('redirect');
```
