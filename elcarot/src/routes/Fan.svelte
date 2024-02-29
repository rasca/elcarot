<script lang="ts">
	import { onMount } from 'svelte';

	import Card from './Card.svelte';
	import type { Nullable } from 'vitest';

	const cardsCount = 22;
	let cards = [...Array(cardsCount).keys()];
    let activeCardIndex: number | null = null;

	let deck: Element;

	const handleMouseMove = (event: MouseEvent) => {
		const rect = deck.getBoundingClientRect();
		const columnWidth = rect.width / cardsCount;
		activeCardIndex = Math.floor((event.clientX - rect.left) / columnWidth);
		console.log(activeCardIndex);
	};

	const handleMouseOut = () => {
		activeCardIndex = null;
	};
</script>

<div
 bind:this={deck}
 on:mousemove={handleMouseMove}
 on:mouseout={handleMouseOut}
 on:blur={handleMouseOut}
 role="button"
 tabindex="0"
 class="deck" style="--cardsCount: {cardsCount};"
>
	{#each cards as card, i}
	<div
	 class="card-container"
	 class:active={activeCardIndex == i}
	 class:left={activeCardIndex !== null && activeCardIndex < i}
	 class:right={activeCardIndex !== null && activeCardIndex > i}
	 class:inactive={activeCardIndex === null}
	>
		<Card arcana_number={card} faceUp={false}/>
	</div>
	{/each}
</div>

<style lang="scss">
	@mixin fan($count, $angle, $inactiveAngle) {
		@for $i from 1 through $count {
			.card-container.left:nth-child(#{$i}) {
				transform: rotate(-$angle / 2 + $angle / ($count + 1) * $i + 5deg);
			}
			.card-container.active:nth-child(#{$i}) {
				transform: translate(0, -2rem) rotate(-$angle / 2 + $angle / ($count + 1) * $i);
			}
			.card-container.right:nth-child(#{$i}) {
				transform: rotate(-$angle / 2 + $angle / ($count + 1) * $i - 5deg);
			}
			.card-container.inactive:nth-child(#{$i}) {
				transform: rotate(-$inactiveAngle / 2 + $inactiveAngle / ($count + 1) * $i);
			}
		}
	}
	.deck {
		flex-grow: 1;
		display: flex;
		align-items: center;
		position: relative;
		@include fan(22, 55deg, 35deg);
		// &:hover {
		// 	@include fan(22, 55deg);
		// }
	}
	.card-container {
		position: absolute;
		width: 100%;
		height: 100%;
		display: flex;
		align-items: center;
		flex-direction: column;
		transform-origin: center 120%;
		translate: 0 0;
		transition: transform 1s ease;
	}
</style>