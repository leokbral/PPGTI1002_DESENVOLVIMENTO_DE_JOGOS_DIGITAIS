<script>
    import menucoverImg from "$lib/assets/menucover.png";
</script>

<div class="main" style="--bgImg: url({menucoverImg});">
    <div class="menu">
        <button
            class="button"
            on:click={() => (window.location.href = "./invasor")}
            >Jogar com o Invasor</button
        >
        <br />
        <br />
        <button
            class="button"
            on:click={() => (window.location.href = "./defensor")}
            >Jogar com o Defensor</button
        >
        <br />
        <br />
        <button
            class="button"
            on:click={() => (window.location.href = "./comojogar")}
            >Como jogar</button
        >
    </div>
</div>

<style>
    .main {
        display: grid;
        grid-template-columns: 2fr 1fr;
        grid-template-rows: 1fr 1fr 1fr;
        height: 97vh;
        background-image: var(--bgImg);
        background-size: contain;
        background-repeat: no-repeat;
        background-position: center;
    }
    .menu {
        grid-column: 2;
        grid-row: 2;
        padding-left: 70px;
        padding-top: 20px;
    }

    .button {
        border: none;
        color: #ac77ba;
        /* padding: 15px 110px; */
        text-align: center;
        text-decoration: none;
        display: inline-block;
        font-size: 16px;
        margin: 4px 2px;
        cursor: pointer;
        background-color: #4a1079;
        width: 200px;
        height: 40px;
        border-radius: 10px;
    }
</style>
