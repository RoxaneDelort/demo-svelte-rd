# Composant avancé

## Récap

Notre composant est une brique qui gère la vie d'un timer. Un bouton permet de remttre le timer à 0 et une fonction incrémente toutes les secondes ce timer.

On fait évoluer le composant pour compter et afficher le nombre de remises à zéro.

La variable counter est déclarée à 0.

```js
let counter = 0;
```

La fonction `reset` incrémente la variable `counter`.

```js
const reset = () => {
    seconds = 0;
    counter++;
}
```

On affiche le compteur dans le DOM

```html
<span>Compteur remis à zéro {counter} fois</span>
```

Notre composant évolue, toutes ses instances évoluent également !

## Les propriétés

On va définir, sur notre composant, un genre de paramètre. Il sera fournit par l'appelant, comme pour une fonction.

On utilise le mot clè `export`

```js
export let start;
```

Le timer ne fonctionne pas encore correctement.

On modifie l'appel du composant dans `App.svelte`

```html
<Timer start="0"/>
<Timer start="10"/>
<Timer start="30"/>
```

Chaque timer démarre avec sa propre valeur.

### Valeur par défaut

On imagine un timer générique qui démarre à 0 par défaut. Il suffit d'initialiser la variable `start` à 0.

```js
export let start=0;
```

L'attribut `start` n'est plus obligatoire lors de l'appel. On voit que désormais `Timer` attends un paramètre `start` de type `int`.

```html
<Timer/>
<Timer start=10/>
<Timer start=30/>
```

### Plusieurs

Ajoutons plusieurs paramètres à notre compteur :

```js
export let start = 0;
export let max = null;
export let title = "Secondes";
export let step = 1000;
```

Modifions le code pour les prendre en compte

```js
const incrementSeconds = () => {
    seconds++;
    if ( max && seconds >= max ) seconds = start;
}
setInterval(incrementSeconds, step);
```

```html
<label>{title}</label>
```

Enfin modifions l'appel :

```html
<Timer title="Secondes"/>
<Timer max=10 step=100 title="Dixièmes"/>
<Timer max=100 step=10 title="Centièmes"/>
```

### Sous forme d'objets

Lorsqu'on à beaucoup de paramètres à envoyer lors de l'appel, cela devient pénible.

On organise les données dans un JSON 

```js
let data = {
    start: 0,
    max: 10,
    step: 100,
    title: "Dixièmes",
}
```

On modifie ensuite l'appel du composant avec l'opérateur de décomposition `...` (spread operator).

```html
<Timer {...data}/>
```

Chaque clé du JSON est identique à un paramètre du composant. Ainsi, la valeur `Dixièmes` rangée dans la clé `title` atterit dans le paramètre `title` du composant, idem pour les autres données.


## Imbrication

On vient de se créer un chrono ! Et pourquoi pas en faire un composant ?

Créons un composant `Chrono.svelte` et insérons le code de App.svelte dedans :

```html
<script>
    import Timer from "./Timer.svelte";

    let seconds = {
        start: 0,
        step: 1000,
        title: "Seconds",
    }
    let dixiemes = {
        start: 0,
        max: 10,
        step: 100,
        title: "Dixièmes",
    }
    let centiemes = {
        start: 0,
        max: 100,
        step: 10,
        title: "Centièmes",
    }
</script>

<Timer {...seconds}/>
<Timer {...dixiemes}/>
<Timer {...centiemes}/>
```

Appelons désormais le composant `Chrono` depuis `App`

```html
<script>
    import Chrono from "./lib/Chrono.svelte";
</script>

<Chrono/>
<Chrono/>
```

Nous utilsons 2 composants, qui utilisent eux-même 2 composants.

---

Un peu de style dans `Chrono`, Rolex n'a qu'à bien se tenir !

```html
<div>
    <Timer {...seconds}/>
    <Timer {...dixiemes}/>
    <Timer {...centiemes}/>
</div>

<style>
    div {
        display: grid;
        grid-template-columns: repeat(3, 1fr);
    }
</style>
```