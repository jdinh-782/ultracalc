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
</script>


<svelte:head>
	<title>Calculators</title>
	<meta name="description" content="Calculators" />
</svelte:head>


<div class="categories-calculators-container">
	<div class="search-bar">
		<datalist id="calculators_datalist">
			{#each calculatorsList as calculator}
				<option>{calculator}</option>
			{/each}
		</datalist>
		<input autocomplete="on" list="calculators_datalist" class="search-calculators-input" id="search_calculators_input" />
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