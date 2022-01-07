<script lang="ts">
	// Start: Local Imports
	// Components
	import HeadTags from '$components/head-tags/HeadTags.svelte';
	import ExternalLink from '$ui/components/external-link/ExternalLink.svelte';

	// Models
	import type { IMetaTagProperties } from '$models/interfaces/imeta-tag-properties.interface';
	// End: Local Imports

	// Start: Local component properties
	/**
	 * @type {IMetaTagProperties}
	 */
	const metaData: Partial<IMetaTagProperties> = {
		title: 'About | Vincent Hirtz',
		description: 'About page of Vincent Hirtz starter project',
		url: '/about',
		keywords: ['sveltekit', 'sveltekit starter', 'sveltekit starter about'],
		searchUrl: '/about',
	};
	// End: Local component properties
</script>

<!-- Start: Header Tag -->
<HeadTags metaData="{metaData}" />
<!-- End: Header Tag -->

<!-- Start: About page section -->
<div class="flex flex-col justify-center items-start max-w-2xl mx-auto mb-16">
	<h1 class="font-bold text-3xl md:text-5xl tracking-tight mb-4 text-black dark:text-white">A propos de moi</h1>
	<div class="mb-8 prose leading-6 text-gray-600 dark:text-gray-400">
		<p> Vincent Hirtz, Web Developer </p>
		<p>
			<iframe
				src="https://www.linkedin.com/embed/feed/update/urn:li:share:6885190097365454848"
				style="height: 38rem; width: 900px;"
				height="900"
				width="504"
				frameborder="0"
				allowfullscreen=""
				title="Post intégré"></iframe>
		</p>
	</div>
</div>
<!-- End: About page section -->
