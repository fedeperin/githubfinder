<script>
	import Nav from './components/Nav.svelte'
	import Search from './components/Search.svelte'
	import Information from './components/Information.svelte'
</script>

<style>
	main {
		background: var(--background);
		width: 100vw;
		min-height: 100vh;
		display: flex;
		align-items: center;
		justify-content: center;
		padding: 75px;
	}

	.container {
		width: 600px;
		height: 100%;
		padding: 10px;
	}

	@media(max-width: 700px) {
		.container {
			width: 90%;
		}
	}

	@media(max-width: 650px) {
		main {
			padding: 50px;
		}

		.container {
			width: 95%;
		}
	}

	@media(max-width: 500px) {
		main {
			padding: 30px;
		}

		.container {
			width: 100%;
		}
	}
</style>

<main>
	<div class="container">
		<Nav />

		<Search />

		<Information />
	</div>
</main>