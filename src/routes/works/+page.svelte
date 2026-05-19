<script lang="ts">
	import { onDestroy, onMount } from 'svelte';
	import proxmoxImage from '$lib/assets/proxmox_logo.png';

	const t3FleetImage = new URL('../../lib/assets/t3fleetmanagement.avif', import.meta.url).href;
	const myVUImage = new URL('../../lib/assets/myvu-phone-overview.png', import.meta.url).href;
	const analytikillImage = new URL('../../lib/assets/analytikill.PNG', import.meta.url).href;
	const scoreboardImage = new URL('../../lib/assets/scoreboard.PNG', import.meta.url).href;
	const weddingImage = new URL('../../lib/assets/wedding.PNG', import.meta.url).href;

	type Project = {
		title: string;
		description: string;
		stack: string;
		link?: string;
		image?: string;
		imageAlt?: string;
	};

	const projects: Project[] = [
		{
			title: 'T3: Fleet Management',
			description:
				'',
			stack: 'React • TypeScript • React Query • Google Maps • Python • PostgreSQL • Gitlab CI/CD',
			link: 'https://t3.tech/solutions/fleet-management',
			image: t3FleetImage,
			imageAlt: 'T3: Fleet Management platform dashboard screenshot'
		},
		{
			title: 'MyVeteransUnited',
			description:
				'',
			stack: 'Angular • TypeScript • C# • PHP • MSSQL • TeamFoundation Server',
			link: 'https://my.veteransunited.com/login',
			image: myVUImage,
			imageAlt: 'MyVeteransUnited Loan platform dashboard screenshot'
		},
		{
			title: '2Unifi',
			description:
				'',
			stack: 'React • React Native • TypeScript • NestJS • TypeORM • MSSQL/CosmosDB • Bitbucket • Azure DevOps CI/CD',
			link: 'https://my.veteransunited.com/login',
			image: myVUImage,
			imageAlt: 'MyVeteransUnited Loan platform dashboard screenshot'
		},
		{
			title: 'AnalytiKill',
			description:
				'Founded and built a community analytics platform supporting a free draft esports league with 750+ active members, 22 franchises and 80+ teams.',
			stack: 'React • TypeScript • React Query • eCharts • Express • Prisma • PostgreSQL • GitHub Actions',
			link: 'https://analytikill.com',
			image: analytikillImage,
			imageAlt: 'AnalytiKill platform dashboard screenshot'
		},
		{
			title: 'WebScoreboard',
			description:
				'Built a real-time scoreboard app controllable from mobile devices, inspired by party game experiences.',
			stack: 'Node.js • Socket.IO • JavaScript • WebSockets',
			link: 'https://tonysanti.com/scoreboard',
			image: scoreboardImage,
			imageAlt: 'WebScoreboard application screenshot'
		},
		{
			title: 'Wedding.TonySanti.com',
			description:
				'Designed and shipped a wedding website with a custom RSVP flow and persistent data storage for event coordination.',
			stack: 'Angular • Node/Express • Firebase',
			link: 'https://wedding.tonysanti.com/',
			image: weddingImage,
			imageAlt: 'Wedding website landing page screenshot'
		},
		{
			title: 'Homelab',
			description:
				'Maintained a two-cluster Proxmox setup with Linux VMs, Docker workloads, nginx reverse proxying, and production Postgres for personal applications.',
			stack: 'Proxmox • Docker • Linux • nginx • DigitalOcean • PostgreSQL',
			image: proxmoxImage,
			imageAlt: 'Proxmox logo for homelab infrastructure'
		},
		{
			title: 'Games and Digital Art Experiments',
			description:
				'Work-in-progress interactive projects exploring mechanics, visuals, and tooling with Godot.',
			stack: 'Godot • GDScript • C#'
		}
	];

	const projectRainbowHues = [0, 32, 58, 120, 220, 275];
	let observer: IntersectionObserver | null = null;


	const setProjectHue = (index: number) => {
		if (index === 0) {
			// Remove tint for the first project (default background)
			delete document.documentElement.dataset.projectRainbow;
			document.documentElement.style.removeProperty('--project-rainbow-hue');
			return;
		}
		document.documentElement.dataset.projectRainbow = 'true';
		document.documentElement.style.setProperty(
			'--project-rainbow-hue',
			`${projectRainbowHues[index % projectRainbowHues.length]}deg`
		);
	};

	const openProject = (url: string) => {
		if (typeof window !== 'undefined') {
			window.open(url, '_blank', 'noreferrer');
		}
	};

	onMount(() => {
		document.documentElement.dataset.projectSnap = 'true';
		setProjectHue(0);

		const slides = Array.from(document.querySelectorAll<HTMLElement>('.project-slide'));
		if (!slides.length || typeof IntersectionObserver === 'undefined') {
			return;
		}

		observer = new IntersectionObserver(
			(entries) => {
				const visible = entries
					.filter((entry) => entry.isIntersecting)
					.sort((a, b) => b.intersectionRatio - a.intersectionRatio)[0];

				if (!visible) {
					return;
				}

				const index = slides.indexOf(visible.target as HTMLElement);
				if (index >= 0) {
					setProjectHue(index);
				}
			},
			{ threshold: [0.5, 0.75, 0.9] }
		);

		for (const slide of slides) {
			observer.observe(slide);
		}
	});

	onDestroy(() => {
		observer?.disconnect();
		delete document.documentElement.dataset.projectSnap;
		delete document.documentElement.dataset.projectRainbow;
		document.documentElement.style.removeProperty('--project-rainbow-hue');
	});
