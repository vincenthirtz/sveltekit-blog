<script lang="ts" context="module">
	/**
	 * @type {import('@sveltejs/kit').Load}
	 */
	export async function load({ fetch }) {
		return {
			props: {
				blogs: await fetch(`/blog.json?recent=${3}`).then((res) => res.json()),
			},
		};
	}
</script>

<script lang="ts">
	// Start: External Imports
	// End: External Imports

	// Start: Svelte Imports
	// End: Svelte Imports

	// Start: Local Imports

	// Core services

	// Utils

	// Components
	import HeadTags from '$components/head-tags/HeadTags.svelte';
	import BlogPost from '$components/blog-post/BlogPost.svelte';
	import ProjectCard from '$components/project-card/ProjectCard.svelte';
	import { projects } from '$utils/projets';
	import TradingViewWidget from 'svelte-tradingview-widget';

	// Models
	import type { IMetaTagProperties } from '$models/interfaces/imeta-tag-properties.interface';
	import type { IBlog } from '$models/interfaces/iblog.interface';
	import NowPlaying from '$components/now-playing/NowPlaying.svelte';
	// End: Local Imports

	// Exports
	export let blogs!: IBlog[];
	// Start: Local component properties
	/**
	 * @type {IMetaTagProperties}
	 */
	const metaData: Partial<IMetaTagProperties> = {
		title: `Vincent Hirtz | Dev' front `,
		description:
			'Sveltekit starter project created with sveltekit, typescript, tailwindcss, postcss, husky, and storybook. The project has the structure set up for the scaleable project. (sveltekit, typescript, tailwindcss, postcss, husky, Storybook).',
		keywords: ['sveltekit', 'sveltekit starter', 'sveltekit starter home'],
	};
	const options = { symbol: 'BINANCE:BTCUSDT', theme: 'dark', locale: 'fr', width: 600, height: 500 };
</script>

<!-- Start: Header Tag -->
<HeadTags metaData="{metaData}" />
<!-- End: Header Tag -->

<!-- Start: Home Page container -->
<div class="flex flex-col justify-center items-start max-w-2xl mx-auto mb-16">
	<h1 class="font-bold text-3xl md:text-5xl tracking-tight mb-4 text-black dark:text-white"> Bonjour, </h1>
	<p class="prose text-gray-600 dark:text-gray-400 mb-16">
		Je suis un développeur front chez <a href="https://www.sapiendo-retraite.fr/">Sapiendo</a> et je passe mon temps
		à découvrir de nouvelles technologies pour l'appliquer dans mon travail au quoitidien.
		<a sveltekit:prefetch href="/about" aria-label="about me" class="text-blue-700 hover:text-blue-800 transition"
			>En savoir plus sur moi.</a
		>
	</p>

	<!-- Start: Popular Blog Section -->
	<h2 class="font-bold text-2xl md:text-4xl tracking-tight mb-4 text-black dark:text-white">Derniers articles</h2>

	{#if blogs.length > 0}
		{#each blogs as blog, index (blog.slug)}
			<BlogPost blog="{blog}" />
		{/each}
	{/if}
	<!-- End: Popular Blog Section -->

	<!-- Start: Top Projects -->
	<h2 class="font-bold text-2xl md:text-4xl tracking-tight mb-4 mt-8 text-black dark:text-white">Derniers projets</h2>

	{#if projects.length > 0}
		{#each projects as project}
			<ProjectCard project="{project}" />
		{/each}
	{/if}
	<!-- End: Top Projects -->

	<h2 class="font-bold text-2xl md:text-4xl tracking-tight mb-4 mt-8 text-black dark:text-white"
		>En direct de Spotify</h2
	>

	<NowPlaying />

	<h2 class="font-bold text-2xl md:text-4xl tracking-tight mb-4 mt-8 text-black dark:text-white">En direct BTC</h2>

	<TradingViewWidget options="{options}" />
</div>
<!-- End: Home Page container -->
