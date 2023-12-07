<script lang="ts">
	export let arcana_number = 0;

	$: arcana_image = `/src/lib/images/arcana/arcana_${arcana_number}.jpg`;

</script>

<div class="card" style="--bg-img: url('{arcana_image}')">
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
