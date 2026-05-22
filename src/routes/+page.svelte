<script lang="ts">
	import { resolve } from '$app/paths';
	import sandchair from '$lib/assets/tonysandchair.png';
</script>

<section class="grid grid-cols-[minmax(0,1.2fr)_minmax(220px,0.8fr)] items-center gap-[1.4rem] py-6 max-[700px]:grid-cols-1">
	<div class="min-w-0">
		<p class="mb-[0.8rem] font-['IBM_Plex_Mono',monospace] text-[0.8rem] uppercase tracking-[0.07em] text-(--muted)">
			Software Engineer • Developer • Tinkerer
		</p>
		<h1 class="mb-4 max-w-[16ch] text-[clamp(2rem,6vw,3.8rem)] leading-[1.08] max-[700px]:max-w-none">
			Anthony M Santi
		</h1>
		<p class="lead">
			Senior Full-Stack Software Engineer and Team Lead focused on shipping scalable products,
			mentoring teams, and delivering measurable business impact across web, mobile, and backend
			systems.
		</p>

		<div class="cta-row">
			<a class="button" href={resolve('/resume')}>View Résumé</a>
			<a class="button button-ghost" href={resolve('/about')}>Read About Me</a>
			<a class="button button-ghost" href={resolve('/projects')}>View Projects</a>
			<a class="button button-ghost" href="https://github.com/darkstars31" target="_blank" rel="noreferrer">
				GitHub
			</a>
		</div>
	</div>

	<div class="flex justify-end max-[700px]:justify-start">
		<img
			class="h-auto w-[min(100%,640px)] max-[700px]:w-[min(100%,280px)] max-[700px]:object-cover"
			src={sandchair}
			alt="Portrait of Anthony Santi"
		/>
	</div>
</section>
