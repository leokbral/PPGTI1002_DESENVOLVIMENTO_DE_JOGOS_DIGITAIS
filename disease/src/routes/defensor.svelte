<script>
    import { defensorDeck } from "$lib/defensorDeck";
    import { invasorDeck } from "$lib/invasorDeck";

    import Card from "$lib/Card.svelte";

    import virusImg from "$lib/assets/virus.png";
    import bacteriumImg from "$lib/assets/bacterium.png";
    import fungusImg from "$lib/assets/fungus.png";
    import feverImg from "$lib/assets/fever.png";
    import hungryImg from "$lib/assets/hungry.png";
    import spreeImg from "$lib/assets/spree.png";
    import mutationImg from "$lib/assets/mutation.png";
    import painImg from "$lib/assets/pain.png";
    import analgesicImg from "$lib/assets/analgesic.png";
    import antibacteriumImg from "$lib/assets/antibacterium.png";
    import antifungusImg from "$lib/assets/antifungus.png";
    import antivirusImg from "$lib/assets/antivirus.png";
    import antipyreticImg from "$lib/assets/antipyretic.png";
    import checkupImg from "$lib/assets/checkup.png";
    import hygieneImg from "$lib/assets/hygiene.png";
    import lifeImg from "$lib/assets/life.png";
    import restImg from "$lib/assets/rest.png";
    import vaccineImg from "$lib/assets/vaccine.png";
    import vitaminImg from "$lib/assets/vitamin.png";
    /*import backgroundgamesong from "$lib/assets/backgroundgamesong.mp3";*/
    import graveyardsong from "$lib/assets/graveyardsong.mp3";

    var audio = new Audio(backgroundgamesong);
        audio.play();

    let playerDeck = defensorDeck.sort(() => Math.random() - 0.5);
    const botDeck = invasorDeck.sort(() => Math.random() - 0.5);

    let enemyDeck = botDeck;

    let playerTurn = false;
    let enemyTurn = true;

    let victoryCondition = 1;
    let life = 100;

    let damage = 0;
    let damageCount = 0;
    let removeVaccine = false;

    let playerHand = [];
    let enemyHand = [];
    let playerGraveyard = [];
    let enemyGraveyard = [];
    let playerField = [];
    let enemyField = [];

    for (let i = 0; i < 5; i++) {
        playerHand = [...playerHand, playerDeck.pop()];
        enemyHand = [...enemyHand, enemyDeck.pop()];
    }

    const imagesSrc = {
        virus: virusImg,
        bacterium: bacteriumImg,
        fungus: fungusImg,
        fever: feverImg,
        hungry: hungryImg,
        spree: spreeImg,
        mutation: mutationImg,
        pain: painImg,
        analgesic: analgesicImg,
        antibacterium: antibacteriumImg,
        antifungus: antifungusImg,
        antivirus: antivirusImg,
        antipyretic: antipyreticImg,
        checkup: checkupImg,
        hygiene: hygieneImg,
        life: lifeImg,
        rest: restImg,
        vaccine: vaccineImg,
        vitamin: vitaminImg,
    };

    const enemyPlay = (card) => {
        if (enemyField.length < 5) {
            if (enemyTurn) {
                enemyHand = enemyHand.filter((c) => c !== card);
                enemyField.push(card);
                enemyField = enemyField;
            }
        }
    };

    const playerPlay = (card) => {
        if (playerField.length < 5) {
            if (playerTurn) {
                playerHand = playerHand.filter((c) => c !== card);
                playerField.push(card);
                playerField = playerField;
            }
        }
    };

    const playerPullCard = () => {
        let card = playerDeck.pop();
        playerDeck = playerDeck;
        playerHand.push(card);
        playerHand = playerHand;
    };

    const enemyPullCard = () => {
        let card = enemyDeck.pop();
        enemyDeck = enemyDeck;
        enemyHand.push(card);
        enemyHand = enemyHand;
    };

    const removeFromPlayerField = (card) => {
        /* console.log("card", returnPlayerCard(cardName), cardName);
        playerField.forEach((c) =>
            console.log(c.name !== cardName, c.name, cardName)
        ); */
        playerField = playerField.filter((c) => c !== card);
        playerGraveyard.push(card);
        playerGraveyard = playerGraveyard;
        var audio = new Audio(graveyardsong);
        audio.play();
    };

    const removeFromEnemyField = (card) => {
        enemyField = enemyField.filter((c) => c !== card);
        enemyGraveyard.push(card);
        enemyGraveyard = enemyGraveyard;
        var audio = new Audio(graveyardsong);
        audio.play();
    };

    const returnPlayerCard = (cardName) => {
        return playerField.filter((c) => c.name === cardName)[0];
    };

    const returnEnemyCard = (cardName) => {
        return enemyField.filter((c) => c.name === cardName)[0];
    };

    //GAME RULES
    const paDMG = (dmgCount, initialDMG) => {
        return (dmgCount * (initialDMG + initialDMG + (dmgCount - 1) * 1)) / 2;
    };

    const pgDMG = (dmgCount, initialDMG) => {
        return initialDMG * (2 ** dmgCount - 1);
    };

    const double = (damage) => {
        return damage * 2;
    };

    const halve = (damage) => {
        life = life + damage / 2;
    };

    const block = (damage) => {
        life = life + damage;
    };

    const cure = (playerCard, enemyCard) => {
        console.log("148", playerCard, enemyCard);
        removeFromEnemyField(enemyCard);
        removeFromPlayerField(playerCard);
        damageCount = 0;
    };

    const checkup = () => {
        enemyHand.forEach((element) => {
            console.log(element);
            element.isCovered = false;
            console.log(element);
        });
    };

    const addLife = () => {
        life = life + 10;
    };

    const vaccine = (card, dmg) => {
        block(dmg);
    };

    const hygiene = (card, dmg) => {
        halve(dmg);
        removeFromPlayerField(card);
    };

    let virusIndex = null;
    let bacteriumIndex = null;
    let fungusIndex = null;
    let feverIndex = null;
    let hungryIndex = null;
    let spreeIndex = null;
    let painIndex = null;
    let mutationIndex = null;

    const desease = (card, damageType, doubleDMG) => {
        damageCount = damageCount + 1;

        let dmg = 0;

        if (damageType === "PA") {
            dmg = paDMG(damageCount, card.damage);
        } else if (damageType === "PG") {
            dmg = pgDMG(damageCount, card.damage);
        }

        if (doubleDMG) {
            dmg = double(dmg);
        }

        life = life - dmg;
        return dmg;
    };

    const checkEnemy = () => {
        let dmg = 0;
        let damageType = "PA";

        let doubleDMG = false;

        enemyField.forEach((card, index) => {
            if (card.name === "virus") {
                //virusIndex = index;
                virusIndex = "virus";
            } else if (card.name === "bacterium") {
                //bacteriumIndex = index;
                bacteriumIndex = "bacterium";
            } else if (card.name === "fungus") {
                //fungusIndex = index;
                fungusIndex = "fungus";
            } else if (card.name === "fever") {
                //feverIndex = index;
                feverIndex = "fever";
            } else if (card.name === "hungry") {
                //hungryIndex = index;
                hungryIndex = "hungry";
            } else if (card.name === "spree") {
                //spreeIndex = index;
                spreeIndex = "spree";
            } else if (card.name === "pain") {
                //painIndex = index;
                painIndex = "pain";
            } else if (card.name === "mutation") {
                //mutationIndex = index;
                mutationIndex = "mutation";
            }
        });

        if (mutationIndex) {
            damageType = "PG";
        }

        if (feverIndex) {
            doubleDMG = true;
        } else if (hungryIndex) {
            doubleDMG = true;
        } else if (spreeIndex) {
            doubleDMG = true;
        } else if (painIndex) {
            doubleDMG = true;
        }

        if (vaccineIndex) {
            if (virusIndex) {
                removeFromEnemyField(returnEnemyCard(virusIndex));
                virusIndex = null;
                removeVaccine = true;
            } else if (bacteriumIndex) {
                removeFromEnemyField(returnEnemyCard(bacteriumIndex));
                bacteriumIndex = null;
                removeVaccine = true;
            }
        }

        if (virusIndex) {
            let card = returnEnemyCard(virusIndex);
            dmg = dmg + desease(card, damageType, doubleDMG);
        }

        if (bacteriumIndex) {
            let card = returnEnemyCard(bacteriumIndex);
            dmg = dmg + desease(card, damageType, doubleDMG);
        }

        if (fungusIndex) {
            let card = returnEnemyCard(fungusIndex);
            dmg = dmg + desease(card, damageType, doubleDMG);
        }

        return dmg;
    };

    /* let vaccineIndex = null;
    let hygieneIndex = null;
    let lifeIndex = null;
    let antiVirusIndex = null;
    let antiBacteriumIndex = null;
    let antiFungusIndex = null;
    let antiPyreticIndex = null;
    let restIndex = null;
    let analgesicIndex = null;
    let vitaminIndex = null;
    let checkupIndex = null; */
    let vaccineIndex = null;

    const checkPlayer = (dmg) => {
        /* vaccineIndex = null;
        hygieneIndex = null;
        lifeIndex = null;
        antiVirusIndex = null;
        antiBacteriumIndex = null;
        antiFungusIndex = null;
        antiPyreticIndex = null;
        restIndex = null;
        analgesicIndex = null;
        vitaminIndex = null;
        checkupIndex = null; */

        vaccineIndex = null;
        let hygieneIndex = null;
        let lifeIndex = null;
        let antiVirusIndex = null;
        let antiBacteriumIndex = null;
        let antiFungusIndex = null;
        let antiPyreticIndex = null;
        let restIndex = null;
        let analgesicIndex = null;
        let vitaminIndex = null;
        let checkupIndex = null;

        playerField.forEach((card, index) => {
            if (card.name === "vaccine") {
                //vaccineIndex = index;
                vaccineIndex = "vaccine";
            } else if (card.name === "hygiene") {
                //hygieneIndex = index;
                hygieneIndex = "hygiene";
            } else if (card.name === "life") {
                lifeIndex = index;
                lifeIndex = "life";
            } else if (card.name === "antivirus") {
                //antiVirusIndex = index;
                antiVirusIndex = "antivirus";
            } else if (card.name === "antibacterium") {
                //antiBacteriumIndex = index;
                antiBacteriumIndex = "antibacterium";
            } else if (card.name === "antifungus") {
                //antiFungusIndex = index;
                antiFungusIndex = "antifungus";
            } else if (card.name === "antipyretic") {
                //antiPyreticIndex = index;
                antiPyreticIndex = "antipyretic";
            } else if (card.name === "analgesic") {
                //analgesicIndex = index;
                analgesicIndex = "analgesic";
            } else if (card.name === "rest") {
                //restIndex = index;
                restIndex = "rest";
            } else if (card.name === "vitamin") {
                //vitaminIndex = index;
                vitaminIndex = "vitamin";
            } else if (card.name === "checkup") {
                //checkupIndex = index;
                checkupIndex = "checkup";
            }
        });

        console.log(
            typeof vaccineIndex,
            vaccineIndex,
            hygieneIndex,
            lifeIndex,
            antiVirusIndex,
            antiBacteriumIndex,
            antiFungusIndex,
            antiPyreticIndex,
            restIndex,
            analgesicIndex,
            vitaminIndex,
            checkupIndex
        );

        console.log(
            typeof virusIndex,
            virusIndex,
            bacteriumIndex,
            fungusIndex,
            feverIndex,
            hungryIndex,
            spreeIndex,
            painIndex,
            mutationIndex
        );

        if (removeVaccine) {
            removeFromPlayerField(returnPlayerCard(vaccineIndex));
            //vaccineIndex = null;
            removeVaccine = false;
        }

        if (vaccineIndex) {
            let card = returnPlayerCard(vaccineIndex);
            vaccine(card, dmg);
        }

        if (hygieneIndex) {
            let card = returnPlayerCard(hygieneIndex);
            hygiene(card, dmg);
        }

        if (lifeIndex) {
            let card = returnPlayerCard(lifeIndex);
            addLife(card, dmg);
            removeFromPlayerField(card);
        }

        if (checkupIndex) {
            let card = returnPlayerCard(checkupIndex);
            checkup();
            removeFromPlayerField(card);
        }

        if (virusIndex) {
            console.log(virusIndex);
            if (antiVirusIndex) {
                console.log(antiVirusIndex);
                let playerCard = returnPlayerCard(antiVirusIndex);
                let enemyCard = returnEnemyCard(virusIndex);
                cure(playerCard, enemyCard);
                virusIndex = null;
            }
        }
        if (bacteriumIndex) {
            if (antiBacteriumIndex) {
                let playerCard = returnPlayerCard(antiBacteriumIndex);
                let enemyCard = returnEnemyCard(bacteriumIndex);
                cure(playerCard, enemyCard);
                bacteriumIndex = null;
            }
        }
        if (fungusIndex) {
            if (antiFungusIndex) {
                let playerCard = returnPlayerCard(antiFungusIndex);
                let enemyCard = returnEnemyCard(fungusIndex);
                cure(playerCard, enemyCard);
                fungusIndex = null;
            }
        }
        if (feverIndex) {
            if (antiPyreticIndex) {
                let playerCard = returnPlayerCard(antiPyreticIndex);
                let enemyCard = returnEnemyCard(feverIndex);
                cure(playerCard, enemyCard);
                feverIndex = null;
            }
        }
        if (hungryIndex) {
            if (vitaminIndex) {
                let playerCard = returnPlayerCard(vitaminIndex);
                let enemyCard = returnEnemyCard(hungryIndex);
                cure(playerCard, enemyCard);
                hungryIndex = null;
            }
        }
        if (spreeIndex) {
            if (restIndex) {
                let playerCard = returnPlayerCard(restIndex);
                let enemyCard = returnEnemyCard(spreeIndex);
                cure(playerCard, enemyCard);
                spreeIndex = null;
            }
        }
        if (painIndex) {
            if (analgesicIndex) {
                let playerCard = returnPlayerCard(analgesicIndex);
                let enemyCard = returnEnemyCard(painIndex);
                cure(playerCard, enemyCard);
                painIndex = null;
            }
        }
    };

    const fight = () => {
        damage = checkEnemy();
        checkPlayer(damage);
        if (life < 0) {
            alert("GAME OVER! Desease wins!");
            window.location.href = "http://localhost:3000/";
        }

        if (
            playerDeck.length < victoryCondition ||
            enemyDeck.length < victoryCondition
        ) {
            alert("GAME OVER! You win!");
            window.location.href = "http://localhost:3000/";
        }
        enemyPullCard();
        playerPullCard();
    };

    const toggle = () => {
        playerTurn = !playerTurn;
        enemyTurn = !enemyTurn;
    };

    const playerCheck = () => {
        if (playerTurn) {
            fight();
            toggle();
        }
    };

    const enemyCheck = () => {
        if (enemyTurn) {
            toggle();
        }
    };
