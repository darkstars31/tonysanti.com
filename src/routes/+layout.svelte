<script lang="ts">
	import { onMount } from 'svelte';
	import { resolve } from '$app/paths';
	import Menu from '@lucide/svelte/icons/menu';
	import Moon from '@lucide/svelte/icons/moon';
	import Sun from '@lucide/svelte/icons/sun';
	import X from '@lucide/svelte/icons/x';
	import './layout.css';
	import faceProfile from '$lib/assets/faceprofile.webp';
	import favicon from '$lib/assets/favicon.svg';

	type Theme = 'light' | 'dark';
	type NavPath = '/about' | '/works' | '/resume';
	type InternalNavItem = {
		label: string;
		path: NavPath;
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

	let { children } = $props();
	let theme = $state<Theme>('dark');
	let mobileMenuOpen = $state(false);
	const currentYear = new Date().getFullYear();
	const navItems: NavItem[] = [
		{ label: 'ABOUT', path: '/about' },
		{ label: 'WORKS', path: '/works' },
		{ label: 'RESUME', path: '/resume' },
		{
			label: 'GITHUB',
			href: 'https://github.com/darkstars31',
			external: true,
			target: '_blank',
			rel: 'noreferrer'
		},
		{
			label: 'LINKEDIN',
			href: 'https://www.linkedin.com/in/anthony-santi/',
			external: true,
			target: '_blank',
			rel: 'noreferrer'
		}
	];

	const applyTheme = (nextTheme: Theme) => {
		theme = nextTheme;
		document.documentElement.dataset.theme = nextTheme;
	};

	const getPreferredTheme = (): Theme => {
		if (typeof window === 'undefined' || typeof window.matchMedia !== 'function') {
			return 'dark';
		}

		return window.matchMedia('(prefers-color-scheme: light)').matches ? 'light' : 'dark';
	};

	const toggleTheme = () => {
		const nextTheme: Theme = theme === 'dark' ? 'light' : 'dark';
		applyTheme(nextTheme);
		localStorage.setItem('theme', nextTheme);
	};

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

	onMount(() => {
		const savedTheme = localStorage.getItem('theme');
		if (savedTheme === 'light' || savedTheme === 'dark') {
			applyTheme(savedTheme);
			return;
		}

		applyTheme(getPreferredTheme());
	});
</script>

<svelte:head>
	<link rel="icon" href={favicon} />
	<script async src="https://www.googletagmanager.com/gtag/js?id=G-JBZJTH1XP2"></script>
	<script>
		window.dataLayer = window.dataLayer || [];
		function gtag() {
			dataLayer.push(arguments);
		}
		gtag('js', new Date());
		gtag('config', 'G-JBZJTH1XP2');
	</script>
	<script>
		(() => {
			const savedTheme = localStorage.getItem('theme');
			const hasMatchMedia = typeof window.matchMedia === 'function';
			const preferredTheme = hasMatchMedia && window.matchMedia('(prefers-color-scheme: light)').matches
				? 'light'
				: 'dark';
			const theme = savedTheme === 'light' || savedTheme === 'dark' ? savedTheme : preferredTheme;
			document.documentElement.dataset.theme = theme;
		})();
	</script>
</svelte:head>

<div class="flex min-h-screen flex-col">
	<header class="sticky top-0 z-10 flex flex-wrap items-center justify-between gap-4 px-6 py-4 backdrop-blur-[6px]">
		<a
			class="inline-flex items-center gap-[0.55rem] font-['IBM_Plex_Mono',monospace] text-[0.9rem] font-semibold uppercase tracking-[0.08em] text-(--text) no-underline"
			href={resolve('/')}
		>
			<img
				class="h-12 w-12 rounded-full border-0 bg-transparent object-cover"
				src={faceProfile}
				alt="Anthony Santi profile"
			/>
			<span>Anthony Santi</span>
		</a>
		<div class="ml-auto inline-flex items-center gap-2 md:hidden!">
			<button
				class="inline-flex h-[2.2rem] w-[2.2rem] cursor-pointer items-center justify-center rounded-full border border-(--line) bg-(--card) p-0 text-(--text) transition-colors hover:border-(--highlight)"
				type="button"
				onclick={toggleTheme}
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
				{#each navItems as item, index (item.label)}
					{#if item.external}
						<button
							type="button"
							class="nav-link-button"
							onclick={() => openExternalLink(item.href)}
							style={`--nav-enter-delay: ${index * 300}ms`}
						>
							{item.label}
						</button>
					{:else}
						<a href={resolve(item.path)} style={`--nav-enter-delay: ${index * 300}ms`}>
							{item.label}
						</a>
					{/if}
				{/each}
			</nav>
			<button
				class="inline-flex h-[2.2rem] w-[2.2rem] cursor-pointer items-center justify-center rounded-full border border-(--line) bg-(--card) p-0 text-(--text) transition-colors hover:border-(--highlight)"
				type="button"
				onclick={toggleTheme}
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
					{#each navItems as item (item.label)}
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
	</header>

	<main class="mx-auto w-[min(1000px,calc(100%-3rem))] flex-1 py-12 pb-16 max-[700px]:w-[min(1000px,calc(100%-2rem))] max-[700px]:pt-[1.8rem]">
		{@render children()}
	</main>

	<footer class="px-6 pb-[1.8rem] pt-[1.2rem] text-center text-[0.92rem] text-(--muted)">
		<p>Enhancing lives every day through thoughtful software.</p>
		<p class="mt-[0.4rem] flex items-center justify-center gap-[0.55rem] text-[0.82rem]">
			<span>&copy; {currentYear} Anthony M Santi.</span>
			<a class="font-semibold text-(--text)" href={resolve('/privacy-policy')}>Privacy Policy</a>
		</p>
	</footer>
</div>
