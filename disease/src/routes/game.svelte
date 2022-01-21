<script>
	
	let playerHand = [];
	let enemyHand = [];
	let playerGraveyard = [];
	let enemyGraveyard = [];
	let playerDeck = Array.from({ length: 40 }, () =>
		Math.floor(Math.random() * 40)
	);
	let enemyDeck = Array.from({ length: 40 }, () =>
		Math.floor(Math.random() * 40)
	);
	let playerField = [];
	let enemyField = [];

	for (let i = 0; i < 5; i++) {
		playerHand.push(playerDeck.pop());
	}

	for (let i = 0; i < 5; i++) {
		//enemyHand.push(enemyDeck.pop());
		enemyHand = [...enemyHand, enemyDeck.pop()];
	}

	const playCard = (hand, card, field) => () => {
		hand = hand.filter((c) => c !== card);
		field.push(card);
		field = field;
		console.log("h", hand, "c", card, "f", field);
	};

	const enemyPlay = (card) => {
		enemyHand = enemyHand.filter((c) => c !== card);
		enemyField.push(card);
		enemyField = enemyField;
	};

	const playerPlay = (card) => {
		playerHand = playerHand.filter((c) => c !== card);
		playerField.push(card);
		playerField = playerField;
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
		playerField = playerField.filter((c) => c !== card);
		playerGraveyard.push(card);
		playerGraveyard = playerGraveyard;
	};

	const removeFromEnemyField = (card) => {
		enemyField = enemyField.filter((c) => c !== card);
		enemyGraveyard.push(card);
		enemyGraveyard = enemyGraveyard;
	};
</script>

<div class="arena">
	<div class="enemy">
		<div class="graveyard">
			{enemyGraveyard.length}
		</div>
		<div class="hand">
			{#each enemyHand as enemyHandCard}
				<div class="card" on:dblclick={enemyPlay(enemyHandCard)}>
					{enemyHandCard}
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
				<div class="card" on:dblclick={removeFromEnemyField(enemyCard)}>
					{enemyCard}
				</div>
			{/each}
		</div>
		<div class="playerField">
			{#each playerField as playerCard}
				<div
					class="card"
					on:dblclick={removeFromPlayerField(playerCard)}
				>
					{playerCard}
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
				<div class="card" on:dblclick={playerPlay(playerHandCard)}>
					{playerHandCard}
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
		display: grid;
		grid-template-rows: 1fr 2fr 1fr;
		background: salmon;
		height: 100%;
		width: 100%;
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
		background: green;
		display: flex;
		flex-direction: column;
	}
	.player {
		grid-row-start: 3;
		grid-row-end: 4;
		background: blue;
		display: flex;
		padding: 10px;
		justify-content: center;
		align-items: center;
	}
	.deck {
		height: 80px;
		width: 50px;
		background: purple;
		border: solid;
		margin: auto;
		margin: min(5px);
	}
	.graveyard {
		height: 80px;
		width: 50px;
		background: purple;
		border: solid;
		margin: auto;
		margin: min(5px);
	}
	.hand {
		height: 100px;
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
	.card {
		height: 80px;
		width: 50px;
		background: gray;
		border: solid;
		margin: min(3px);
	}
	.enemyField {
		padding: 10px;
		display: flex;
		margin: auto;
	}
	.playerField {
		margin: auto;
		display: flex;

		padding: 10px;
	}
</style>