</script>

<div class="arena">
    <div class="enemy">
        <div class="graveyard">
            {enemyGraveyard.length}
        </div>
        <div class="hand">
            {#each enemyHand as enemyHandCard}
                <div on:dblclick={enemyPlay(enemyHandCard)}>
                    <Card
                        imgAlt={enemyHandCard.name}
                        imgSrc={imagesSrc[enemyHandCard.name]}
                        isCovered={enemyHandCard.isCovered}
                    />
                </div>
            {/each}
        </div>
        <div class="deck" on:dblclick={enemyPullCard}>
            {enemyDeck.length}
        </div>
    </div>
    <div class="board">
        <div class="enemyField">
            {#each enemyField as enemyCard}
                <div on:dblclick={removeFromEnemyField(enemyCard)}>
                    <Card
                        imgAlt={enemyCard.name}
                        imgSrc={imagesSrc[enemyCard.name]}
                        isCovered={false}
                    />
                </div>
            {/each}
        </div>
        <div class="hud">
            <button class="check-enemy" on:click={enemyCheck} class:turn={enemyTurn}
                >invasorChek</button
            >
            <p class="life">{life}</p>
            <button class="check-player" on:click={playerCheck} class:turn={playerTurn}
                >defensorCheck</button
            >
        </div>
        <div class="playerField">
            {#each playerField as playerCard}
                <div on:dblclick={removeFromPlayerField(playerCard)}>
                    <Card
                        imgAlt={playerCard.name}
                        imgSrc={imagesSrc[playerCard.name]}
                        isCovered={false}
                    />
                </div>
            {/each}
        </div>
    </div>
    <div class="player">
        <div class="deck" on:dblclick={playerPullCard}>
            {playerDeck.length}
        </div>
        <div class="hand">
            {#each playerHand as playerHandCard}
                <div on:dblclick={playerPlay(playerHandCard)}>
                    <Card
                        imgAlt={playerHandCard.name}
                        imgSrc={imagesSrc[playerHandCard.name]}
                        isCovered={false}
                    />
                </div>
            {/each}
        </div>
        <div class="graveyard">
            {playerGraveyard.length}
        </div>
    </div>
</div>

<style>
    .arena {
        margin: auto;
        display: grid;
        grid-template-rows: 1fr 2fr 1fr;
        background: salmon;
        height: 95vh;
        width: 95vw;
        background-image: url(https://previews.123rf.com/images/flas100/flas1001710/flas100171000142/88488655-brown-wooden-table-top-near-scratched-grunge-wallpaper-.jpg);
    }
    .enemy {
        grid-row-start: 1;
        grid-row-end: 2;
        display: flex;
        padding: 10px;
    }
    .board {
        grid-row-start: 2;
        grid-row-end: 3;
        /* background: green; */
        display: flex;
        flex-direction: column;
    }
    .player {
        grid-row-start: 3;
        grid-row-end: 4;
        /* background: blue; */
        display: flex;
        padding: 10px;
        justify-content: center;
        align-items: center;
    }
    .deck {
        height: 80px;
        width: 50px;
        background: darkslategray;
        border: solid;
        border-radius: 10px;
        margin: auto;
        margin: min(5px);
        display: flex;
        align-items: center;
        justify-content: center;
        border-width: 2px;
        color: whitesmoke;
        border-color: black;
    }
    .graveyard {
        height: 80px;
        width: 50px;
        background: darkslategray;
        border: solid;
        border-width: 2px;
        border-color: black;
        border-radius: 10px;
        margin: auto;
        margin: min(5px);
        display: flex;
        align-items: center;
        justify-content: center;
        color: whitesmoke;
    }
    .hand {
        height: 100%;
        width: 1fr;
        min-width: 300px;
        background: purple;
        border: solid;
        display: flex;
        align-items: center;
        margin: auto;
        padding-left: 10px;
        padding-right: 10px;
    }

    .check-player {
        margin-bottom: -80px;
        height: 50px;
    }
    .check-enemy {
        margin-top: -80px;
        height: 50px;
    }

    .life {
        margin: 30px;
    }
    /* .card {
        height: 80px;
        width: 50px;
        background: gray;
        border: solid;
        margin: min(3px);
    } */

    .hud {
        align-self: flex-end;
        justify-content: center;
        align-items: center;
        margin-right: 100px;
        display: flex;
        flex-direction: column;
        background-color: yellow;
    }
    .enemyField {
        padding: 10px;
        display: flex;
        margin: auto;
        height: 140px;
    }
    .playerField {
        margin: auto;
        display: flex;
        padding: 10px;
        height: 140px;
    }

	.turn {
        background-color: green;
    }
</style>
