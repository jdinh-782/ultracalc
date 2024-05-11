<script lang='ts'>
	import Typewriter from 'svelte-typewriter';
	import Calculator from '../assets/calculators/Calculator.svelte';

	let displayMessages: Array<string> = [
		"A simple, powerful solution to the world of calculators.",
		"A faster, efficient way to perform calculations.",
		"UltraCalc"
	];
</script>


<svelte:head>
	<title>UltraCalc</title>
	<meta name="description" content="UltraCalc" />
</svelte:head>


<section>
	<Typewriter mode="loopRandom">
		{#each displayMessages as message}
			<span class="display-message">{message}</span>
		{/each}
	</Typewriter>

	<Calculator></Calculator>

	<a href="/" class="view-calculators-link">
		<span>
			View Calculators
		</span>
		<svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24" {...$$props}>
			<path fill="currentColor" d="M8.59 16.58L13.17 12L8.59 7.41L10 6l6 6l-6 6z" />
		</svg>
	</a>
</section>


<style>
	section {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		flex: 0.6;
		gap: 25px;
		font-family: monospace;
	}

	.display-message {
		font-size: 24px;
		font-weight: 600;
		font-family: inherit;
		color: var(--color-theme-3);
		width: 100%;

		@media (min-width: 480px) and (max-width: 768px) {
			font-size: 16px;
		}

		@media (max-width: 480px) {
			display: none;
		}
	}

	.view-calculators-link {
		margin-left: auto;

		@media (max-width: 1360px) {
			margin-right: 15%;
		}
	}

	a {
		display: flex;
		align-items: center;
		justify-content: center;
		text-decoration: none;
		transition: color 0.2s linear;

		& span {
			font-size: 24px;

			@media (max-width: 768px) {
				font-size: 16px;
			}
		}
	}

	a:hover {
		color: snow;
		text-decoration: none;
	}

	svg {
		width: 1.5em;
		height: 2em;
		display: block;
	}
</style>
