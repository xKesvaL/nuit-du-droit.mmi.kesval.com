<script lang="ts">
	import { navigating } from '$app/stores';
	import { BRAND } from '$lib/config';
	import '$lib/styles/main.scss';
	import '$lib/styles/nprogress.scss';
	import '@kesval/design';
	import '../app.postcss';
	import nprogress from 'nprogress';
	import { setupViewTransition } from 'sveltekit-view-transition';
	import { page } from '$app/stores';

	import BackToTopButton from '$lib/components/layout/BackToTopButton.svelte';
	import Footer from '$lib/components/layout/Footer.svelte';

	nprogress.configure({ easing: 'ease', minimum: 0.2, speed: 600 });
	$: $navigating ? nprogress.start() : nprogress.done();

	setupViewTransition();
</script>

<svelte:head>
	<meta content={BRAND.author.name} name="copyright" />
	<meta content={BRAND.name} name="og:site_name" />
</svelte:head>

<main class="flex flex-col gap-4 py-8">
	<h1 class="text-center text-4xl">Nuit du droit</h1>
	<nav class="container max-w-lg bg-card rounded-xl flex gap-2 p-2">
		<a
			class="flex-1 text-center rounded-lg bg-background h-full p-2"
			class:active={$page.url.pathname === '/fete-educative'}
			href="/fete-educative">Une fête éducative</a
		>
		<a
			class="flex-1 text-center rounded-lg bg-background h-full p-2"
			class:active={$page.url.pathname === '/evenement-festif-familial'}
			href="/evenement-festif-familial">Un événement festif</a
		>
	</nav>
	<section class="section min-h-screen max-w-prose mx-auto py-4 flex flex-col gap-4">
		<slot />
	</section>
	<img
		src="/images/nuit-du-droit.webp"
		alt="nuit du droit logo"
		class="mx-auto max-w-[5rem] rounded-full"
	/>
	<div class="flex justify-center gap-4">
		<p>Reitzer Thibaud</p>
		<p>Abeddou Jordan</p>
	</div>
</main>

<BackToTopButton />

<style lang="scss">
	main {
		background: radial-gradient(circle at 28% 37%, hsl(var(--primary-300) / 0.25), transparent 50%),
			radial-gradient(circle at 70% 66%, hsl(var(--secondary-300) / 0.25), transparent 50%);

		h1 {
			font-family: var(--ft-title);
		}

		nav a {
			&.active {
				background: rgb(var(--primary));
				color: white;
			}
		}
	}
</style>
