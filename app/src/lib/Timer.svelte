<script>
    export let start = 0;
    export let max = null;
    export let title = "Secondes";
    export let step = 1000;

    let seconds = start;
    let counter = 0; 

    const incrementSeconds = () => {
        seconds++;
        if ( max && seconds >= max ) seconds = start;
    }
    setInterval(incrementSeconds, step);

    const reset = () => {
        seconds = 0;
        counter++;
    }
</script>

  
<div>
    <label>{title}</label>
    <p>{seconds}</p>
    <button on:click={reset}>reset</button>
    <span>Compteur remis à zéro {counter} fois</span>
</div>


<style>
    div {
        margin: auto;
        background: #0a0a0a;
        padding: 15px 30px;
        color: #fafafa;
        margin: 30px;
    }
    p {
        font-size: 4em;
    }
</style>