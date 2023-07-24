<script>
    let seconds = 0;

    const incrementSeconds = () => {
        seconds++;
    }
    setInterval(incrementSeconds, 1000);

    const reset = () => {
        seconds = 0;
    }
</script>

  
<div>
    <label>Secondes écoulées</label>
    <p>{seconds}</p>
    <button on:click={reset}>reset</button>
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