</script>

<section class="content-page projects-page">
	<div class="vertical-carousel" aria-label="Projects vertical carousel">
		{#each projects as project, index (project.title)}
			<article class="project-slide" aria-label={`Project ${index + 1}: ${project.title}`}>
				<div class="slide-copy">
					<p class="slide-index">{String(index + 1).padStart(2, '0')}</p>
					<h2>{project.title}</h2>
					<p>{project.description}</p>
					<p class="stack">{project.stack}</p>
					{#if project.link}
						<button type="button" class="button button-ghost" onclick={() => openProject(project.link!)}>
							Open Project
						</button>
					{/if}
				</div>

				<div class="slide-media" aria-hidden={project.image ? undefined : 'true'}>
					{#if project.image}
						<img src={project.image} alt={project.imageAlt ?? `${project.title} image`} />
					{:else}
						<div class="media-placeholder">
							<p class="placeholder-kicker">NO IMAGE</p>
							<p>Visual coming soon</p>
						</div>
					{/if}
				</div>
			</article>
		{/each}
	</div>

	<p class="project-note">
		More code samples and active repositories are available on
		<a href="https://github.com/darkstars31" target="_blank" rel="noreferrer">GitHub</a>.
	</p>
</section>

<style>
	.projects-page {
		display: grid;
		gap: 1rem;
		--top-nav-offset: clamp(5.8rem, 9vw, 7.2rem);
	}

	.projects-header p {
		max-width: 56ch;
	}

	.projects-header {
		scroll-snap-align: start;
		scroll-margin-top: var(--top-nav-offset);
	}

	.vertical-carousel {
		display: grid;
		gap: 3.5rem;
		padding-bottom: 2rem;
	}

	.project-slide {
		scroll-snap-align: start;
		scroll-snap-stop: always;
		scroll-margin-top: var(--top-nav-offset);
		min-height: clamp(520px, calc(100vh - var(--top-nav-offset) - 1.5rem), 820px);
		display: grid;
		grid-template-columns: minmax(0, 1fr) minmax(0, 1fr);
		gap: 0.85rem;
		padding: 0.9rem;
		border: none;
		border-radius: 0.8rem;
		background: transparent;
	}

	.slide-copy {
		display: grid;
		align-content: start;
		gap: 0.6rem;
		padding: 0.2rem;
	}

	.slide-index {
		font-family: 'IBM Plex Mono', monospace;
		font-size: 0.73rem;
		letter-spacing: 0.05em;
		text-transform: uppercase;
		color: var(--muted);
		margin: 0;
	}

	.slide-copy h2 {
		margin: 0;
		font-size: clamp(1.4rem, 3vw, 2rem);
	}

	.slide-copy > p {
		margin: 0;
	}

	.slide-copy :global(.button) {
		width: fit-content;
		margin-top: 0.2rem;
	}

	.slide-media {
		min-height: 100%;
		display: flex;
		align-items: center;
	}

	.slide-media img,
	.media-placeholder {
		width: 100%;
		height: 100%;
		min-height: 240px;
		border-radius: 0.7rem;
	}

	.slide-media img {
		object-fit: scale-down;
		max-height: clamp(760px, 45vh, 420px);
	}

	.media-placeholder {
		display: grid;
		align-content: center;
		justify-items: center;
		gap: 0.3rem;
		padding: 0.9rem;
		background: color-mix(in srgb, var(--card) 88%, var(--bg-accent));
		border: none;
	}

	.placeholder-kicker {
		margin: 0;
		font-family: 'IBM Plex Mono', monospace;
		font-size: 0.72rem;
		text-transform: uppercase;
		letter-spacing: 0.08em;
		color: var(--muted);
	}

	.media-placeholder p {
		margin: 0;
		color: var(--muted);
		font-size: 0.85rem;
	}

	@media (max-width: 820px) {
		.vertical-carousel {
			gap: 1.5rem;
		}

		.project-slide {
			min-height: auto;
			grid-template-columns: 1fr;
		}
	}
</style>
