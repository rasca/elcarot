<script lang="ts">
	import Deck from './Deck.svelte';
	// import Card from './Card.svelte';
	// import welcome from '$lib/images/svelte-welcome.webp';
	// import welcome_fallback from '$lib/images/svelte-welcome.png';

	let shuffling = true;
	let interval: any;
	let arcana_number = 0;

	// $: if (shuffling) {
	// 	interval = setInterval(() => {
	// 		changeCard();
	// 	}, 100);
	// } else {
	// 	clearInterval(interval);
	// }

	let changeCard = () => {
		arcana_number = Math.floor(Math.random() * 22);
	}
</script>

<svelte:head>
	<title>El Carot</title>
	<meta name="description" content="Un mazo de los 22 arcanos mayores del Tarot. Representados por personajes que empiezan con la letra C: El Carot." />
</svelte:head>

<section>
	<p>
		Toca la pantalla cuando lo sientas para obtener tu carta
	</p>
	<Deck />
	<div class="buffer"></div>
</section>

<style>
	section {
		flex-grow: 1;
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: stretch;
	}

	.buffer {
		height: 5rem;
	}

</style>
