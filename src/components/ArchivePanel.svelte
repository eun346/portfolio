<script lang="ts">
	import { onMount } from 'svelte';
	import I18nKey from '../i18n/i18nKey';
	import { i18n } from '../i18n/translation';
	import { getPostUrlBySlug } from '../utils/url-utils';

	// Props
	export let sortedPosts: Post[] = [];

	interface Post {
		slug: string;
		data: {
			title: string;
			tags: string[];
			category?: string;
			published: Date;
		};
	}

	interface Group {
		year: number;
		posts: Post[];
	}

	let tagFilters: string[] = [];
	let categoryFilters: string[] = [];
	let isUncategorizedFilter: boolean = false;

	// Helper functions
	const formatDate = (date: Date) =>
		`${(date.getMonth() + 1).toString().padStart(2, '0')}-${date
			.getDate()
			.toString()
			.padStart(2, '0')}`;

	const formatTag = (tags: string[]) => tags.map((t) => `#${t}`).join(' ');

	// onMount is used only for client-side actions like reading the URL.
	onMount(() => {
		const params = new URLSearchParams(window.location.search);
		tagFilters = params.has('tag') ? params.getAll('tag') : [];
		categoryFilters = params.has('category') ? params.getAll('category') : [];
		isUncategorizedFilter = params.has('uncategorized');
	});
	
	// Reactive statement to filter posts whenever filters or the source posts change.
	$: filteredPosts = sortedPosts.filter((p) => {
		const tagMatch = tagFilters.length ? p.data.tags?.some((t) => tagFilters.includes(t)) : true;
		const categoryMatch = categoryFilters.length ? p.data.category && categoryFilters.includes(p.data.category) : true;
		const uncategorizedMatch = isUncategorizedFilter ? !p.data.category : true;
		
		// If multiple filters are active, they should combine correctly.
		if (isUncategorizedFilter) {
			return tagMatch && uncategorizedMatch;
		}
		
		// A post must match the tag filter AND the category filter if both are present.
		return tagMatch && categoryMatch;
	});
	
	// Reactive statement to group the filtered posts by year.
	// This will automatically re-run whenever `filteredPosts` changes.
	$: groups = Object.entries(
		filteredPosts.reduce((acc, post) => {
			const year = post.data.published.getFullYear();
			if (!acc[year]) {
				acc[year] = [];
			}
			acc[year].push(post);
			return acc;
		}, {} as Record<number, Post[]>)
	)
		.map(([year, posts]) => ({
			year: Number.parseInt(year, 10), // Fix: Use Number.parseInt()
			posts,
		}))
		.sort((a, b) => b.year - a.year);

</script>

<div class="card-base px-8 py-6">
	{#each groups as group}
		<div>
			<div class="flex h-[3.75rem] w-full items-center">
				<div class="w-[15%] text-right font-bold text-2xl text-75 md:w-[10%]">
					{group.year}
				</div>
				<div class="w-[15%] md:w-[10%]">
					<div
						class="z-50 mx-auto h-3 w-3 rounded-full bg-none outline outline-3 outline-[var(--primary)] -outline-offset-[2px]"
					></div>
				</div>
				<div class="w-[70%] text-left text-50 transition md:w-[80%]">
					{group.posts.length}
					{i18n(group.posts.length === 1 ? I18nKey.postCount : I18nKey.postsCount)}
				</div>
			</div>

			{#each group.posts as post}
				<a
					href={getPostUrlBySlug(post.slug)}
					aria-label={post.data.title}
					class="group btn-plain block h-10 w-full rounded-lg hover:text-[initial]"
				>
					<div class="flex h-full items-center">
						<div class="w-[15%] text-right text-sm text-50 transition md:w-[10%]">
							{formatDate(post.data.published)}
						</div>

						<div class="dash-line relative flex h-full w-[15%] items-center md:w-[10%]">
							<div
								class="z-50 mx-auto h-1 w-1 rounded bg-[oklch(0.5_0.05_var(--hue))] outline outline-4
								outline-[var(--card-bg)] transition-all group-hover:h-5 group-hover:bg-[var(--primary)]
								group-hover:outline-[var(--btn-plain-bg-hover)] group-active:outline-[var(--btn-plain-bg-active)]"
							></div>
						</div>

						<div
							class="w-[70%] max-w-[65%] overflow-hidden overflow-ellipsis whitespace-nowrap pr-8
							text-left font-bold text-75 transition-all group-hover:translate-x-1 group-hover:text-[var(--primary)] md:w-[65%]"
						>
							{post.data.title}
						</div>

						<div
							class="hidden overflow-hidden overflow-ellipsis whitespace-nowrap text-left
							text-sm text-30 transition md:block md:w-[15%]"
						>
							{formatTag(post.data.tags)}
						</div>
					</div>
				</a>
			{/each}
		</div>
	{/each}
</div>