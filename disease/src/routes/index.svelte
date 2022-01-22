<script>
    import menucoverImg from "$lib/assets/menucover.png";
</script>

<div class="main" style="--bgImg: url({menucoverImg});">
    <div class="subtitle" />
    <p>Como <a href="./comojogar">jogar</a></p>
    <p>Jogue com o <a href="./invasor">INVASOR</a></p>
    <p>Jogue com o <a href="./defensor">DEFENSOR</a></p>
</div>

<style>
    .main {
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        height: 97vh;
        background-image: var(--bgImg);
        background-size: contain;
        background-repeat: no-repeat;
        background-position: center;
    }
    .subtitle {
        font-size: 10px;
        line-height: 1.3%;
    }
</style>
