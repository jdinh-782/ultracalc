<script>
	import { page } from '$app/stores';
	import MediaQuery from '../../assets/MediaQuery.svelte';
</script>


<header>
	<div class="corner left">
		<a href="/">
			<!-- TODO: Testing out custom MediaQuery class -->
			<!-- <MediaQuery mediaQuery="(max-width: 480px)" let:matches>
				{#if matches}
					<span>U</span>
				{:else}
					<span>UltraCalc</span>
				{/if}
			</MediaQuery> -->
			<span>UltraCalc</span>
		</a>
	</div>

	<nav>
		<svg viewBox="0 0 2 3" aria-hidden="true">
			<path d="M0,0 L1,2 C1.5,3 1.5,3 2,3 L2,0 Z" />
		</svg>
		<ul>
			<li aria-current={$page.url.pathname === '/' ? 'page' : undefined}>
				<a href="/">Home</a>
			</li>
			<li aria-current={$page.url.pathname === '/about' ? 'page' : undefined}>
				<a href="/about">About</a>
			</li>
			<li aria-current={$page.url.pathname === '/calculators' ? 'page' : undefined}>
				<a href="/calculators">Calculators</a>
			</li>
			<!-- TODO: Sign up page -->
			<!-- <li aria-current={$page.url.pathname.startsWith('/sign-up') ? 'page' : undefined}>
				<a href="/sign-up">Sign Up</a>
			</li> -->
		</ul>
		<svg viewBox="0 0 2 3" aria-hidden="true">
			<path d="M0,0 L0,3 C0.5,3 0.5,3 1,2 L2,0 Z" />
		</svg>
	</nav>

	<div class="corner right">
		<a href="https://svelte.dev/">
			<span>
				Coming Soon
			</span>
		</a>
	</div>
</header>


<style>
	header {
		display: flex;
		justify-content: space-between;
		font-family: monospace;  /* TODO: Test out JetBrains Mono */
	}

	.corner {
		height: 5em;
		margin: 0 auto;
	}

	.corner a {
		display: flex;
		align-items: center;
		justify-content: center;
		text-decoration: none;
		height: 100%;
		transition: color 0.2s linear;

		@media (max-width: 768px) {
			margin-top: 25px;
		}

		& span {
			font-size: 32px;

			@media (max-width: 768px) {
				font-size: 48px;
			}
		}
	}

	.right {
		@media (max-width: 768px) {
			display: none;
		}
	}

	.corner a:hover {
		color: snow;
	}

	nav {
		display: flex;
		justify-content: center;
		--background: rgba(255, 255, 255, 0.7);

		@media (max-width: 768px) {
			display: none;
		}
	}

	svg {
		width: 2em;
		height: 3em;
		display: block;
	}

	path {
		fill: var(--background);
	}

	ul {
		position: relative;
		padding: 0;
		margin: 0;
		height: 3em;
		display: flex;
		justify-content: center;
		align-items: center;
		list-style: none;
		background: var(--background);
		background-size: contain;
	}

	li {
		position: relative;
		height: 100%;
	}

	li[aria-current='page']::before {
		--size: 6px;
		content: '';
		width: 0;
		height: 0;
		position: absolute;
		top: 0;
		left: calc(50% - var(--size));
		border: var(--size) solid transparent;
		border-top: var(--size) solid var(--color-theme-1);
	}

	nav a {
		display: flex;
		height: 100%;
		align-items: center;
		padding: 0 0.5rem;
		color: var(--color-text);
		font-weight: 700;
		font-size: 0.8rem;
		text-transform: uppercase;
		letter-spacing: 0.1em;
		text-decoration: none;
		transition: color 0.2s linear;
	}

	a:hover {
		color: var(--color-theme-1);
	}
</style>
