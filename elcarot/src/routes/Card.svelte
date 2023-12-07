<script lang="ts">
	import { createEventDispatcher } from 'svelte';

	const dispatch = createEventDispatcher();

	export let arcana_number = 0;

	$: arcana_image = `/src/lib/images/arcana/arcana_${arcana_number}.jpg`;

</script>

<div
 class="card"
 style="--bg-img: url('{arcana_image}')"
 on:click={() => dispatch('select')}
 on:keypress={() => dispatch('select')}
 role="button"
 tabindex="0"
>
	<!-- <img src={arcana_image} alt="arcana"/> -->
</div>

<style lang="scss">
	.card {
		flex-grow: 1;
		display: flex;
		flex-direction: column;
		background-image: var(--bg-img);
		background-size: contain;
		background-repeat: no-repeat;
		background-position: center;
	}
</style>
