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