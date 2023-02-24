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
            <td>create()</td>
            <td>photos.create</td>
        </tr>
        <tr>
            <td>Opslaan nieuw item</td>
            <td>POST</td>
            <td>/photos</td>
            <td>store()</td>
            <td>photos.store</td>
        </tr>
        <tr>
            <td rowspan="2"><b>R</b>ead</td>
            <td>Toon alle items</td>
            <td>GET</td>
            <td>/photos</td>
            <td>index()</td>
            <td>photos.index</td>
        </tr>
        <tr>
            <td>Toon één item</td>
            <td>GET</td>
            <td>/photos/{photo}</td>
            <td>show()</td>
            <td>photos.show</td>
        </tr>
        <tr>
            <td rowspan="2"><b>U</b>pdate</td>
            <td>Toon edit-formulier</td>
            <td>GET</td>
            <td>/photos/{photo}/edit</td>
            <td>edit()</td>
            <td>photos.edit</td>
        </tr>
        <tr>
            <td>Opslaan aangepast item</td>
            <td>PUT</td>
            <td>/photos/{photo}</td>
            <td>update()</td>
            <td>photos.update</td>
        </tr>
        <tr>
            <td rowspan="2"><b>D</b>elete</td>
            <td>Verwijderen item</td>
            <td>DELETE</td>
            <td>/photos/{photo}</td>
            <td>destroy()</td>
            <td>photos.destroy</td>
        </tr>
    </tbody>
</table>
