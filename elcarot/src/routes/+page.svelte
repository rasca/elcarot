<script lang="ts">
	import { slide } from 'svelte/transition';

	import Deck from './Deck.svelte';
	import Loader from './Loader.svelte';

	let loading = true;

	let selectedCard: number | undefined;

	let cardSelected = (event: any) => {
		selectedCard = event.detail;
		console.log(event);
	}

	let cardsLoaded = (event: any) => {
		loading = false;
	}

</script>

<svelte:head>
	<title>El Carot</title>
	<meta name="description" content="Un mazo de los 22 arcanos mayores del Tarot. Representados por personajes que empiezan con la letra C: El Carot." />
</svelte:head>

<section>
	{#if loading}
	<Loader/>
	{:else if selectedCard === undefined}
	<p transition:slide>
		Toca la pantalla cuando lo sientas para obtener tu carta
	</p>
	{/if}
	<Deck on:select={cardSelected} on:load={cardsLoaded}/>
	<div class="buffer"></div>
</section>

<style>
	section {
		flex-grow: 1;
		display: flex;
		flex-direction: column;
		justify-content: center;
	}

	.buffer {
		height: 5rem;
	}

</style>
