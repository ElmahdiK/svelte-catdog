<script>
	export let type = 'primary';
</script>

<button on:click class={type}>
	<slot />
</button>

<style>
	button {
		box-shadow: 0px 2px 2px rgba(0, 0, 0, 0.2);
		border: 0px;
		padding: 10px;
		cursor: pointer;
		text-transform: uppercase;
	}
	.primary {
		background-color: orange;
	}
	.secondary {
		background-color: dodgerblue;
	}
</style>
