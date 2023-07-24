# Fetch

On utilisera le projet Directus de démo pour la boutique d'Amaury.

Le but est de faire une requête pour lire la liste des produits.

## Configuration de l'environnement

Dans ce projet, je vais accéder à l'api qui se trouve sur un serveur, branché à internet. Son URL est `https://xyz.directus.app`.

Vite me permet d'avoir des variables d'environnement ! Parfait pour y mettre cette url. 
Il suffit de créer un fichier `.env` à la racine du projet et de mettre des variables dedans. 

Chaque variable doit-être préfixée par `VITE_`

```
VITE_URL_DIRECTUS="https://xyz.directus.app/"
```

Côté Svelte, on peu accéder à la variable comme ceci :

```js
console.log(import.meta.env.VITE_URL_DIRECTUS);
```

## Requête

Envoi de la requête avec fetch :

```js
const endpoint = import.meta.env.VITE_URL_DIRECTUS + "items/MA_RESSOURCE";
const promise = fetch(endpoint);
```

Fetch envoi une requête sur le réseau et nous retourne une promesse. Pour attendre cette promesse, on utilise la syntaxe `async` et `await`.

Une fonction `async` peut attendre une promesse avec `await` :

```js
const getProducts = async () => {
    const endpoint = import.meta.env.VITE_URL_DIRECTUS + "items/MA_RESSOURCE";
    const promise = fetch(endpoint);
    const response = await promise;

    // Ou directement
    const response = await fetch(endpoint);
}
```

Une fois que l'on a la reponse HTTP en main, il ne manque plus qu'à extraire les données, encore avec une promesse :)

```js
const json = await response.json();
console.log(json);
```

Pour utiliser ces données dans le code, je dois affecter une variable globale de mon composants :

```js
<script>
    let products;

    const getProducts = async () => {
        const endpoint = import.meta.env.VITE_URL_DIRECTUS + "items/MA_RESSOURCE";
        const response = await fetch(endpoint);
        const json = await response.json();
	products = json.data;
    }
</script>

<pre>{products}</pre>
```

# Svelte + Promise

Svelte peut faire mieux que ça :D

Il nous fournit une structure pour attendre les promesses ! Le bloc `#await` 

Je modifie ma fonction pour qu'elle me retourne les données.

```js
<script>
    const getProducts = async () => {
        const endpoint = import.meta.env.VITE_URL_DIRECTUS + "items/MA_RESSOURCE";
        const response = await fetch(endpoint);
        const json = await response.json();
	return json.data;
    }
</script>
```

Ensuite je l'appelle dans le DOM avec `#await`. Une fonction `async` est en fait une promesse :

```js
{#await getProducts()}
    <p>Patientons...</p>
{:then products}
    <pre>{products}</pre>
{/await}
```

On affiche un bout de DOM pendant la résolution, puis un autre après. 

On peut également afficher une partie s'il y a eu une erreur :

```js
{#await getProducts()}
    <p>Patientons...</p>
{:then products}
    <pre>{products}</pre>
{:catch error}
	<p>OhOh : {error.message}</p>
{/await}
```
