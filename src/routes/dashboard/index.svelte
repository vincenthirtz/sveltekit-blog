<script lang="ts" context="module">
	/**
	 * @type {import('@sveltejs/kit').Load}
	 */
	export async function load({ fetch }) {
		return {
			props: {
				topTracks: await fetch(`/api/top-tracks.json`).then((res) => res.json()),
			},
		};
	}
</script>

<script lang="ts">
	// Local Imports

	// Components
	import TopTracks from '$components/top-tracks/TopTracks.svelte';
	import HeadTags from '$components/head-tags/HeadTags.svelte';

	// Models
	import type { IMetaTagProperties } from '$models/interfaces/imeta-tag-properties.interface';
	import type { ITopTrack } from '$models/interfaces/itop-track.interface';

	// Exports
	export let topTracks!: ITopTrack[];

	// Start: Local component properties
	/**
	 * @type {IMetaTagProperties}
	 */
	const metaData: Partial<IMetaTagProperties> = {
		title: 'Dashboard | Vincent Hirtz',
		description: 'Dashboard page of Vincent Hirtz starter project',
		url: '/dashboard',
		keywords: ['sveltekit', 'sveltekit starter', 'sveltekit starter dashboard'],
		searchUrl: '/dashboard',
	};
</script>

<!-- Start: Header Tag -->
<HeadTags metaData="{metaData}" />
<!-- End: Header Tag -->

<div class="flex flex-col justify-center items-start max-w-2xl mx-auto mb-16">
	<h1 class="font-bold text-3xl md:text-5xl tracking-tight mb-4 text-black dark:text-white"> Dashboard </h1>
	<div class="mb-8">
		<p class="text-gray-600 dark:text-gray-400 mb-4">
			Il s'agit de la vue du tableau de bord de mon portefeuille pour suivre les métriques liées aux différentes
			plates-formes que j'utilise et qui sont disponibles pour un usage public. Pour le moment, il ne fait que
			suivre les métriques Spotify.
		</p>
	</div>
	<h2 class="font-bold text-3xl tracking-tight mb-4 mt-16 text-black dark:text-white"> Top 10 Spotify </h2>
	<p class="text-gray-600 dark:text-gray-400 mb-4">
		Curieux de savoir sur quoi je suis actuellement en train d'écouter sur Spotify ? Voici mes meilleurs morceaux
		sur Spotify mis à jour quotidiennement.
	</p>
	<TopTracks topTracks="{topTracks}" />
</div>
