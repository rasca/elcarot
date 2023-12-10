<script lang="ts">
	import { createEventDispatcher } from 'svelte';

	const dispatch = createEventDispatcher();

	export let arcana_number = 0;
	export let faceUp = false;
	let imageSource: any;

	$: if (faceUp) {
		imageSource = `/src/lib/images/arcana/arcana_${arcana_number}.jpg`;
	} else {
		imageSource = `/src/lib/images/arcana/back.jpg`;
	}

</script>

<div
 class="card"
 style="--bg-img: url('{imageSource}')"
 on:click={() => dispatch('select')}
 on:keypress={() => dispatch('select')}
 role="button"
 tabindex="0"
>
	<div class="img"></div>
</div>

<style lang="scss">
	.card {
		flex-grow: 1;
		display: flex;
		flex-direction: row;
		height: 50%;
		width: 50%;
		justify-content: center;
	}
	.img {
		aspect-ratio: 910 / 1596 ;
		background-image: var(--bg-img);
		background-size: contain;
		background-repeat: no-repeat;
		background-position: center;
		border-radius: 1rem;
		box-shadow: -1px -1px 2px 2px transparentize(black, 0.8);
	}
</style>
