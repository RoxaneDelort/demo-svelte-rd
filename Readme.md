# Composant simple

Faire le grand ménage en supprimant tout le code relatif au template.

Intégrer le code suivant dans `App.svelte` :

```html
<script>
  let seconds = 0;
</script>

<div>
  <label>Secondes écoulées</label>
  <p>{seconds}</p>
</div>

<style>
  div {
    margin: auto;
    background: #0a0a0a;
    padding: 15px 30px;
    color: #fafafa;
  }
  p {
    font-size: 4em;
  }
</style>
```

* Le fichier contient l'intelligence (JS), la structure de donnée (HTML) et le style (CSS)
* La valeur de la variable est insérée dans l'html

## Evolution du DOM

Ajouter la fonction suivante dans la partie JS :

```js
const incrementSeconds = () => {
    seconds++;
}
setInterval(incrementSeconds, 1000);
```

* La fonction fait évoluer la valeur de la variable `seconds` toute les 1000ms (1s).
* Le DOM évolue en temps réel !

## Evénement

Ajouter le code suivant :

```html
const reset = () => {
    seconds = 0;
}
...
<button on:click={reset}>reset</button>
```

* La fonction affecte la valeur `0` à la variable `seconds`
* La fonction est appelée quand je clique sur le bouton grâce à `on:click={reset}`

## Transformer le code en composant

Créer un fichier `Timer.svelte` et déplacer le code de `App.svelte` dedans.

Importer le composant depuis `App.svelte` et l'utiliser une ou plusieurs fois.

```html
<script>
    import Timer from "./lib/Timer.svelte";
</script>

<Timer/>
<Timer/>
<Timer/>
```
