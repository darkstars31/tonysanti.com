<script lang="ts">
	import { onMount } from 'svelte';
	import { resolve } from '$app/paths';
	import SiteNavigation from '$lib/components/SiteNavigation.svelte';
	import './layout.css';
	import faceProfile from '$lib/assets/faceprofile.webp';
	import favicon from '$lib/assets/favicon.svg';

	type Theme = 'light' | 'dark';
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

	let { children } = $props();
	let theme = $state<Theme>('dark');
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
			class="profile-link inline-flex items-center gap-[0.55rem] font-['IBM_Plex_Mono',monospace] text-[0.9rem] font-semibold uppercase tracking-[0.08em] text-(--text) no-underline"
			href={resolve('/')}
		>
			<img
				class="profile-coin h-12 w-12 rounded-full border-0 bg-transparent object-cover"
				src={faceProfile}
				alt="Anthony Santi profile"
			/>
			<span>Anthony Santi</span>
		</a>
		<SiteNavigation items={navItems} {theme} onToggleTheme={toggleTheme} />
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
