<script lang="ts">
	import { onDestroy, onMount } from 'svelte';
	import proxmoxImage from '$lib/assets/proxmox_logo.png?url';
	import t3FleetImage from '$lib/assets/t3fleetmanagement.avif?url';
	import myVUImage from '$lib/assets/myvu-phone-overview.png?url';
	import twoUnifiImage from '$lib/assets/2unifi.PNG?url';
	import analytikillImage from '$lib/assets/analytikill.PNG?url';
	import scoreboardImage from '$lib/assets/scoreboard.PNG?url';
	import weddingImage from '$lib/assets/wedding.PNG?url';
	import experimentsImage from '$lib/assets/games.png?url';

	type Project = {
		title: string;
		description: string;
		stack: string;
		cta?: {
			label: string;
			url: string;
		}[];
		image?: string;
		imageStyle?: string;
		imageAlt?: string;
	};

	const projects: Project[] = [
		{
			title: 'T3: Fleet Management',
			description:
				'Fleet management platform providing real-time tracking, reporting, and analytics for vehicle fleets, leveraging React frontend and Python backend services.',
			stack: 'React • TypeScript • React Query • Google Maps • Python • PostgreSQL • Gitlab CI/CD',
			cta: [
				{
					label: 'Learn More',
					url: 'https://t3.tech/solutions/fleet-management'
				}
			],
			image: t3FleetImage,
			imageStyle: '',
			imageAlt: 'T3: Fleet Management platform dashboard screenshot'
		},
		{
			title: 'MyVeteransUnited',
			description:
				'All-in-one Loan management platform for Veterans United Home Loans customers, featuring Angular frontend and C#/PHP microservices backend.',
			stack: 'AngularJS • TypeScript • C# • EntityFramework • PHP • MSSQL • TeamFoundation Server',
			cta: [
				{
					label: 'Want to see it?',
					url: 'https://my.veteransunited.com/login'
				}
			],
			image: myVUImage,
			imageAlt: 'MyVeteransUnited Loan platform dashboard screenshot'
		},
		{
			title: '2Unifi',
			description:
				'Multi-faceted banking platform designed to streamline financial operations for SMB Business clients, featuring a React-based client portal and React Native mobile app with NestJS microservices backend.',
			stack: 'React • React Native • TypeScript • NestJS • Microservices • TypeORM • MSSQL/CosmosDB • Bitbucket • Azure DevOps CI/CD',
			cta: [
				{
					label: 'Check It Out',
					url: 'https://www.2ufi.com/'
				}
			],
			image: twoUnifiImage,
			imageAlt: '2Unifi platform dashboard screenshot'
		},
		{
			title: 'AnalytiKill',
			description:
				'Founded and built a community analytics platform supporting a free draft esports league with 750+ active members, 22 franchises and 80+ teams.',
			stack: 'React • TypeScript • React Query • eCharts • Express • Prisma • PostgreSQL • GitHub Actions',
			cta: [
				{
					label: 'Explore',
					url: 'https://analytikill.com'
				}
			],
			image: analytikillImage,
			imageAlt: 'AnalytiKill platform dashboard screenshot'
		},
		{
			title: 'WebScoreboard',
			description:
				'Built a real-time scoreboard app controllable from mobile devices, inspired by party game experiences.',
			stack: 'Node.js • Socket.IO • JavaScript • WebSockets',
			cta: [
				{
					label: 'Try It Out',
					url: 'https://tonysanti.com/scoreboard'
				}
			],
			image: scoreboardImage,
			imageAlt: 'WebScoreboard application screenshot'
		},
		{
			title: 'Wedding.TonySanti.com',
			description:
				'Designed and shipped a wedding website with a custom RSVP flow and persistent data storage for event coordination.',
			stack: 'Angular • Node/Express • Firebase',
			cta: [
				{
					label: 'Learn More',
					url: 'https://wedding.tonysanti.com/'
				}
			],
			image: weddingImage,
			imageAlt: 'Wedding website landing page screenshot'
		},
		{
			title: 'Homelab',
			description:
				'Maintain a two-cluster Proxmox setup with Linux VMs, Docker workloads, nginx reverse proxying, and production Postgres for personal applications.',
			stack: 'Proxmox • Docker • Linux • nginx • DigitalOcean • PM2 Process Manager • PostgreSQL',
			image: proxmoxImage,
			imageAlt: 'Proxmox logo for homelab infrastructure'
		},
		{
			title: 'Games and Digital Art Experiments',
			description:
				'Work-in-progress interactive projects exploring mechanics, visuals, and tooling with Godot.',
			cta: [
				{
					label: 'Endurence Arena (Unfinished Phaser.io prototype)',
					url: 'https://tonysanti.com/games/endurancearena/'
				},
				{
					label: 'Rupee Clicker (Mini-Game)',
					url: 'https://tonysanti.com/games/rupeeclicker/'
				}
			],
			stack: 'Godot • GDScript • Phaser.io • C#',
			image: experimentsImage,
			imageAlt: 'Collage of experimental game projects'
		}
	];

	const projectRainbowHues = [0, 32, 58, 120, 220, 275];
	let observer: IntersectionObserver | null = null;
	const canUseDOM = typeof document !== 'undefined';


	const setProjectHue = (index: number) => {
		if (!canUseDOM) {
			return;
		}

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
		if (!canUseDOM) {
			return;
		}

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
					<p class="slide-index">{String(index + 1).padStart(2, '0')}/{String(projects.length).padStart(2, '0')}</p>
					<h2>{project.title}</h2>
					<p>{project.description}</p>
					<p class="stack">{project.stack}</p>
					{#if project.cta}
						{#each project.cta as cta (cta.url)}
							<button type="button" class="button button-ghost" onclick={() => openProject(cta.url)}>
								{cta.label}
							</button>
						{/each}
					{/if}
				</div>

				<div class={`slide-media ${project.imageStyle ?? ''}`} aria-hidden={project.image ? undefined : 'true'}>
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
		object-fit: cover;
		overflow: visible;
		max-height: calc(60% - 0.4rem);
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
