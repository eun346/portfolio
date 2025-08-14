<script lang="ts">
import { onMount } from "svelte";
import I18nKey from "../i18n/i18nKey";
import { i18n } from "../i18n/translation";
import { getPostUrlBySlug } from "../utils/url-utils";

export let tags: string[] = [];
export let categories: string[] = [];
export let sortedPosts: Post[] = [];

const params = new URLSearchParams(window.location.search);
tags = params.has("tag") ? params.getAll("tag") : [];
categories = params.has("category") ? params.getAll("category") : [];
const uncategorized = params.get("uncategorized");

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

let groups: Group[] = [];

const formatDate = (date: Date) =>
	`${(date.getMonth() + 1).toString().padStart(2, "0")}-${date
		.getDate()
		.toString()
		.padStart(2, "0")}`;

const formatTag = (tags: string[]) => tags.map((t) => `#${t}`).join(" ");

onMount(() => {
	let filtered = sortedPosts;

	if (tags.length)
		filtered = filtered.filter((p) => p.data.tags?.some((t) => tags.includes(t)));

	if (categories.length)
		filtered = filtered.filter((p) => p.data.category && categories.includes(p.data.category));

	if (uncategorized) filtered = filtered.filter((p) => !p.data.category);

	const grouped: Record<number, Post[]> = {};
	for (const post of filtered) {
		const year = post.data.published.getFullYear();
		if (!grouped[year]) grouped[year] = [];
		grouped[year].push(post);
	}

	groups = Object.keys(grouped)
		.map((y) => {
			const year = parseInt(y, 10);
			return { year, posts: grouped[year] };
		})
		.sort((a, b) => b.year - a.year);
});
</script>

<div class="card-base px-8 py-6">
	{#each groups as group}
		<div>
			<div class="flex items-center h-[3.75rem] w-full">
				<div class="w-[15%] md:w-[10%] text-right font-bold text-2xl text-75">
					{group.year}
				</div>
				<div class="w-[15%] md:w-[10%]">
					<div
						class="h-3 w-3 bg-none rounded-full outline outline-[var(--primary)] mx-auto -outline-offset-[2px] z-50 outline-3"
					></div>
				</div>
				<div class="w-[70%] md:w-[80%] text-left text-50 transition">
					{group.posts.length} {i18n(group.posts.length === 1 ? I18nKey.postCount : I18nKey.postsCount)}
				</div>
			</div>

			{#each group.posts as post}
				<a
					href={getPostUrlBySlug(post.slug)}
					aria-label={post.data.title}
					class="group btn-plain block h-10 w-full rounded-lg hover:text-[initial]"
				>
					<div class="flex items-center h-full">
						<!-- date -->
						<div class="w-[15%] md:w-[10%] text-right text-sm text-50 transition">
							{formatDate(post.data.published)}
						</div>

						<!-- dot and line -->
						<div class="w-[15%] md:w-[10%] relative dash-line flex items-center h-full">
							<div
								class="mx-auto w-1 h-1 rounded transition-all group-hover:h-5
                     bg-[oklch(0.5_0.05_var(--hue))] group-hover:bg-[var(--primary)]
                     outline outline-4 z-50 outline-[var(--card-bg)]
                     group-hover:outline-[var(--btn-plain-bg-hover)]
                     group-active:outline-[var(--btn-plain-bg-active)]"
							></div>
						</div>

						<!-- post title -->
						<div
							class="w-[70%] md:max-w-[65%] md:w-[65%] font-bold text-left text-75 pr-8
                     whitespace-nowrap overflow-ellipsis overflow-hidden
                     group-hover:translate-x-1 transition-all group-hover:text-[var(--primary)]"
						>
							{post.data.title}
						</div>

						<!-- tag list -->
						<div
							class="hidden md:block md:w-[15%] text-left text-sm
                     whitespace-nowrap overflow-ellipsis overflow-hidden text-30 transition"
						>
							{formatTag(post.data.tags)}
						</div>
					</div>
				</a>
			{/each}
		</div>
	{/each}
</div>
