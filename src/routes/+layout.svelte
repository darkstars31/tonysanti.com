<script lang="ts">
	import { onMount } from 'svelte';
	import { resolve } from '$app/paths';
	import Menu from '@lucide/svelte/icons/menu';
	import Moon from '@lucide/svelte/icons/moon';
	import Sun from '@lucide/svelte/icons/sun';
	import X from '@lucide/svelte/icons/x';
	import './layout.css';
	import faceProfile from '$lib/assets/faceprofile.png';
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
		{ label: 'RÉSUMÉ', path: '/resume' },
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

<div class="site-shell">
	<header class="site-header">
		<a class="brand" href={resolve('/')}>
			<img class="brand-avatar" src={faceProfile} alt="Anthony Santi profile" />
			<span>Anthony Santi</span>
		</a>
		<div class="mobile-header-controls md:hidden!">
			<button
				class="theme-toggle"
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
				class="mobile-menu-toggle"
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
		<div class="header-actions hidden! md:flex!">
			<nav aria-label="Primary" class="site-nav">
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
				class="theme-toggle"
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
		<div class={`mobile-nav md:hidden! ${mobileMenuOpen ? 'is-open' : ''}`} id="mobile-primary-nav">
			<div class="mobile-nav-inner">
				<nav aria-label="Mobile primary" class="mobile-site-nav">
					{#each navItems as item (item.label)}
						{#if item.external}
							<button
								type="button"
								class="mobile-nav-link-button"
								onclick={() => {
									closeMobileMenu();
									openExternalLink(item.href);
								}}
							>
								{item.label}
							</button>
						{:else}
							<a href={resolve(item.path)} onclick={closeMobileMenu}>{item.label}</a>
						{/if}
					{/each}
				</nav>
			</div>
		</div>
	</header>

	<main class="page-content">
		{@render children()}
	</main>

	<footer class="site-footer">
		<p>Enhancing lives every day through thoughtful software.</p>
		<p class="footer-legal">
			<span>&copy; {currentYear} Anthony M Santi.</span>
			<a href={resolve('/privacy-policy')}>Privacy Policy</a>
		</p>
	</footer>
</div>
