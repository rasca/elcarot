<script lang="ts">
	import { slide } from 'svelte/transition';

	import Deck from './Deck.svelte';
	import Loader from './Loader.svelte';
	import cards from '$lib/cards.json';

	let loading = true;
	let selectedCard: number | undefined;
	let deckComponent: Deck;

	let cardSelected = (event: any) => {
		selectedCard = event.detail;
		console.log(event);
	}

	let cardsLoaded = (event: any) => {
		loading = false;
	}

	let pickAnother = () => {
		selectedCard = undefined;
		deckComponent.reset();
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
	<Deck bind:this={deckComponent} on:select={cardSelected} on:load={cardsLoaded}/>
	{#if selectedCard !== undefined}
	<h2 class="card-title" transition:slide>{cards[selectedCard].name}</h2>
	<p class="description" transition:slide>
		{cards[selectedCard].description}
	</p>
	<button class="pick-another" on:click={pickAnother} transition:slide>
		Elige otra carta
	</button>
	{/if}
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

	.card-title {
		font-family: var(--font-titles);
		font-size: 2rem;
		text-align: center;
		margin: 1rem 0 0.5rem;
		color: var(--color-text);
	}

	.description {
		font-family: 'Georgia', 'Times New Roman', serif;
		font-size: 1.1rem;
		line-height: 1.7;
		text-align: center;
		max-width: 600px;
		margin: 0.5rem auto 1.5rem;
		padding: 0 1.5rem;
		color: var(--color-text);
	}

	.pick-another {
		display: block;
		margin: 0 auto;
		padding: 0.75rem 1.5rem;
		font-family: var(--font-titles);
		font-size: 1.2rem;
		background: transparent;
		border: 2px solid var(--color-text);
		color: var(--color-text);
		cursor: pointer;
		transition: background-color 0.2s, color 0.2s;
	}

	.pick-another:hover {
		background: var(--color-text);
		color: var(--color-bg-0);
	}

</style>
