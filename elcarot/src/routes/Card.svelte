<script lang="ts">
	import { createEventDispatcher } from 'svelte';

	const dispatch = createEventDispatcher();

	export let arcana_number = 0;
	export let faceUp = false;
	let imageSource: any;

	$: if (faceUp) {
		imageSource = `img/arcana/arcana_${arcana_number}.png`;
	} else {
		imageSource = `img/arcana/back.png`;
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
	<img src={imageSource} alt="carot card"/>
</div>

<style lang="scss">
	.card {
		flex-grow: 1;
		display: flex;
		flex-direction: column;
		align-items: center;
	}
	img {
		// object-fit: contain;
		aspect-ratio: 910 / 1596 ;
		height: 10px;
		flex: 1 0 0 ;
	}
</style>
