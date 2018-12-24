---
title: Introduzione
type: guide
order: 2
---

## Cos'è Vue.js?

Vue (pronunciato /vjuː/, like **view**) è un **framework progressivo** per costruire interfacce utente. A differenza di altri framework monolitici, Vue è progettato da zero per essere incrementalmente utilizzabile. La libreria principale è focalizzata solo sul livello di visualizzazione ed è facile da integrare con altre librerie o progetti esistenti. D'altra parte, Vue è anche perfettamente in grado di alimentare sofisticate applicazioni a pagina singola quando utilizzato in combinazione con [strumenti moderni](single-file-components.html) e [librerie di supporto](https://github.com/vuejs/awesome-vue#components--libraries).

Se sei uno sviluppatore di frontend esperto e vuoi vedere un confronto tra Vue e altre librerie/framework, dai un'occhiata a [Confronto con altri Framework](comparison.html).

## Inizia

<p class="tip">La guida ufficiale presuppone la conoscenza di un livello intermedio di HTML, CSS e JavaScript. Se sei totalmente nuovo nello sviluppo del frontend, potrebbe non essere la migliore idea partire direttamente con un framework come primo passo: impara le basi e poi tornare indietro! Le precedenti esperienze con altri framework aiutano, ma non sono necessarie.</p>

