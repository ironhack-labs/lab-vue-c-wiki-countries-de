![logo_ironhack_blue 7](https://user-images.githubusercontent.com/23629340/40541063-a07a0a8a-601a-11e8-91b5-2f13e4e6b441.png)

# LAB | Vue.js WikiCountries  (Composition API)


## Einführung

Nachdem du zu viel Zeit auf GitHub verbracht hast, hast du einen [JSON-Datensatz von Ländern](https://ih-countries-api.herokuapp.com/countries) gefunden und beschlossen, ihn zu nutzen, um deine Wikipedia der Länder zu erstellen!

<p align="center">    
 <img src="https://education-team-2020.s3.eu-west-1.amazonaws.com/web-dev/labs/lab-wiki-countries-1.gif" alt="Example - Finished LAB" /> </p>   


## Anforderungen

- Forke dieses Repo
- Klone dieses Repo
- Öffne das LAB und starte:

  ```bash
  $ cd lab-vue-c-wiki-countries
  $ npm install
  $ npm run dev
  ``` 

## Abgabe

- Führe nach Fertigstellung die folgenden Befehle aus:

  ```bash
  git add .
  git commit -m "done"
  git push origin main
  ```  
- Erstelle einen Pull Request, damit deine TAs deine Arbeit überprüfen können.



## Los geht's

Säubere die `App.vue` Komponente, sodass sie die folgende Struktur innerhalb der Template-Tags hat

```vue
<!-- src/App.js -->
<template>
  <div class="app"></div>
</template>
```

<br>   

## Anweisungen

### Iteration 0 | Installation von vue Router

Denke daran, den vue Router zu installieren:

```shell
$ yarn install vue-router
```

or

```bash
npm install vue-router
```

Und richte den Router in deiner `src/router/index.js` Datei ein:

```js
// src/router/index.js
import { createRouter, createWebHistory } from "vue-router";

const routes = [
  {
    path: "/",
    name: "list",
    component: () => import("../components/CountriesList.vue"),
    children: [
      {
        path: "/list/:alpha3Code",
        name: "list",
        component: () => import("../components/CountryDetails.vue"),
      },
    ],
  },
];

const router = createRouter({
  history: createWebHistory("/"),
  routes,
  scrollBehavior() {
    document.getElementById("app").scrollIntoView();
  },
});

export default router;
``` 

Verwenden Sie es dann in der `main.js`-Datei wie folgt:

```js
// src/main.js
import { createApp } from "vue";
import App from "./App.vue";
import router from "./router";

createApp(App).use(router).mount("#app");
```

### Bootstrap-Installation

Wir werden [Bootstrap](https://getbootstrap.com/) für das Design verwenden :+1:

```shell 
$ yarn install bootstrap  
```   

oder:

```bash
npm install bootstrap@v5.2.2
```

Um die Bootstrap-Styles in der gesamten App verfügbar zu machen, importiere das Stylesheet in `main.js` vor der `createApp`-Zeile:

```javascript 
// src/main.js    
 import 'bootstrap/dist/css/bootstrap.css'; 
```   

<!-- ## Anweisungen -->

### Iteration 1.1 | Erstellen von Komponenten

In dieser Iteration werden wir uns auf das allgemeine Layout konzentrieren. Bevor du beginnst, erstelle innerhalb des `src` Ordners den `components` Ordner. Dort wirst du mindestens 3 Komponenten erstellen:

- `Navbar`: Zeigt die grundlegende Navigationsleiste mit dem Namen des LAB an.

- `CountriesList`: Zeigt die Liste der Links mit den Ländernamen an. Jeder Link sollte ein `vue-router-dom` `router-link` sein, über den wir den Ländercode (`alpha3Code`) über die URL <u>senden</u> werden.

- `CountryDetails`: Ist die Komponente, die wir über `vue-router`'s `Route` renden werden und den Ländercode (`alpha3Code`) über die URL <u>erhalten</u> wird. Dies ist tatsächlich die ID des Landes (Beispiel: `/ESP` für Spanien, `/FRA` für Frankreich).

Um dir bei der Strukturierung der Komponenten zu helfen, haben wir dir ein Beispiel einer Seite in `example.html` gegeben.

Wenn du es stylen möchtest, frische dein Wissen über Bootstrap in der [Dokumentation](https://getbootstrap.com/docs/4.0) auf oder schau dir an, wie wir das Styling in der `example.html` angegangen sind.


### Iteration 1.2 | Navbar-Komponente

Der einfachste Weg, eine Komponente in Vue zu definieren, ist das Schreiben einer JavaScript-Funktion, auch als Funktionskomponente bezeichnet. Die Navigationsleiste sollte den Titel _LAB - WikiCountries_ anzeigen.

### Iteration 1.3 | CountriesList-Komponente

Diese Komponente sollte eine Liste von `router-link`s rendern, die dazu verwendet werden, um eine Browser-URL-Änderung auszulösen. Ein Klick auf einen `router-link` wird die entsprechende `Route` aktivieren, die die Komponente mit den Details des Landes zeigt.


### Iteration 1.4 | CountryDetails-Komponente und `router-view`-Setup

Jetzt, da unsere Liste der Länder bereit ist, sollten wir die `CountryDetails`-Seite erstellen. `CountryDetails` zeigt die Länderdetails entsprechend dem Link an, auf den wir geklickt haben. Diese Komponente sollte dynamisch mit `<router-vue />` dargestellt/gerendert werden.

```vue 
<!-- Example -->    
 <router-view> 
```   
Komponenten, die mit Vue.js gerendert werden, können die Abfrage mit `this.$route` lesen. Wir können dies verwenden, um Informationen aus der URL-Leiste des Browsers abzurufen, zum Beispiel den `alpha3Code`-Code des Landes.

**HINWEIS:** Für das kleine Bild der Flagge kann man den kleingeschriebenen `alpha2Code` verwenden und ihn in der URL wie unten gezeigt einbetten:

- Frankreich: https://flagpedia.net/data/flags/icon/72x54/fr.png
- Deutschland: https://flagpedia.net/data/flags/icon/72x54/de.png
- Brasilien: https://flagpedia.net/data/flags/icon/72x54/br.png
- usw.

----   

### Iteration 2 | Verknüpfung aller Teile

Sobald die Komponenten erstellt wurden, sollte die Struktur der Elemente, die von Ihrer `App.js` gerendert werden, in etwa wie folgt aussehen:

```vue
<template>
  <div class="app">
    <NavBar />
    <router-view />
  </div>
</template>

<script setup>
import NavBar from "./components/NavBar.vue";
</script>

<style></style>
```   

----   

### Iteration 3 | Setzen Sie den Status beim Laden der Komponente

Unsere `App.vue`-Anwendung sollte `countries` in die Vue-Datenmethode einfügen, um die Daten aus der Datei `src/countries.json` zu halten.
    
----   

### Iteration 4 | Bonus | Hol Dir Länderdaten von einer API

Anstatt auf die statischen Daten aus einer `json`-Datei zu vertrauen, wollen wir etwas Interessanteres tun und die Daten von einer tatsächlichen API abrufen.

Lass uns einen `GET`-Request an die URL [https://ih-countries-api.herokuapp.com/countries](https://ih-countries-api.herokuapp.com/countries) schicken und die zurückgegebenen Daten als Liste der Länder nutzen. Du kannst entweder `fetch` oder `axios` verwenden, um den Request auszuführen.

Wenn Sie die Options-API verwenden, sollten Sie den `mounted()`-Hook verwenden, um den Lebenszyklus-Hook festzulegen, der nur einmal ausgeführt wird und eine Anfrage an die API sendet.

Sie sollten `<script setup>` verwenden, um die Lebenszyklusmethode der Zusammensetzungs-API festzulegen, mit der Sie am Anfang des Lebenszyklus arbeiten können.

<br>

<p align="center">
  <img src="https://vuejs.org/assets/lifecycle.16e4c08e.png" alt="Where is the setup lifecycle" />
</p>

<br>

Die Anfrage sollte passieren, sobald die Anwendung geladen wird. Überlegen Sie daher, wann und von wo aus wir die Anfrage an die API stellen sollten.
    
----   

### Iteration 5 | Bonus | Abruf von Daten zu einem Land von einer API

Verwende den `mounted()`-Hook, um das `CountryDetails`-Komponente zu setzen. Es sollte eine Anfrage an die RestCountries-API stellen und die Daten für das spezifische Land abrufen. Du kannst den Endpunkt der Anfrage mit dem `alpha3Code` des Landes konstruieren. Beispiel:

- Vereinigte Staaten: [https://ih-countries-api.herokuapp.com/countries/USA](https://ih-countries-api.herokuapp.com/countries/USA)
- Japan: [https://ih-countries-api.herokuapp.com/countries/JPN](https://ih-countries-api.herokuapp.com/countries/JPN)
- Indien: [https://ih-countries-api.herokuapp.com/countries/IND](https://ih-countries-api.herokuapp.com/countries/IND)

Der Effekt sollte nach der initialen Rendern und jedes Mal ausgeführt werden, wenn sich der URL-Parameter mit dem `alpha3Code` ändert.

<br>  

**Viel Spaß beim Coden!** :heart: