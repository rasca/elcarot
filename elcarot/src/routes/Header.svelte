<script>
	import { page } from '$app/stores';
	import logo from '$lib/images/stars.png';
	import github from '$lib/images/github.svg';
</script>

<div>
	<header>
		<h1>El Carot</h1>
	</header>
	<hr />
</div>

<style lang="scss">
	header {
		display: flex;
		align-items: center;
		position: relative;
		h1 {
			text-transform: uppercase;
			flex-grow: 1;
			margin: 0;
		}
		margin: 1rem 0;
	}

	hr {
		display:block;
		border:0;
		height:10px;
		background: url('$lib/images/three-stars.svg') no-repeat center;
		position: relative;
		&:after {
			content: '';
			height: 1px;
			width: 100%;
			background-color: rgba(0, 0, 0, 0.05);
			position: absolute;
			top: 50%;
		}
	}
</style>
