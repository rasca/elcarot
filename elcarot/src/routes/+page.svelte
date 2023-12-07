<script>
	import Card from './Card.svelte';
	// import welcome from '$lib/images/svelte-welcome.webp';
	// import welcome_fallback from '$lib/images/svelte-welcome.png';
</script>

<svelte:head>
	<title>El Carot</title>
	<meta name="description" content="Un mazo de los 22 arcanos mayores del Tarot. Representados por personajes que empiezan con la letra C: El Carot." />
</svelte:head>

<section>
	<p>
		Toca la pantalla cuando lo sientas para obtener tu carta
	</p>
	<Card></Card>
</section>

<style>
	section {
		flex-grow: 1;
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: stretch;
	}

</style>
