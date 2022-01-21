<script>
    export let isCovered;
    export let imgSrc;
    export let imgAlt;
</script>

<div class="card">
    {#if !isCovered}
        <img src={imgSrc} alt={imgAlt} height="143px" width="102px" class="imagem">
    {/if}
    
</div>

<style>

.card {
		height: 140px;
		width: 100px;
		background: darkslategray;
		margin: min(3px);
        border: solid;
        border-width: 2px;
        border-radius: 10px;
        
	}

.imagem {
    margin: -1px 0 0 -2px;
    object-fit: fill;
    border-radius: 10px;
}
</style>