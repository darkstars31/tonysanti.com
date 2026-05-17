<script lang="ts">
	import { onMount } from 'svelte';
	import { resolve } from '$app/paths';
	import { Moon, Sun } from '@lucide/svelte';
	import './layout.css';
	import favicon from '$lib/assets/favicon.svg';

	type Theme = 'light' | 'dark';

	let { children } = $props();
	let theme = $state<Theme>('dark');
	const currentYear = new Date().getFullYear();

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

<div class="site-shell">
	<header class="site-header">
		<a class="brand" href={resolve('/')}>Anthony Santi</a>
		<div class="header-actions">
			<nav aria-label="Primary" class="site-nav">
				<a href={resolve('/about')}>About</a>
				<a href={resolve('/projects')}>Projects</a>
				<a href={resolve('/case-studies')}>Case Studies</a>
				<a href={resolve('/resume')}>Resume</a>
				<a href="https://github.com/darkstars31" target="_blank" rel="noreferrer">GitHub</a>
				<a href="https://www.linkedin.com/in/anthony-santi/" target="_blank" rel="noreferrer">LinkedIn</a>
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
	</header>

	<main class="page-content">
		{@render children()}
	</main>

	<footer class="site-footer">
		<p>Enhancing lives every day through thoughtful software.</p>
		<p class="footer-legal">
			<span>&copy; {currentYear} Anthony Michael Santi.</span>
			<a href={resolve('/privacy-policy')}>Privacy Policy</a>
		</p>
	</footer>
</div>
