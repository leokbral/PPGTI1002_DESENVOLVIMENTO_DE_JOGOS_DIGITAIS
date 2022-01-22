<script>
    import menucoverImg from "$lib/assets/menucover.png";
</script>

<div class="main" style="--bgImg: url({menucoverImg})">>
    <h1>DISEASE</h1>
    <div class="subtitle">
        <h2>WEB GAME</h2>
    </div>
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
        background-image: url(menucoverImg);
    }
    .subtitle {
        font-size: 10px;
        line-height: 1.3%;
    }
</style>
