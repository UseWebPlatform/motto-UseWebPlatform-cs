# #UseWebPlatform <sup><sub>Czech <a href="https://github.com/UseWebPlatform/motto-UseWebPlatform-cs/compare/v1.3.0...v1.4.0#files_bucket">v1.4.0</a> - 2017-12-04</sub></sup>

Používejte API [webové platformy](https://www.w3.org/standards/), vzory, polyfilly a lehké knihovny pro znovu použitelný, výkonný a udržitelný kód.

Deset pravidel:

- [1. Stavte na Ecma a W3C standardech](#1-stavte-na-ecma-a-w3c-standardech)
- [2. Vyhněte se front-endovým frameworkům](#2-vyhněte-se-front-endovým-frameworkům)
- [3. Negenerujte HTML na straně serveru](#3-negenerujte-html-na-straně-serveru)
- [4. JavaScript, CSS Properties, HTML Templates, Web Workers, WebAssembly](#4-javascript-css-properties-html-templates-web-workers-webassembly)
- [5. PRPL vzor](#5-prpl-vzor)
- [6. Inkrementální aktualizace a sdílené závislosti](#6-inkrementální-aktualizace-a-sdílené-závislosti)
- [7. Custom elementy a pravidla přístupného webu](#7-custom-elementy-a-pravidla-přístupného-webu)
- [8. Progresivní webové aplikace PWA](#8-progresivní-webové-aplikace-pwa)
- [9. Neopakujte se](#9-neopakujte-se)
- [10. Modulární web pro všechny](#10-modulární-web-pro-všechny)

## 1. Stavte na Ecma a W3C standardech

Tvořte lepší web postavený na nových W3C standardech [Custom Elements v1](https://developers.google.com/web/fundamentals/web-components/customelements) a [Shadow DOM v1](https://developers.google.com/web/fundamentals/web-components/shadowdom) umožňující rozšířit W3C [DOM](https://en.wikipedia.org/wiki/Document_Object_Model) jako jediný framework. Komplexní webové aplikace tvořte modulárně z mnoha zapouzdřených custom elementů s vlastním stromem pomocí Shadow DOM. Dodržujte metodu [progressive enhancement](https://www.zdrojak.cz/clanky/graceful-degradation-vs-progressive-enhancement/) za pomoci W3C [polyfillů](https://www.w3.org/2001/tag/doc/polyfills/).

Tyto a níže uvedené Ecma a W3C standardy vám umožňují psát udržitelný kód :sparkles: **maintainable code** :sparkles: a zajišťují lepší dostupnost webových vývojářů. :tada:

<details>
<summary>Další užitečné zdroje</summary>

### Web Components

- [What are web components?](https://www.webcomponents.org/introduction)
- [Building Components](https://developers.google.com/web/fundamentals/web-components/)
- [Shadow DOM: fast and encapsulated styles](https://meowni.ca/posts/shadow-dom/)
- [Custom Elements Everywhere (Polymer Summit 2017)](https://www.youtube.com/watch?v=sK1ODp0nDbM&index=12&list=PLNYkxOF6rcIDP0PqVaJxqNWwIgvoEPzJi)
- [Custom Elements Everywhere](https://custom-elements-everywhere.com)

**Nepotřebujete** Angular Components, React Components, Vue Components, atd.

### Polyfilly

- [Web Components Polyfills](https://www.webcomponents.org/polyfills)
- [Polymer 3.0 - No Polyfills Needed!](https://youtu.be/JH6jEcLxJEI?t=12m45s) :tada:
- [Polyfill.io](https://polyfill.io) - Upgrade the web. Automatically.

</details>

## 2. Vyhněte se front-endovým frameworkům

Těžké a složité frameworky pro front-end (Angular, Bootstrap, Ember, jQuery, React, Vue, atd.) zpomalují načtení (žerou data, výkon i baterii) a omezují vývoj, udržitelnost a snadné rozšiřování webových stránek a aplikací. Srovnání frameworků pomocí progresivních webových aplikací (PWA) je na stránce [HNPWA](https://hnpwa.com), zde porovnejte časy pro interaktivní zobrazení.

CSS frameworky (Bootstrap, Foundation, atd.) obsahují velké množství nepoužívaného (unused) CSS kódu na dané stránce. Nepoužívejte CSS frameworky, tím se vyhnete stahování zbytečných kilobajtů a umožníte prohlížeči začít dříve renderovat stránku.

Custom elementy se Shadow DOM řeší z větší části problematiku nepoužívaného CSS a JS kódu, která se nechá měřit pomocí [DevTools Coverage](https://developers.google.com/web/updates/2017/04/devtools-release-notes#coverage). Členit CSS kód pomocí Shadow DOM je výkonější, než pomocí JS, viz pěkný článek [Shadow DOM: fast and encapsulated styles](https://meowni.ca/posts/shadow-dom/).

Náklady na zpracování JS kódu jsou vetší než u jiných dat, viz pěkný článek [The Cost Of JavaScript](https://medium.com/dev-channel/the-cost-of-javascript-84009f51e99e).

<details>
<summary>Další užitečné zdroje</summary>

### Proč nepotřebujete frameworky

- [Web Components VS Frameworks](https://medium.com/@oneeezy/frameworks-vs-web-components-9a7bd89da9d4)
- [You Don't Need jQuery](https://github.com/oneuijs/You-Dont-Need-jQuery)
- [You might not need a CSS framework](https://hacks.mozilla.org/2016/04/you-might-not-need-a-css-framework/)
- [JavaScript back to basics: You might not need React or Angular 2](https://react-etc.net/entry/javascript-back-to-basics-you-might-not-need-react-or-angular-2)

</details>

## 3. Negenerujte HTML na straně serveru

### SSR

Není třeba SSR (server-side rendering) pro generování HTML kódu na straně serveru, z něj přes API získávejte jen JSON data, tím šetříte drahá data na pomalých sítích, výkon i baterii na straně klienta. Vyhněte se pomalým a složitým back-endovým frameworkům generující HTML, např. ASP.NET, Django, Laravel, React, Tomcat, Vue, atd.

Webové stránky nebo aplikace bez SSR mohou při opětovném zobrazení již běžet z lokální Service Worker Cache paměti, tím se pak chovají stejně jako nativní aplikace pro Android, iOS, macOS či Windows.

### CSR

Kombinace CSR (client-side rendering) + [PRPL vzor](#5-prpl-vzor) + [W3C Service Worker Cache](https://developers.google.com/web/ilt/pwa/caching-files-with-service-worker) + [CDN](https://en.wikipedia.org/wiki/Content_delivery_network) řeší rychlé načtení webových stránek a aplikací (front-endu). Service Worker Cache jim umožňuje běžet offline, bez připojení k internetu. Komunikace se serverem (back-endem) probíhá přes [JSON API](http://jsonapi.org), [GraphQL](http://graphql.org) nebo [REST API](https://en.wikipedia.org/wiki/Representational_State_Transfer). Pro tyto API je vhodné použít např. Node.js, Go lang nebo Python. Příkladem je :sparkles: [JAMstack](https://jamstack.org) :sparkles:.

### Back-end

Nechte správu o složitý back-end cloud službám, nemusíte pak řešit [horizontální škálování](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling), [SLA](https://en.wikipedia.org/wiki/Service-level_agreement) a [GDPR](https://www.gdpr.cz) jako "data processor".

Například cloud Firebase je dobře navržen pro multi-platformní vývoj aplikací. Jeho služba Firebase Functions krásně řeší modularitu back-endu, viz příklady v git repozitáři [Cloud Functions for Firebase Sample Library](https://github.com/firebase/functions-samples). Firebase bude připraven na GDPR, viz [FAQ](https://firebase.google.com/support/faq/#privacy).

Jestli vás baví back-end nebo nechcete cloud, tak se podívejte na jiná řešení ze seznamů [Awesome Serverless](https://github.com/search?utf8=%E2%9C%93&q=Awesome+Serverless).

Jestli potřebujete CMS pro váš front-end, tak si vyberte ze seznamu [HeadlessCMS](https://headlesscms.org).

Máte-li málo času nebo nemáte prostředky, tak zkuste najít potřebné API na tržišti [RapidAPI](https://rapidapi.com). 

### SEO

[SEO](https://en.wikipedia.org/wiki/Search_engine_optimization) webových stránek a aplikací řešte pomocí :sparkles: [Headless Chrome](https://developers.google.com/web/updates/2017/04/headless-chrome) :sparkles:.

Projekt Polymer vyvíjí [PRPL server](https://github.com/Polymer/prpl-server-node), který umí search bótům podstrčit statickou stránku (bez JavaScriptu) vygenerovanou pomocí Headless Chrome.

<details>
<summary>Další užitečné zdroje</summary>

### Proč CSR

- [JAMstack vs Isomorphic Server Side Rendering](https://www.netlify.com/blog/2017/06/06/jamstack-vs-isomorphic-server-side-rendering/)
- [An API-First Development Approach](https://dzone.com/articles/an-api-first-development-approach-1)
- [Postman makes API development faster, easier, and better](https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop)

### JSON API

- [The Benefits of Using JSON API](https://nordicapis.com/the-benefits-of-using-json-api/)
- [Pragmatic JSON API Design](https://www.youtube.com/watch?v=3jBJOga4e2Y)
- [You Might Not Need GraphQL](https://blog.runscope.com/posts/you-might-not-need-graphql)
- [Sending json api object using postman](https://stackoverflow.com/questions/43002142/sending-json-api-object-using-postman)

### GraphQL

- [The GitHub GraphQL API](https://githubengineering.com/the-github-graphql-api/)
- [GraphQL Server on Cloud Functions for Firebase](https://codeburst.io/graphql-server-on-cloud-functions-for-firebase-ae97441399c0)
- [Altair GraphQL Client](https://chrome.google.com/webstore/detail/altair-graphql-client/flnheeellpciglgpaodhkhmapeljopja)
- [Apollo GraphQL](https://www.apollographql.com)
- [Apollo Client Developer Tools](https://chrome.google.com/webstore/detail/apollo-client-developer-t/jdkknkkbebbapilgoeccciglkfbmbnfm)
- [The Fullstack Tutorial for GraphQL](https://www.howtographql.com)

### Firebase

- [Extending Firebase to the Web (Firebase Dev Summit 2017)](https://www.youtube.com/watch?v=puUqJTJVz5A&list=PLl-K7zZEsYLlTSrObc8GxDLarH7tF9WeW&index=7)
- [Introducing Cloud Firestore (Firebase Dev Summit 2017)](https://www.youtube.com/watch?v=W3xIOQu0h1w&index=12&list=PLl-K7zZEsYLlTSrObc8GxDLarH7tF9WeW)
- [Write Production Quality Cloud Functions (Firebase Dev Summit 2017)](https://www.youtube.com/watch?v=tResEeK6P5I&list=PLl-K7zZEsYLlTSrObc8GxDLarH7tF9WeW&index=15)

### RapidAPI

- [Mashape’s API Marketplace is now part of RapidAPI](https://medium.com/the-era-of-apis/mashapes-api-marketplace-is-now-part-of-rapidapi-53701442f5e4)
- [20 Tutorials on How to Create Your Own API](https://medium.com/the-era-of-apis/20-tutorials-on-how-to-create-your-own-api-sorted-by-programming-language-9ad2fa5fc429)

### SEO

- [Solving SEO with Headless Chrome (Polymer Summit 2017)](https://www.youtube.com/watch?v=ydThUDlBDfc&index=21&list=PLNYkxOF6rcIDP0PqVaJxqNWwIgvoEPzJi)
- [Puppeteer Playground](https://try-puppeteer.appspot.com)
- [Rendertron - headless rendering service](https://render-tron.appspot.com)

</details>

## 4. JavaScript, CSS Properties, HTML Templates, Web Workers, WebAssembly

### JavaScript

Programujte ve standardizovaném jazyce Ecma JavaScript ES6 ([ECMAScript 2015](https://en.wikipedia.org/wiki/ECMAScript)), který umí číst všichni webový vývojáři. Naučte se správně tento jazyk, pomůžou vám odkazy níže.

Jazyk TypeScript či jiné JS preprocessory (Dart, CoffeeScript) nejsou na front-endu třeba, neboť knihovna Polymer rozšiřuje [HTML Properties](https://www.w3schools.com/jsref/dom_obj_all.asp) na elementu o statické typy, private a protected typy, výchozí hodnotu, read-only stav a jiné, více na stránce [Declare Properties](https://www.polymer-project.org/2.0/docs/devguide/properties). S těmito properties pracuje plugin [Polymer IDE](https://github.com/StartPolymer/awesome-polymer#editor-plugins). Výhodou je, že se nepotřebujete učit další nový jazyk. 

Jestli potřebujete nasadit **TypeScript**, třeba pro komplexní webové komponenty, tak projekt Polymer udržuje dekoratéry pro tento jazyk, uloženy jsou v gitu [polymer-decorators](https://github.com/Polymer/polymer-decorators). Nejdříve pečlivě zvažte, zda potřebujete TypeScript, který svádí k používaní nového jazyka, který není standardizovaný a tím pádem je výsledný kód težko udržitelný a není čitelný pro všechny. Viz tento pěkný článek [You Might Not Need TypeScript (or Static Types)](https://medium.com/javascript-scene/you-might-not-need-typescript-or-static-types-aa7cb670a77b) a [komentář k článku TypeScript vs. JavaScript](https://medium.com/@richardeng/ive-used-many-programming-languages-over-the-past-40-years-including-statically-typed-eg-fff827379c1).

### CSS

Kódujte ve standardizovaném jazyce W3C [CSS3](https://www.w3schools.com/css/css3_intro.asp), který umí číst všichni webový vývojáři. Tento jazyk byl rozšířen o dynamické proměnné W3C [CSS Properties](https://www.polymer-project.org/2.0/docs/devguide/custom-css-properties). Díky polyfillu je možné rozšířit CSS o [CSS Mixins](https://www.polymer-project.org/2.0/docs/devguide/custom-css-properties#use-custom-css-mixins) (metody). Tato dvě rozšíření jazyka CSS a modularita CSS na úrovni custom elementů se Shadow DOM vám umožňuje opustit statické CSS preprocessory, např. SASS, LESS, Stylus. Výhodou je, že se nepotřebujete učit další nový jazyk. Jestli potřebujete rozšířit CSS o nové vlastnosti či funkce, tak použijte postprocessor [PostCSS](https://github.com/postcss/postcss), který nemění jazyk CSS.

Polymer pomocí [paper elementů](https://www.webcomponents.org/collection/PolymerElements/paper-elements) ukazuje, že pro Material Design není třeba rozšiřovat jazyk CSS o preprocessory. Modularita CSS pomocí custom elementů se Shadow DOM vám umožňuje aplikovat jen potřebné styly pro dané zobrazení webové stránky nebo aplikace. Tato modularita z větší části řeší problematiku nepoužívaného (unused) CSS na stránce.

### HTML Templates

Využívejte vlastnosti W3C [HTML Templates](https://www.polymer-project.org/2.0/docs/devguide/dom-template) namísto HTML preprocessorů (Handlebars, Nunjucks, Pug) nebo JS templatů. Na cestě je :sparkles: [lit-html](https://github.com/PolymerLabs/lit-html) :sparkles:, který přináší [několik výhod oproti JSX](https://github.com/PolymerLabs/lit-html#benefits-over-jsx) a bude podporován knihovnou Polymer v3.0.

### Web Workers

Používejte W3C [Web Workers](https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API/Using_web_workers) API pro spouštění skriptů ve vláknech na pozadí, neovlivňující vlákno uživatelského rozhraní.

### WebAssembly

Výkonnostní kód pište v jazyce C nebo C++ pomocí W3C [WebAssembly](https://en.wikipedia.org/wiki/WebAssembly), které nahrazuje [Chrome Native Client](https://developer.chrome.com/native-client).

<details>
<summary>Další užitečné zdroje</summary>

### CSS Variables, CSS Mixins

- [CSS Variables: Why Should You Care?](https://developers.google.com/web/updates/2016/02/css-variables-why-should-you-care)
- [Using CSS custom properties (variables)](https://developer.mozilla.org/en-US/docs/Web/CSS/Using_CSS_variables)
- [What is the difference between CSS variables and preprocessor variables?](https://css-tricks.com/difference-between-types-of-css-variables/)
- [Polymer custom CSS properties](https://www.polymer-project.org/2.0/docs/devguide/custom-css-properties)
- [Polymer custom CSS mixins](https://www.polymer-project.org/2.0/docs/devguide/custom-css-properties#use-custom-css-mixins)

**Nepotřebujete** SASS, LESS, Stylus, atd.

### HTML Templates

- [HTML \<template\> element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/template)
- [Polymer data binding helper elements](https://www.polymer-project.org/2.0/docs/devguide/templates)
- [HTML templates, via JavaScript template literals](https://github.com/PolymerLabs/lit-html)

**Nepotřebujete** Mustache, Handlebars, Nunjucks, Pug, atd.

### JavaScript

#### Naučte se správně jazyk JavaScript :exclamation:

- [JavaScript Best Practices](https://www.w3schools.com/js/js_best_practices.asp)
- [JavaScript Common Mistakes](https://www.w3schools.com/js/js_mistakes.asp)
- [JavaScript Use Strict](https://www.w3schools.com/js/js_strict.asp)
- [JavaScript Performance](https://www.w3schools.com/js/js_performance.asp)
- [JavaScript ES6](http://es6-features.org) - New features: overview & comparison.
- [Learn How To Debug JavaScript with Chrome DevTools](https://codeburst.io/learn-how-to-debug-javascript-with-chrome-devtools-9514c58479db)
- [ES8 was Released and here are its Main New Features](https://hackernoon.com/es8-was-released-and-here-are-its-main-new-features-ee9c394adf66)
- [Awesome Mobile Web Specialist](https://github.com/PolymerTemple/awesome-mobile-web-specialist)

#### Kurzy jazyka JavaScript

- [freeCodeCamp](https://www.freecodecamp.org)
- [Codewars JavaScript](https://www.codewars.com/?language=javascript)
- [Modern JavaScript with Tyler McGinnis](https://www.youtube.com/playlist?list=PLqrUy7kON1meLrM6e7WW02jJ8QongnT7Z)
- [What are the best websites to learn to code?](https://www.producthunt.com/ask/3452-what-are-the-best-websites-to-learn-to-code)

#### Statické typy

- [You Might Not Need TypeScript (or Static Types)](https://medium.com/javascript-scene/you-might-not-need-typescript-or-static-types-aa7cb670a77b)
- [Polymer Custom Element Properties](https://www.polymer-project.org/2.0/docs/devguide/properties)

**Nepotřebujete** Dart, TypeScript, Elm, PureScript, CoffeeScript, ClojureScript, atd.

### Web Workers

- [WebWorkers: Code Session - Supercharged](https://www.youtube.com/watch?v=X57mh8tKkgE)

</details>

## 5. PRPL vzor

:sparkles: [PRPL Pattern](https://developers.google.com/web/fundamentals/performance/prpl-pattern/) :sparkles: je vzor pro strukturování a zobrazování progresivních webových aplikací (PWA), s důrazem na jejich výkon a spouštění.

Jednotlivé webové komponenty (JS moduly) se stahují binárně najednou (jen jednou) při prvním dotazu na server (HTTP/2) na základě dané trasy (URL), kde jsou potřeba pro render na straně klienta.

### PRPL-50

[Měřte čas potřebný pro interaktivní zobrazení](https://youtu.be/0A-2BhEZiM4?t=9m20s) (Time to Interactive) webové stránky nebo aplikace. Tento čas je závislý na množství přenesených dat. Na 3G mobilních sítích je omezení přibližně **50 KB** per trasu :exclamation:

Lehká [knihovna Polymer v2.0](https://www.polymer-project.org/2.0/docs/devguide/feature-overview) má přibližně 12 KB, takže zbývá asi 38 KB pro vaše data. :tada:

<details>
<summary>Další zajímavé odkazy</summary>

### PRPL servery

- [prpl-server-node](https://github.com/Polymer/prpl-server-node)
- [prpl-server-go](https://github.com/CaptainCodeman/prpl-server-go)

#### Funkce PRPL serveru

- [Differential Serving](https://github.com/Polymer/prpl-server-node#differential-serving)
- [HTTP/2 Server Push](https://github.com/Polymer/prpl-server-node#http2-server-push)
- [Rendering for Bots (SEO, Open Graph)](https://github.com/Polymer/prpl-server-node#rendering-for-bots)

### Limit 50 KB

- [Building m.uber: Engineering a High-Performance Web App for the Global Market](https://eng.uber.com/m-uber/)

</details>

## 6. Inkrementální aktualizace a sdílené závislosti

Využívejte kombinaci [HTTP/2](https://developers.google.com/web/fundamentals/performance/http2/) + [Server Push](https://developers.google.com/web/fundamentals/performance/http2/#server_push) + standardní formáty modulů, jako jsou [HTML Imports](https://w3c.github.io/webcomponents/spec/imports/) nebo [ES6 Modules](http://exploringjs.com/es6/ch_modules.html) umožňující inkrementální sdílené závislosti a jejich efektivní doručení ke klientovi přes cache, bez složitých nástrojů a zavaděčů, jako jsou např. Browserify, Rollup, Webpack, atd. Tato kombinace řeší zároveň inkrementální aktualizace výsledné webové stránky nebo aplikace. Pro tuto kombinaci umí Polymer build proces sestavit závislosti, více na stránce [Build for production](https://www.polymer-project.org/2.0/toolbox/build-for-production).

<details>
<summary>Další užitečné zdroje</summary>

### Polymer v3.0

Knihovna Polymer v3.0 využívá [ES6 moduly via script tag](https://caniuse.com/#feat=es6-module) namísto HTML importů, více informací na stránce [MDN import](https://developer.mozilla.org/cs/docs/Web/JavaScript/Reference/Statements/import). Dále [dynamický import modulů](https://blog.chromium.org/2017/10/chrome-63-beta-dynamic-module-imports_27.html).

</details>

## 7. Custom elementy a pravidla přístupného webu

Při vytváření custom elementů dodržujte checklist [The Gold Standard Checklist for Web Components](https://github.com/webcomponents/gold-standard/wiki). Jejich zdrojový kód je čten častěji, než je psán, proto [**pište kód pro lidi**](https://www.youtube.com/watch?v=gweY3L0YA1Y) :exclamation:

Dodržujte W3C [pravidla přístupného webu](http://www.pravidla-pristupnosti.cz), se kterými pomáhají již vytvořené Polymer komponenty.

Na cestě je nová generace Polymer elementů, které se zaměřují na vylepšení výkonu, menší API a lepší rozšiřitelnost pomocí dědičnosti ES6 tříd, viz pěkné video [Evolving the Next Generation of Polymer Elements (Polymer Summit 2017)](https://www.youtube.com/watch?v=rvpJ5O0W_6A&list=PLNYkxOF6rcIDP0PqVaJxqNWwIgvoEPzJi&index=6) a článek [The future of elements](https://www.polymer-project.org/blog/2017-11-27-future-of-elements.html).

<details>
<summary>Další užitečné zdroje</summary>

### Custom elementy
  
- [Custom Element Best Practices](https://developers.google.com/web/fundamentals/web-components/best-practices)

### Přístupnost webu

- [A11ycasts with Rob Dodson](https://www.youtube.com/playlist?list=PLNYkxOF6rcICWx0C9LVWWVqvHlYJyqw7g)
- [Totally Tooling Tips: Accessibility Testing](https://www.youtube.com/watch?v=56zCnwj58e4)
- [Pragmatic Accessibility: A How-To Guide for Teams (Google I/O '17)](https://www.youtube.com/watch?v=A5XzoDT37iM)
- [Accessibility is My Favorite Part of the Platform - Google I/O 2016](https://www.youtube.com/watch?v=2qjgxH384Nc)
- [PWAs in any context (Progressive Web App Summit 2016)](https://www.youtube.com/watch?v=8dr_IUGwsO0)
- [Accessible Components: Labeling -- Polycasts #51](https://www.youtube.com/watch?v=1D25YXLBBX8&list=PLNYkxOF6rcIDdS7HWIC_BYRunV6MHs5xo&index=12)
- [Accessible Components: Screen readers -- Polycasts #50](https://www.youtube.com/watch?v=Lktz1KXbTOU&index=13&list=PLNYkxOF6rcIDdS7HWIC_BYRunV6MHs5xo)
- [Accessible Components: Keyboard access -- Polycasts #49](https://www.youtube.com/watch?v=REVxMvdBYMw&index=14&list=PLNYkxOF6rcIDdS7HWIC_BYRunV6MHs5xo)
- [A11y with Polymer (The Polymer Summit 2015)](https://www.youtube.com/watch?v=o6yLWihykVA&index=14&list=PLNYkxOF6rcICdISJclfQhj2S8QZGjXV8J)
- [The future of accessibility for custom elements](https://medium.com/dev-channel/the-future-of-accessibility-for-custom-elements-291cfb3ffabe) - 2017-10

### Unused CSS

- [Oh No! Our Stylesheet Only Grows and Grows and Grows!](https://css-tricks.com/oh-no-stylesheet-grows-grows-grows-append-stylesheet-problem/)
- [Monitoring unused CSS by unleashing the raw power of the DevTools Protocol](http://blog.cowchimp.com/monitoring-unused-css-by-unleashing-the-devtools-protocol/)

</details>

## 8. Progresivní webové aplikace PWA

Rychlé modulární [progresivní webové aplikace](https://developers.google.com/web/progressive-web-apps/) vytvoříte s architekturou :sparkles: [App Shell](https://developers.google.com/web/fundamentals/architecture/app-shell) :sparkles: za pomoci web komponent s lehkou knihovnou (např. Polymer, SkateJS, Slim.js), PRPL vzoru a checklistu [Progressive Web App Checklist](https://developers.google.com/web/progressive-web-apps/checklist), ze kterého pochopíte co obnáší tato nová cesta pro webové aplikace. :sparkles: **best-performing apps** :sparkles:

Progresivní webové aplikace se chovají "stejně" jako nativní aplikace na platformě Android. Na platformách iOS a Windows není zatím plná podpora. Na platformách [Chrome OS](https://www.google.cz/search?q=Chrome+OS) ([Chromebook](https://www.google.cz/search?q=Chromebook), [Chromebox](https://www.google.cz/search?q=Chromebox), [Chromebase](https://www.google.cz/search?q=Chromebase)) a [Chromium OS](https://www.chromium.org/chromium-os) ([CloudReady](https://www.neverware.com)) beží nativně. Jejich progresivní přístup jim umožňuje běžet kdekoliv díky mnoha webovým prohlížečům. :tada:

PWA aplikace v produkci ukazují, že mají význam, viz statistiky [PWA Stats](https://www.pwastats.com). :+1:

Webová platforma již nyní má několik rozhraní, které umožňují komunikovat s hardwarem, např. [GamePad API](https://www.chromestatus.com/features/5118776383111168), [Generic Sensor API](https://developers.google.com/web/updates/2017/09/sensors-for-the-web), [Web Bluetooth API](https://www.chromestatus.com/feature/5264933985976320), [WebUSB API](https://www.chromestatus.com/features/5651917954875392) a na cestě jsou [Web NFC API](https://www.chromestatus.com/features/6261030015467520), [Standby API](https://www.chromestatus.com/features/5768542523752448).

### Projekt Polymer

Kód PWA aplikací je díky projektu Polymer a hotovým web komponentám čitelný a udržitelný, viz například kód [demo PWA shopu](https://github.com/Polymer/shop), [demo PWA news](https://github.com/Polymer/news) a PWA aplikace [Polymer Summit 2017](https://github.com/Polymer/summit-2017). :+1:

Stav aplikace můžete spravovat pomocí vzorů [Mediator Pattern](https://github.com/StartPolymer/awesome-polymer#mediator-pattern) nebo [Global Mediator Pattern](https://github.com/StartPolymer/awesome-polymer#global-mediator-pattern), ten za pomoci knihovny [UniFlow](https://github.com/StartPolymer/awesome-polymer#uniflow) nebo [Redux](https://github.com/StartPolymer/awesome-polymer#redux).

<details>
<summary>Další užitečné zdroje :eyes:</summary>

### Úvod do PWA

- [Introduction to Progressive Web App Architectures](https://developers.google.com/web/ilt/pwa/introduction-to-progressive-web-app-architectures-slides)
- [Intro to Progressive Web Apps - Free course](https://www.udacity.com/course/intro-to-progressive-web-apps--ud811)
- [Support native integration](https://developers.google.com/web/fundamentals/codelabs/your-first-pwapp/#support_native_integration)
- [WHY You Should Build A Progressive Web App NOW](https://www.youtube.com/watch?v=0LOk_OgUWGM)
- [Twitter Lite PWA Significantly Increases Engagement and Reduces Data Usage](https://developers.google.com/web/showcase/2017/twitter)
- [Kickstarting Your Journey to Progressive Web Apps (Chrome Dev Summit 2017)](https://www.youtube.com/watch?v=goafiwzhKMI)
- [Polymer 2.0 — Building Progressive Web Apps with Enhanced Web Platform Features](https://medium.com/platform-engineer/polymer-2-0-building-progressive-web-apps-with-enhanced-web-platform-features-933251824f13)
- [PWAs with Polymer: a checklist](https://meowni.ca/posts/polymer-pwa-checklist/)
- [Creating UX that “Just Feels Right” with Progressive Web Apps (Google I/O '17)](https://www.youtube.com/watch?v=mmq-KVeO-uU)
- [Web Push Notifications: Permission UX](https://developers.google.com/web/fundamentals/push-notifications/permission-ux)
- [Integrating with Browsers and OS - Android Trusted Web Activity (Chrome Dev Summit 2017)](https://www.youtube.com/watch?v=_sLa0qhuqcA)
- [Trusted Web activities are a new way to integrate PWA with Android app](https://developers.google.com/web/updates/2017/10/using-twa)
- [Awesome PWA](https://github.com/hemanth/awesome-pwa) - Useful resources for creating Progressive Web Apps.

### Podpora PWA ze strany prohlížečů a operačních systémů OS

- [Chrome / Chromium: The New and Improved Add to Home screen](https://developers.google.com/web/updates/2017/02/improved-add-to-home-screen)
- [Add Progressive Web Apps to your Home screen in Firefox for Android](https://hacks.mozilla.org/2017/10/progressive-web-apps-firefox-android/)
- [How to Save PWA to iOS Homescreen](https://vimeo.com/236430523)
- [Safari service workers and other PWA good news stories](https://mobiforge.com/news-comment/safari-service-workers-and-other-pwa-good-news-stories)
- [Progressive Web Apps (PWA) and Windows 10](https://forum.kirupa.com/t/progressive-web-apps-pwa-and-windows-10/637192)
- [Google wants Progressive Web Apps to replace Chrome apps](http://www.androidpolice.com/2017/12/05/google-wants-progressive-web-apps-replace-chrome-apps/)

### Porovnání PWA s nativní aplikací pro Android či iOS

| | Website | PWA (1) | Native App
--- | --- | --- | ---
Offline | NO :heavy_minus_sign: | YES :+1: | YES :+1:
App stores | NO :heavy_minus_sign: | NO :heavy_minus_sign: (2)(3) | YES :+1:
Responsive | YES :+1: | YES :+1: | YES :+1:
Searchable | YES :+1: | YES :+1: | NO :heavy_minus_sign:
Local Notifications | NO :heavy_minus_sign: | YES :+1: | YES :+1:
Push Messages | NO :heavy_minus_sign: | YES :+1: | YES :+1:
Install needed to run | NO :+1: | NO :+1: | YES :heavy_minus_sign:
Fast Updates | YES :+1: | YES :+1: | NO :heavy_minus_sign:
Cross-platform | YES :+1: | YES :+1: | NO :heavy_minus_sign:
Performance | NO :heavy_minus_sign: | YES :+1: (4) | YES :+1:
Lower dev time and cost | YES :+1: | YES :+1: | NO :heavy_minus_sign:
Lower user acquisition cost | YES :+1: | YES :+1: (5) | NO :heavy_minus_sign:
**Result** | +2 | +10 :heart: | 0

(1) PWA na [Chrome od v59 na Androidu](https://developers.google.com/web/updates/2017/02/improved-add-to-home-screen), [Chromebook](https://youtu.be/m-sCdS0sQO8?t=16m12s), [Samsung Internet v5.4 na Androidu](https://medium.com/samsung-internet-dev/announcing-samsung-internet-v5-4-stable-fd941e0dcd58), Windows 10 (brzy)  
(2) Progresivní webové aplikace se brzy objeví ve Windows Store pro Windows 10. :+1:  
(3) Aktualizace nemusí probíhat prostřednictvím obchodu s aplikacemi. :+1:  
(4) Performance použitím [RAIL Performance Model](https://developers.google.com/web/fundamentals/performance/rail), Web Workers, WebAssembly.  
(5) [Progressive Web Apps vs Native: Which Is Better for Your Business?](https://www.technology.org/2017/07/28/progressive-web-apps-vs-native-which-is-better-for-your-business/)

**Nepotřebujete** Apache Cordova, PhoneGap, Crosswalk, React Native, atd.

### Seznamy PWA aplikací

- [Outweb](https://outweb.io)
- [PWA Directory](https://pwa-directory.appspot.com)
- [pwa.rocks](https://pwa.rocks)

</details>

## 9. Neopakujte se

Píšte [dokumentaci](https://www.polymer-project.org/2.0/docs/tools/documentation) a [testy pomocí Web Component Tester](https://www.polymer-project.org/2.0/docs/tools/tests) pro každý znovu použitelný custom element, který žije ve vlastním git repozitáři s landing a demo stránkou :sparkles: **reusable code** :sparkles:. To vám umožňuje tvořit stabilní webové komponenty a neopakovat se (**DRY**: Don't repeat yourself).

## 10. Modulární web pro všechny

Veřejné znovu použitelné custom elementy pro ostatní publikujte na platformě GitHub. Tyto elementy pak ukládejte do katalogu [webcomponents.org](https://www.webcomponents.org), kde je již [**přes 1300 elementů**](https://www.webcomponents.org/elements). :tada:

Webové komponenty jako W3C standard vylepšují a nahrazují Angular Components, Vue Components a jiné, viz projekt [Custom Elements Everywhere](https://custom-elements-everywhere.com).

Notifikace z platformy GitHub hlídejte nejlépe pomocí aplikace [Octobox](https://octobox.io). S platformou GitHub vás seznámí [GitHub Guides](https://guides.github.com) a [tryGit](https://try.github.io).

<br>

> Motto ve formě hashtagu #UseWebPlatform vzniklo rozšířením motta [#UseThePlatform](https://www.polymer-project.org/about).

---

[Informace o projektu Polymer a komunitě Polymeristi](https://github.com/Polymeristi/readme).

#### Licence

<a rel="license" href="http://creativecommons.org/licenses/by/4.0/deed.cs"><img alt="Licence Creative Commons" style="border-width:0" src="https://i.creativecommons.org/l/by/4.0/88x31.png" /></a><br /><span xmlns:dct="http://purl.org/dc/terms/" href="http://purl.org/dc/dcmitype/Text" property="dct:title" rel="dct:type">#UseWebPlatform</span>, jehož autorem je <a xmlns:cc="http://creativecommons.org/ns#" href="https://github.com/JosefJezek" property="cc:attributionName" rel="cc:attributionURL">Josef Ježek</a>,<br>podléhá licenci <a rel="license" href="http://creativecommons.org/licenses/by/4.0/deed.cs">Creative Commons Uveďte původ 4.0 Mezinárodní</a>.
