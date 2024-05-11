<script lang='ts'>
	const categoriesCalculatorsList = [
		{
			category: "Math",
			calculatorNames: ["Algebra Calculator", "Calculus Calculator", "Trigonometry Calculator", "Graphing Calculator", "Statistics Calculator"]
		},
		{
			category: "Home & Auto",
			calculatorNames: ["Mortgage Calculator", "General Loan Calculator", "Auto Loan Calculator"]
		},
		{
			category: "Education",
			calculatorNames: ["GPA Calculator", "Grade Prediction Calculator"]
		},
		{
			category: "Insurance",
			calculatorNames: ["Car Insurance Calculator", "Home Insurance Calculator"]
		},
		{
			category: "Health & Fitness",
			calculatorNames: ["BMI Calculator", "Ideal Weight Calculator", "Calorie Calculator", "Macro Calculator"]
		},
		{
			category: "Finance",
			calculatorNames: ["Sales Tax Calculator", "Interest Rate Calculator", "Income Tax Calculator", "Paycheck Calculator"]
		}
	];

	const calculatorsList = categoriesCalculatorsList.flatMap(obj => obj?.calculatorNames);

	let searchInput: string = "";

	function onInputSearch(event: any) {
		const val = event?.target?.value;
		searchInput = val;
	}

	function onClickSearchButton() {
		// console.log(searchInput);
		// TODO: Check search input value and navigate to corresponding calculator page
	}
</script>


<svelte:head>
	<title>Calculators</title>
	<meta name="description" content="Calculators" />
</svelte:head>


<div class="categories-calculators-container">
	<div class="search-bar">
		<button class="search-button" on:click={() => onClickSearchButton()}>
			<svg xmlns="http://www.w3.org/2000/svg" height="36px" viewBox="0 -960 960 960" width="36px" fill="#5f6368">
				<path d="M784-120 532-372q-30 24-69 38t-83 14q-109 0-184.5-75.5T120-580q0-109 75.5-184.5T380-840q109 0 184.5 75.5T640-580q0 44-14 83t-38 69l252 252-56 56ZM380-400q75 0 127.5-52.5T560-580q0-75-52.5-127.5T380-760q-75 0-127.5 52.5T200-580q0 75 52.5 127.5T380-400Z"/>
			</svg>
		</button>

		<datalist id="calculators_datalist">
			{#each calculatorsList as calculator}
				<option>{calculator}</option>
			{/each}
		</datalist>
		<input autocomplete="on" list="calculators_datalist" class="search-calculators-input" placeholder="Search" id="search_calculators_input" on:input={($event) => onInputSearch($event)} />
	</div>

	<div class="categories-wrapper">
		{#each categoriesCalculatorsList as obj} 
			<div class="category-calculators-wrapper">
				<span class="category-name">
					{obj?.category}
				</span>

				<div class="calculators-list-wrapper">
					{#each obj?.calculatorNames as calculatorName}
						<a href="/">{calculatorName}</a>
					{/each}
				</div>
			</div>
		{/each}
	</div>
</div>


<style>
	.categories-calculators-container {
		background: whitesmoke;
		border: 2px solid black;
		display: flex;
		flex-direction: column;
		padding: 2rem;
		/* width: 100%; */
		justify-content: center;
		align-items: center;
		align-self: center;
		font-family: monospace;

		& .search-bar {
			border: 2px solid black;
			border-radius: 25px;
			background: white;
			display: inline-flex;
			flex-direction: row;
			align-items: center;
			padding: 0.5rem;

			& .search-button {
				background: transparent;
				border: none;
				cursor: pointer;
			}

			& .search-button:hover {
				filter: invert(50%);
			}

			& .search-calculators-input {
				align-self: center;
				font-size: 24px;
				padding: 1rem;
				border-radius: inherit;
				border: none;
				width: 500px;

				@media (min-width: 480px) and (max-width: 768px) {
					width: 300px;
					font-size: 18px;
				}
			}

			@media (max-width: 480px) {
				display: none;
			}
		}

		& .categories-wrapper {
			display: inline-flex;
			flex-direction: column;
			gap: 5rem;
			padding-top: 2.5rem;

			@media (max-width: 480px) {
				padding: 0;
			}

			& .category-calculators-wrapper {
				display: inline-flex;
				flex-direction: row;
				justify-content: space-between;
				gap: 7.5rem;
				width: 100%;

				@media (max-width: 768px) {
					justify-content: center;
				}

				& .category-name {
					align-self: center;
					font-size: 24px;
					font-weight: bold;

					@media (max-width: 768px) {
						display: none;
					}
				}

				& .calculators-list-wrapper {
					display: inline-flex;
					flex-direction: column;
					align-items: center;
					gap: 0.5rem;
					font-size: 20px;

					@media (max-width: 480px) {
						font-size: 14px;
					}
				}
			}
		}
	}
</style>