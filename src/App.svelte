<script>
	import Welcome from './components/Welcome.svelte'
	import Clouds from './components/Clouds.svelte'
	import Guess from './components/Guess.svelte'
</script>

<main>
	<div class="container">
		<div class="row">
			<Welcome />
			<Guess />
		</div>

		<Clouds />
	</div>
</main>

<style></style>