<script lang='ts'>
    import { e, evaluate } from 'mathjs';
    import { onMount } from 'svelte';

    // TODO: Test more inputs
    let inputGrid: Array<Array<string>> = [
		['AC', 'C', '%', '÷'],
		['7', '8', '9', '×'], 
		['4', '5', '6', '-'],
		['1', '2', '3', '+'],
		['0', '.', '±', '=']
	];

    let currentInput: string = '0';
    let previousCalculation: string = "Previous calculation appears here.";

    interface StoredCalculation {
		expression: string,
		result: string
	};
    let storedCalculations: Array<StoredCalculation> = [];
    let storedCalculationsDialog: any;

    onMount(() => {
        storedCalculationsDialog = document.getElementById("stored_calculations_dialog");
    })

    // TODO: Add typing input functionality
	function getInputValue(value: string): void {
        if (currentInput === "Error") {
            currentInput = '';
        }

		if (value === 'AC') {
			currentInput = '0';
			return;
		}

		if (value === 'C') {
			if (currentInput?.length > 0) {
				currentInput = currentInput?.slice(0, -1);
			}
			else {
				currentInput = '0';
			}
			return;
		}

		if (value === '=') {
            if (currentInput?.length > 1) {
                calculate();
            }
            else {
                currentInput = '0';
            }
			return;
		}

		if (value === '±') {
			const lastValue = currentInput?.slice(-1);

			if (lastValue === '+') {
				currentInput = currentInput.replace(/.$/, '-');
			}
			else if (lastValue === '-') {
				currentInput = currentInput.replace(/.$/, '+');
			}
			else {
				currentInput = currentInput.concat('', '+');
			}
			return;
		}

		if (currentInput === '0' && value !== '.') {
			currentInput = '';
		}

		currentInput = currentInput.concat('', value);
	}

    function calculate(): void {
        try {
            currentInput = currentInput.replace('÷', '/');
            currentInput = currentInput.replace('×', '*');
            const result = evaluate(currentInput);

            previousCalculation = `${currentInput} = ${result?.toString()}`;
            storedCalculations = [...storedCalculations, {expression: currentInput?.toString(), result: result?.toString()}];

            currentInput = result?.toString();
        }
        catch (e) {
            console.error(e);
            currentInput = "Error";
        }
    }

    function showStoredCalculations(): void {
        storedCalculationsDialog.showModal();
    }
</script>


