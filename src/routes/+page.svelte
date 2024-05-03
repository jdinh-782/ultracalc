<script lang='ts'>
	import Typewriter from 'svelte-typewriter';

	let displayMessages: Array<string> = [
		"An easier way to perform calculations.",
		"A simple, powerful solution to the world of calculators.",
		"UltraCalc"
	];

	let inputGrid: Array<Array<string>> = [
		['(', ')', '%', 'AC'],
		['7', '8', '9', '÷'], 
		['4', '5', '6', '×'],
		['1', '2', '3', '-'],
		['0', '.', '=', '+']
	];

	let currentInput: string = '0';

	interface StoredCalculation {
		expression: string,
		result: string
	};
	let storedCalculations: Array<StoredCalculation> = [];

	// TODO: Add typing input functionality
	function getInputValue(value: string): void {
		if (value === 'AC') {
			currentInput = '0';
			return;
		}

		if (value === '=') {
			calculate();
			return;
		}

		if (currentInput === '0' && value !== '.') {
			currentInput = '';
		}
		currentInput = currentInput.concat('', value);
	}

	function calculate(): void {
		try {
			let finalInput = currentInput.replace('×', '*');
			finalInput = finalInput.replace('÷', '/');

			let result = eval(finalInput);

			storedCalculations.push({
				expression: currentInput.toString(),
				result: result.toString()
			});
			currentInput = result.toString();
		}
		catch (e) {
			alert(e);
		}
	}
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

	<div class="calculator-container">
		<span class="digit-input">{currentInput}</span>
		
		<span class="divider"></span>

		<div class="inputs-grid">
			{#each inputGrid as row}
			<div class="row">
				{#each row as cell}
				<button class="cell" on:click={() => getInputValue(cell.toString())}>
					<strong>{cell}</strong>
				</button>
				{/each}
			</div>
			{/each}
		</div>

	</div>

	<a href="https://github.com/sveltejs/kit" target="_blank" class="view-calculators-link">
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
		font-family: inherit;
		color: black;
		width: 100%;
	}

	.calculator-container {
		width: 75%;
		background-color: snow;
		border-radius: 25px;
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		padding: 20px;

		& .digit-input {
			margin-left: auto;
			font-size: 64px;
			color: black;
		}

		& .inputs-grid {
			display: flex;
			flex-direction: column;
			justify-content: center;
			align-items: center;
			gap: 25px;
			width: 100%;

			& .row {
				display: inline-flex;
				flex-direction: row;
				justify-content: center;
				align-items: center;
				gap: 25px;
				width: 100%;

				& .cell {
					font-size: 24px;
					width: 100%;
					border: 1px solid black;
					border-radius: 25px;
					text-align: center;
					transition: background-color 0.2s linear;
					background-color: snow;
					padding: 10px;
					color: var(--color-theme-1);
				}

				& .cell:hover {
					cursor: pointer;
					background-color: whitesmoke;
				}

				& .cell:focus {
					background-color: silver;
					visibility: hidden;
					opacity: 0;
					transition: visibility 0s 0.1s, opacity 0.5s linear;
				}
			}
		}
	}

	.divider {
		content: "";
		color: black;
		width: 100%;
		height: 25px;
		border-top: 2px solid black;
	}

	.view-calculators-link {
		margin-left: auto;
		margin-right: 10%;
	}

	a {
		display: flex;
		align-items: center;
		justify-content: center;
		text-decoration: none;
		transition: color 0.2s linear;

		& span {
			font-size: 24px;
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
