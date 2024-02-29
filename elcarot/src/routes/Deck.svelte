<script lang="ts">
	import { onMount } from 'svelte';
	import { createEventDispatcher } from 'svelte';

	import Card from './Card.svelte';

	const dispatch = createEventDispatcher();

	const cardsCount = 22;
	let cards = [...Array(cardsCount).keys()];
    let activeCardIndex: number = 0;

	let loading = true;
	let error = false;
	let selected = false;

	let deck: Element;

	let select = (event: any) => {
		// stop the interval
		selected = true;
		dispatch('select', activeCardIndex);
	}

	// Function to preload a single image
	function preloadImage(url: string) {
		return new Promise((resolve, reject) => {
			const img = new Image();
			img.src = url;
			img.onload = resolve;
			img.onerror = reject;
		});
  }

	// Preload all images and trigger an event when done
	onMount(() => {
		Promise.all(cards.map(card => preloadImage(`/src/lib/images/arcana/arcana_${card}.png`)))
		.then(() => {
			loading = false;
			dispatch('load');

			// Request the next frame
			requestAnimationFrame(changeImage);
		})
		.catch(error => {
			error = true;
		});
	});

	 let selectNewCard = () => {
		let newIndex = Math.floor(Math.random() * (cardsCount - 1));
		if (newIndex >= activeCardIndex) {
			newIndex++;
		}
		activeCardIndex = newIndex;
	}

	let lastTimestamp = 0;
	function changeImage(timestamp: number) {
		if (selected) {
			return;
		}
		// Check if 100ms have passed since the last image update
		if (timestamp - lastTimestamp > 100) {
			selectNewCard();
			lastTimestamp = timestamp; // Update the timestamp of the last change
		}
		requestAnimationFrame(changeImage);
	}

</script>

<div
 bind:this={deck}
 on:click={select}
 on:keydown={select}
 role="button"
 tabindex="0"
 class="deck"
>
	{#if error }
	error
	{:else if !loading}
	<Card arcana_number={activeCardIndex} faceUp={true}/>
	{/if}
</div>

<style lang="scss">
	.deck {
		flex-grow: 1;
		display: flex;
		flex-direction: column;
	}
</style>