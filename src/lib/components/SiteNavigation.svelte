<script lang="ts">
	import { resolve } from '$app/paths';
	import Menu from '@lucide/svelte/icons/menu';
	import Moon from '@lucide/svelte/icons/moon';
	import Sun from '@lucide/svelte/icons/sun';
	import X from '@lucide/svelte/icons/x';

	type InternalNavItem = {
		label: string;
		path: string;
		external?: false;
	};

	type ExternalNavItem = {
		label: string;
		href: string;
		external: true;
		target?: '_blank';
		rel?: string;
	};

	type NavItem = InternalNavItem | ExternalNavItem;

	let { items, theme, onToggleTheme } = $props<{
		items: NavItem[];
		theme: 'light' | 'dark';
		onToggleTheme: () => void;
	}>();

	let mobileMenuOpen = $state(false);

	const toggleMobileMenu = () => {
		mobileMenuOpen = !mobileMenuOpen;
	};

	const closeMobileMenu = () => {
		mobileMenuOpen = false;
	};

	const openExternalLink = (url: string) => {
		if (typeof window === 'undefined') {
			return;
		}

		window.open(url, '_blank', 'noreferrer');
	};
</script>

<div class="ml-auto inline-flex items-center gap-2 md:hidden!">
	<button
		class="inline-flex h-[2.2rem] w-[2.2rem] cursor-pointer items-center justify-center rounded-full border border-(--line) bg-(--card) p-0 text-(--text) transition-colors hover:border-(--highlight)"
		type="button"
		onclick={onToggleTheme}
		aria-label={theme === 'dark' ? 'Switch to light theme' : 'Switch to dark theme'}
		title={theme === 'dark' ? 'Switch to light theme' : 'Switch to dark theme'}
	>
		{#if theme === 'dark'}
			<Moon size={16} strokeWidth={2} aria-hidden="true" />
		{:else}
			<Sun size={16} strokeWidth={2} aria-hidden="true" />
		{/if}
	</button>
	<button
		class="inline-flex h-[2.2rem] w-[2.2rem] cursor-pointer items-center justify-center rounded-full border border-(--line) bg-(--card) p-0 text-(--text) transition-colors hover:border-(--highlight) aria-expanded:border-(--highlight) aria-expanded:text-(--highlight)"
		type="button"
		onclick={toggleMobileMenu}
		aria-label={mobileMenuOpen ? 'Close navigation menu' : 'Open navigation menu'}
		aria-expanded={mobileMenuOpen}
		aria-controls="mobile-primary-nav"
	>
		{#if mobileMenuOpen}
			<X size={18} strokeWidth={2.1} aria-hidden="true" />
		{:else}
			<Menu size={18} strokeWidth={2.1} aria-hidden="true" />
		{/if}
	</button>
</div>

<div class="hidden! flex-wrap items-center justify-end gap-3 md:flex!">
	<nav aria-label="Primary" class="site-nav flex flex-wrap justify-end gap-[0.8rem]">
		{#each items as item, index (item.label)}
			{#if item.external}
				<button
					type="button"
					class="nav-link-button font-['IBM_Plex_Mono',monospace]"
					onclick={() => openExternalLink(item.href)}
					style={`--nav-enter-delay: ${index * 300}ms`}
				>
					{item.label}
				</button>
			{:else}
				<a
					class="font-['IBM_Plex_Mono',monospace]"
					href={resolve(item.path)}
					style={`--nav-enter-delay: ${index * 300}ms`}
				>
					{item.label}
				</a>
			{/if}
		{/each}
	</nav>
	<button
		class="inline-flex h-[2.2rem] w-[2.2rem] cursor-pointer items-center justify-center rounded-full border border-(--line) bg-(--card) p-0 text-(--text) transition-colors hover:border-(--highlight)"
		type="button"
		onclick={onToggleTheme}
		aria-label={theme === 'dark' ? 'Switch to light theme' : 'Switch to dark theme'}
		title={theme === 'dark' ? 'Switch to light theme' : 'Switch to dark theme'}
	>
		{#if theme === 'dark'}
			<Moon size={16} strokeWidth={2} aria-hidden="true" />
		{:else}
			<Sun size={16} strokeWidth={2} aria-hidden="true" />
		{/if}
	</button>
</div>

<div
	class={`w-full overflow-hidden transition-all duration-300 ease-out md:hidden! ${mobileMenuOpen ? 'max-h-96 translate-y-0 opacity-100 pointer-events-auto' : 'max-h-0 translate-y-[-0.35rem] opacity-0 pointer-events-none'}`}
	id="mobile-primary-nav"
>
	<div class="overflow-hidden">
		<nav aria-label="Mobile primary" class="grid gap-[0.45rem] pt-[0.55rem]">
			{#each items as item (item.label)}
				{#if item.external}
					<button
						type="button"
						class="first:border-t-0 border-x-0 border-b-0 border-t border-t-[color-mix(in_srgb,var(--line)_72%,transparent)] bg-transparent px-0 py-[0.45rem] text-left font-['IBM_Plex_Mono',monospace] text-[0.84rem] uppercase tracking-[0.06em] text-(--text) transition-colors hover:text-(--primary)"
						onclick={() => {
							closeMobileMenu();
							openExternalLink(item.href);
						}}
					>
						{item.label}
					</button>
				{:else}
					<a
						class="first:border-t-0 border-t border-t-[color-mix(in_srgb,var(--line)_72%,transparent)] px-0 py-[0.45rem] font-['IBM_Plex_Mono',monospace] text-[0.84rem] uppercase tracking-[0.06em] text-(--text) no-underline transition-colors hover:text-(--primary)"
						href={resolve(item.path)}
						onclick={closeMobileMenu}
					>
						{item.label}
					</a>
				{/if}
			{/each}
		</nav>
	</div>
</div>

<style>
	.site-nav a,
	.site-nav .nav-link-button {
		color: var(--text);
		text-decoration: none;
		font-weight: 600;
		font-size: 0.95rem;
		padding: 0.25rem 0.35rem;
		border-bottom: 2px solid transparent;
		position: relative;
		opacity: 0;
		transform: translateY(-0.45rem) scale(0.94);
		animation: nav-pop 300ms cubic-bezier(0.22, 1, 0.36, 1) forwards;
		animation-delay: var(--nav-enter-delay, 0ms);
		transition: border-color 0.25s cubic-bezier(0.4, 0, 0.2, 1), color 0.18s;
	}

	.site-nav .nav-link-button {
		font-family: inherit;
		line-height: inherit;
		background: transparent;
		border-right: none;
		border-left: none;
		border-top: none;
		cursor: pointer;
	}

	@keyframes nav-pop {
		from {
			opacity: 0;
			transform: translateY(-0.45rem) scale(0.94);
		}

		to {
			opacity: 1;
			transform: translateY(0) scale(1);
		}
	}

	.site-nav a::before,
	.site-nav a::after,
	.site-nav .nav-link-button::before,
	.site-nav .nav-link-button::after {
		content: '';
		position: absolute;
		left: 0;
		width: 100%;
		height: 2px;
		background: var(--primary);
		border-radius: 2px;
		pointer-events: none;
		opacity: 0;
		transform: scaleX(0);
		transition:
			opacity 0.18s 0.18s,
			transform 0.28s cubic-bezier(0.4, 0, 0.2, 1) 0.18s;
	}

	.site-nav a::before,
	.site-nav .nav-link-button::before {
		top: 0;
	}

	.site-nav a::after,
	.site-nav .nav-link-button::after {
		top: 0;
		left: 0;
		width: 2px;
		height: 100%;
		background: var(--primary);
		border-radius: 2px;
		opacity: 0;
		transform: scaleY(0);
		transform-origin: top;
		transition:
			opacity 0.18s 0.32s,
			transform 0.28s cubic-bezier(0.4, 0, 0.2, 1) 0.32s;
	}

	.site-nav a:hover,
	.site-nav .nav-link-button:hover {
		color: var(--primary);
		border-bottom: 2px solid var(--primary);
	}

	.site-nav a:hover::before,
	.site-nav .nav-link-button:hover::before {
		opacity: 1;
		transform: scaleX(1);
		transition-delay: 0.18s, 0.18s;
	}

	.site-nav a:hover::after,
	.site-nav .nav-link-button:hover::after {
		opacity: 1;
		transform: scaleY(1);
		transition-delay: 0.32s, 0.32s;
	}

	@media (prefers-reduced-motion: reduce) {
		.site-nav a,
		.site-nav .nav-link-button {
			opacity: 1;
			transform: none;
			animation: none;
		}

		.site-nav a::before,
		.site-nav a::after,
		.site-nav .nav-link-button::before,
		.site-nav .nav-link-button::after {
			transition: none;
		}
	}
</style>