<div class="calculator-container">
    <div class="top-row-info-wrapper">
        <button class="stored-calculations-button" on:click={() => showStoredCalculations()}>
            <svg xmlns="http://www.w3.org/2000/svg" height="36px" viewBox="0 -960 960 960" width="36px" fill="#5f6368">
                <path d="M120-560v-240h80v94q51-64 124.5-99T480-840q150 0 255 105t105 255h-80q0-117-81.5-198.5T480-760q-69 0-129 32t-101 88h110v80H120Zm2 120h82q12 93 76.5 157.5T435-204l48 84q-138 0-242-91.5T122-440Zm412 70-94-94v-216h80v184l56 56-42 70ZM719 0l-12-60q-12-5-22.5-10.5T663-84l-58 18-40-68 46-40q-2-13-2-26t2-26l-46-40 40-68 58 18q11-8 21.5-13.5T707-340l12-60h80l12 60q12 5 23 11.5t21 14.5l58-20 40 70-46 40q2 13 2 25t-2 25l46 40-40 68-58-18q-11 8-21.5 13.5T811-60L799 0h-80Zm40-120q33 0 56.5-23.5T839-200q0-33-23.5-56.5T759-280q-33 0-56.5 23.5T679-200q0 33 23.5 56.5T759-120Z"/>
            </svg>
        </button>

        <dialog id="stored_calculations_dialog" class="stored-calculations-dialog" bind:this={storedCalculationsDialog} on:close>
            <h1>Stored Calculations</h1>

            {#if storedCalculations?.length > 0}
                <div class="stored-calculations-wrapper">
                    {#each storedCalculations as calculation}
                        <div class="stored-calculation-info">
                            <span>{calculation?.expression}</span>
                            <span> = </span>
                            <span>{calculation?.result}</span>
                        </div>
                    {/each}
                </div>
            {:else}
                <span>Your previous expressions and answers will be stored here.</span>
            {/if}

            <button class="close-dialog-button" on:click={() => {storedCalculationsDialog.close()}}>Close</button>
        </dialog>
    
        <span class="previous-calculation">{previousCalculation}</span>
    </div>

    <span class="calculator-input">{currentInput}</span>
    
    <span class="divider"></span>

    <div class="inputs-grid">
        {#each inputGrid as row}
        <div class="row">
            {#each row as cell}
                <button class="cell" on:click={() => getInputValue(cell?.toString())}>
                    <strong>{cell}</strong>
                </button>
            {/each}
        </div>
        {/each}
    </div>

</div>


<style>
    .divider {
		content: "";
		color: var(--color-theme-3);
		width: 100%;
		height: 25px;
		border-top: 2px solid var(--color-theme-3);
	}

    .calculator-container {
		width: 100%;
		background-color: snow;
		border-radius: 25px;
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		padding: 20px;
		border: 4px solid var(--color-theme-1);
		transition: box-shadow 0.2s linear;

		@media (max-width: 1360px) {
			width: 75%;
		}

        & .top-row-info-wrapper {
            display: inline-flex;
            flex-direction: row;
            align-items: center;
            width: 100%;

            & .stored-calculations-button {
                margin-right: auto;
                cursor: pointer;
                background: transparent;
                border: none;
            }

            & .stored-calculations-button:hover {
                filter: invert(50%);
            }

            & .stored-calculations-dialog {
                max-width: 100%;
                text-align: right;

                & h1 {
                    text-align: center;
                }
                
                & .stored-calculations-wrapper {
                    width: 100%;
                    display: inline-flex;
                    flex-direction: column;
                    align-items: center;
                    text-align: center;
                    gap: 1rem;

                    & .stored-calculation-info {
                        display: inline-flex;
                        flex-direction: row;
                        gap: .5rem;
                        border: 2px solid black;
                        padding: .5rem;

                        & span {
                            font-size: 24px;
                        }
                    }
                }

                & .close-dialog-button {
                    background: transparent;
                    cursor: pointer;
                    font-size: 16px;
                    margin-top: 2rem;
                }
            }

            & .previous-calculation {
                margin-left: auto;
                font-size: 14px;
            }

            @media (max-width: 768px) {
                display: none;
            }
        }

		& .calculator-input {
			margin-left: auto;
			font-size: 64px;
			color: var(--color-theme-3);
			caret-color: transparent;
			text-decoration: none;
			user-select: none;
			text-overflow: ellipsis;
			background: none;
			border: none;
			outline: none;
			text-align: right;
			width: 100%;
			
			@media (max-width: 768px) {
				font-size: 32px;
			}
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

				@media (max-width: 768px) {
					gap: 10px;
				}

				& .cell {
					font-size: 24px;
					width: 100%;
					border: 2px solid var(--color-theme-1);
					border-radius: 25px;
					text-align: center;
					transition: background-color 0.2s linear;
					background-color: snow;
					padding: 10px;
					color: var(--color-theme-3);

					@media (max-width: 768px) {
						font-size: 12px;
					}
				}

				& .cell:hover {
					cursor: pointer;
					background-color: whitesmoke;
				}

				& .cell:focus {
					background-color: #E5E4E2;
					visibility: hidden;
					opacity: 0;
					transition: visibility 0s 0.1s, opacity 0.5s linear;
				}
			}
		}
	}

	.calculator-container:hover {
		box-shadow: 0px -5px 10px 0px var(--color-theme-1);
	}
</style>