Il modo più facile per provare Vue.js è usare [l'esempio Hello World di JSFiddle](https://jsfiddle.net/chrisvfritz/50wL7mdz/). Sentiti libero di aprirlo in un'altra scheda e di seguirlo mentre passiamo attraverso alcuni esempi di base. Oppure puoi <a href="https://gist.githubusercontent.com/chrisvfritz/7f8d7d63000b48493c336e48b3db3e52/raw/ed60c4e5d5c6fec48b0921edaed0cb60be30e87c/index.html" target="_blank" download="index.html">creare un file <code>index.html</code></a> ed includere Vue così:

``` html
<script src="https://cdn.jsdelivr.net/npm/vue"></script>
```

La pagina [Installazione](installation.html) mostra più modi per installare Vue. Nota: **Non** consigliamo ai principianti di iniziare con `vue-cli`, specialmente se non hai familiarità con strumenti basati su Node.js.

## Rendering dichiarativo

Al centro di Vue.js c'è un sistema che permette al DOM di mostrare i dati in modo dichiarativo usando una semplice sintassi di template:

``` html
<div id="app">
  {{ message }}
</div>
```
``` js
var app = new Vue({
  el: '#app',
  data: {
    message: 'Ciao Vue!'
  }
})
```
{% raw %}
<div id="app" class="demo">
  {{ message }}
</div>
<script>
var app = new Vue({
  el: '#app',
  data: {
    message: 'Ciao Vue!'
  }
})
</script>
{% endraw %}

Abbiamo così creato la nostra prima app Vue! Tutto ciò è molto simile al rendering di una stringa template, ma intanto Vue ha fatto molto lavoro sotto il cofano. I dati e il DOM adesso sono collegati, e ogni cosa adesso è **reattiva**. Come lo sappiamo? Apri la console JavaScript del tuo browser (in questo momento, in questa pagina) e imposta a `app.message` un diverso valore. Dovresti vedere l'esempio mostrato sopra aggiornarsi di conseguenza.

Oltre all'interpolazione del testo, possiamo anche associare attributi così:

``` html
<div id="app-2">
  <span v-bind:title="message">
    Rimani con il mouse sopra al testo per alcuni secondi
e vedrai apparire dinamicamente il titolo!
  </span>
</div>
```
``` js
var app2 = new Vue({
  el: '#app-2',
  data: {
    message: 'Hai caricato questa pagina ' + new Date().toLocaleString()
  }
})
```
{% raw %}
<div id="app-2" class="demo">
  <span v-bind:title="message">
    Rimani con il mouse sopra al testo per alcuni secondi e vedrai apparire dinamicamente il titolo!
  </span>
</div>
<script>
var app2 = new Vue({
  el: '#app-2',
  data: {
    message: 'Hai caricato questa pagina il ' + new Date().toLocaleString()
  }
})
</script>
{% endraw %}

<!-- TODO: rileggere -->

Qui stiamo incontrando qualcosa di nuovo. L'attributo `v-bind` che vedi è chiamato ** direttiva **. Le direttive hanno come prefisso `v-` per indicare che sono attributi speciali forniti da Vue e, come si può intuire, applicano un comportamento reattivo speciale al DOM renderizzato. Qui, in pratica, si dice "mantieni aggiornato l'attributo` title` di questo elemento con la proprietà `message` sull'istanza Vue."

Se apri nuovamente la tua console JavaScript e inserisci `app2.message = 'qualche nuovo messaggio'`, vedrai ancora una volta che l'HTML associato, in questo caso l'attributo` title`, è stato aggiornato.

## Condizioni e Cicli

È anche possibile attivare o disattivare la presenza di un elemento:

``` html
<div id="app-3">
  <span v-if="seen">Ora mi vedi</span>
</div>
```

``` js
var app3 = new Vue({
  el: '#app-3',
  data: {
    seen: true
  }
})
```

{% raw %}
<div id="app-3" class="demo">
  <span v-if="seen">Ora mi vedi</span>
</div>
<script>
var app3 = new Vue({
  el: '#app-3',
  data: {
    seen: true
  }
})
</script>
{% endraw %}

Apri la console ed esegui `app3.seen = false`. Dovresti veder scomparire il messaggio.

<!-- TODO: rileggere -->
Questo esempio dimostra che possiamo associare dati non solo a testo e attributi, ma anche alla ** struttura ** del DOM. Inoltre, Vue fornisce anche un potente sistema di effetti di transizione che può applicare automaticamente [effetti di transizione] (transitions.html) quando gli elementi vengono inseriti / aggiornati / rimossi da Vue.

Ci sono molte altre direttive, ognuna con le proprie funzionalità speciali. Ad esempio, la direttiva `v-for` può essere utilizzata per visualizzare un elenco di elementi che utilizzano i dati di una matrice:

``` html
<div id="app-4">
  <ol>
    <li v-for="todo in todos">
      {{ todo.text }}
    </li>
  </ol>
</div>
```
``` js
var app4 = new Vue({
  el: '#app-4',
  data: {
    todos: [
      { text: 'Studiare JavaScript' },
      { text: 'Studiare Vue.js' },
      { text: 'Sviluppare qualcosa di fantastico' }
    ]
  }
})
```
{% raw %}
<div id="app-4" class="demo">
  <ol>
    <li v-for="todo in todos">
      {{ todo.text }}
    </li>
  </ol>
</div>
<script>
var app4 = new Vue({
  el: '#app-4',
  data: {
    todos: [
      { text: 'Studiare JavaScript' },
      { text: 'Studiare Vue.js' },
      { text: 'Sviluppare qualcosa di fantastico' }
    ]
  }
})
</script>
{% endraw %}

Eseguire in console `app4.todos.push({ text: 'Nuova attività' })`. Dovresti veder nell'elenco la nuova attività.

## Gestire l'input dell'utente
<!-- TODO: rileggere -->
Per consentire agli utenti di interagire con la tua app, possiamo usare la direttiva `v-on` per allegare listener di eventi che invocano metodi sulle nostre istanze di Vue:

``` html
<div id="app-5">
  <p>{{ message }}</p>
  <button v-on:click="reverseMessage">Messaggio inverso</button>
</div>
```
``` js
var app5 = new Vue({
  el: '#app-5',
  data: {
    message: 'Ciao Vue.js!'
  },
  methods: {
    reverseMessage: function () {
      this.message = this.message.split('').reverse().join('')
    }
  }
})
```
{% raw %}
<div id="app-5" class="demo">
  <p>{{ message }}</p>
  <button v-on:click="reverseMessage">Messaggio inverso</button>
</div>
<script>
var app5 = new Vue({
  el: '#app-5',
  data: {
    message: 'Ciao Vue.js!'
  },
  methods: {
    reverseMessage: function () {
      this.message = this.message.split('').reverse().join('')
    }
  }
})
</script>
{% endraw %}

<!-- TODO: rileggere -->
Nota che in questo metodo aggiorniamo lo stato della nostra app senza toccare il DOM - tutte le manipolazioni del DOM sono gestite da Vue, e il codice che scrivi è focalizzato sulla logica sottostante.

Vue fornisce anche la direttiva `v-model` che rende l'associazione bidirezionale tra l'input del modulo e lo stato delle app un gioco da ragazzi:

``` html
<div id="app-6">
  <p>{{ message }}</p>
  <input v-model="message">
</div>
```
``` js
var app6 = new Vue({
  el: '#app-6',
  data: {
    message: 'Ciao Vue!'
  }
})
```
{% raw %}
<div id="app-6" class="demo">
  <p>{{ message }}</p>
  <input v-model="message">
</div>
<script>
var app6 = new Vue({
  el: '#app-6',
  data: {
    message: 'Ciao Vue!'
  }
})
</script>
{% endraw %}

## Componenti

<!-- TODO: rileggere -->
Il sistema dei componenti è un altro concetto importante in Vue, perché è un'astrazione che ci consente di costruire applicazioni su larga scala composte da componenti piccoli, autosufficienti e spesso riutilizzabili. Se ci pensiamo, quasi ogni tipo di interfaccia di applicazione può essere astratto in un albero di componenti:

![Component Tree](/images/components.png)

<!-- TODO: rileggere -->
In Vue, un componente è essenzialmente un'istanza Vue con opzioni predefinite. La registrazione di un componente in Vue è semplice:

``` js
// Definisci un nuovo componente chiamato 'todo-item'
Vue.component('todo-item', {
  template: '<li>Questa è una attività</li>'
})
```

Now you can compose it in another component's template:

``` html
<ol>
  <!-- Create an instance of the todo-item component -->
  <todo-item></todo-item>
</ol>
```

But this would render the same text for every todo, which is not super interesting. We should be able to pass data from the parent scope into child components. Let's modify the component definition to make it accept a [prop](components.html#Props):

``` js
Vue.component('todo-item', {
  // The todo-item component now accepts a
  // "prop", which is like a custom attribute.
  // This prop is called todo.
  props: ['todo'],
  template: '<li>{{ todo.text }}</li>'
})
```

Now we can pass the todo into each repeated component using `v-bind`:

``` html
<div id="app-7">
  <ol>
    <!--
      Now we provide each todo-item with the todo object
      it's representing, so that its content can be dynamic.
      We also need to provide each component with a "key",
      which will be explained later.
    -->
    <todo-item
      v-for="item in groceryList"
      v-bind:todo="item"
      v-bind:key="item.id">
    </todo-item>
  </ol>
</div>
```
``` js
Vue.component('todo-item', {
  props: ['todo'],
  template: '<li>{{ todo.text }}</li>'
})

var app7 = new Vue({
  el: '#app-7',
  data: {
    groceryList: [
      { id: 0, text: 'Vegetables' },
      { id: 1, text: 'Cheese' },
      { id: 2, text: 'Whatever else humans are supposed to eat' }
    ]
  }
})
```
{% raw %}
<div id="app-7" class="demo">
  <ol>
    <todo-item v-for="item in groceryList" v-bind:todo="item" :key="item.id"></todo-item>
  </ol>
</div>
<script>
Vue.component('todo-item', {
  props: ['todo'],
  template: '<li>{{ todo.text }}</li>'
})
var app7 = new Vue({
  el: '#app-7',
  data: {
    groceryList: [
      { id: 0, text: 'Vegetables' },
      { id: 1, text: 'Cheese' },
      { id: 2, text: 'Whatever else humans are supposed to eat' }
    ]
  }
})
</script>
{% endraw %}

This is a contrived example, but we have managed to separate our app into two smaller units, and the child is reasonably well-decoupled from the parent via the props interface. We can now further improve our `<todo-item>` component with more complex template and logic without affecting the parent app.

In a large application, it is necessary to divide the whole app into components to make development manageable. We will talk a lot more about components [later in the guide](components.html), but here's an (imaginary) example of what an app's template might look like with components:

``` html
<div id="app">
  <app-nav></app-nav>
  <app-view>
    <app-sidebar></app-sidebar>
    <app-content></app-content>
  </app-view>
</div>
```

### Relation to Custom Elements

You may have noticed that Vue components are very similar to **Custom Elements**, which are part of the [Web Components Spec](https://www.w3.org/wiki/WebComponents/). That's because Vue's component syntax is loosely modeled after the spec. For example, Vue components implement the [Slot API](https://github.com/w3c/webcomponents/blob/gh-pages/proposals/Slots-Proposal.md) and the `is` special attribute. However, there are a few key differences:

1. The Web Components Spec is still in draft status, and is not natively implemented in every browser. In comparison, Vue components don't require any polyfills and work consistently in all supported browsers (IE9 and above). When needed, Vue components can also be wrapped inside a native custom element.

2. Vue components provide important features that are not available in plain custom elements, most notably cross-component data flow, custom event communication and build tool integrations.

## Ready for More?

We've briefly introduced the most basic features of Vue.js core - the rest of this guide will cover them and other advanced features with much finer details, so make sure to read through it all!
