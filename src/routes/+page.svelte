<script>
	import Button from '../components/Button.svelte';

	let imageSrc;
	let hasError = false;
	let isFetching = false;

	$: fetchDogImage(false);

	const fetchDogImage = (breed) => {
		hasError = false;
		imageSrc = null;
		isFetching = true;
		fetch(
			breed
				? `https://dog.ceo/api/breed/african/images/random` // breeds/image/random
				: `https://api.thecatapi.com/v1/images/search`
		)
			.then((response) => response.json())
			.then((obj) => {
				imageSrc = obj.message || obj[0].url;
			})
			.catch((error) => {
				hasError = true;
			})
			.finally(() => {
				isFetching = false;
			});
	};

	const handleClick = (bool) => {
		fetchDogImage(bool);
	};
</script>

<svelte:head>
	<link href="https://fonts.googleapis.com/css?family=Roboto" rel="stylesheet" />
</svelte:head>

<main>
	<aside>
		<h1>Svelte Animals</h1>
		<p>
			Click on
			<Button
				on:click={(event) => {
					event.preventDefault();
					handleClick(false);
				}}>cat</Button
			> or
			<Button
				type="secondary"
				on:click={(event) => {
					event.preventDefault();
					handleClick(true);
				}}>dog</Button
			>
			to see a random image
		</p>
	</aside>
	<section>
		{#if hasError}
			Oops. something's wrong.
		{:else if isFetching}
			loading...
		{:else}
			<img src={imageSrc} alt="Dog" />
		{/if}
	</section>
</main>

<style>
	main {
		display: flex;
		height: 100dvh;
	}
	aside {
		background-color: #fff;
		box-shadow: 0px 2px 4px #ccc;
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		flex: 1;
		z-index: 2;
	}
	p {
		margin-top: 20px;
	}
	section {
		background-color: #fafafa;
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		flex: 2;
	}
	img {
		box-shadow: 1px 2px 10px rgba(0, 0, 0, 0.4);
		height: 400px;
	}
</style>
