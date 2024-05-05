<script>
	import Header from './header/Header.svelte';
	import './styles.css';
</script>

<div class="app">
	<Header />

	<main>
		<slot />
	</main>

	<footer>
		<span>
			© 2024 UltraCalc. All Rights Reserved.
		</span>
	</footer>
</div>

<style>
	.app {
		display: flex;
		flex-direction: column;
		min-height: 100vh;
	}

	main {
		flex: 1;
		display: flex;
		flex-direction: column;
		padding: 1rem;
		width: 100%;
		max-width: 64rem;
		margin: 0 auto;
		box-sizing: border-box;
	}

	footer {
		display: flex;
		flex-direction: row;
		justify-content: center;
		align-items: center;
		padding: 12px;
		gap: 12px;
		font-size: 10px;
		font-family: monospace;
	}

	@media (min-width: 480px) {
		footer {
			padding: 12px 0;
			font-size: 16px;
		}
	}
</style>
