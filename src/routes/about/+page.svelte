<script lang="ts">
	const shippedWins = [
		'Led onshore and offshore engineers as a Team Lead at NBH Bank (2Unifi)',
		'Automated Testing, taking manual account onboarding from 6 minutes down to 45 seconds',
		'Reduced Azure DevOps pipeline run times by 50% through build parallelization and caching',
		'Optimized React to handle over 350,000 heavy equipment assets',
		'Ideated and implemented a "white-glove" bulk onboarding process for clients with a large number of assets',
		'Helped deliver a payment processor integration that saved $12M per year',
		'Built and scaled products using React, React Native, NestJS, C#, FastAPI, and cloud services',
		"Transitioned 300,000 user accounts from internal auth to Okta's B2C platform with zero downtime",
		'Designed and launched the first B2C web app at Veterans United Home Loans'
	];
</script>

<section class="grid gap-4">
	<h1 class="mb-4 max-w-[16ch] text-[clamp(2rem,6vw,3.8rem)] leading-[1.08] max-[700px]:max-w-none">About Me</h1>
	<p class="max-w-[72ch] text-[0.95rem]">
		I am Anthony, a full-stack software engineer and technical leader who enjoys
		turning complex business needs into production-ready software. I have spent my career building
		reliable systems across banking, fintech, and enterprise platforms while helping teams improve
		quality, delivery speed, and collaboration.
	</p>
	<p class="max-w-[72ch] text-[0.95rem]">
		My focus is practical impact: stable architectures, automated workflows, and product features
		that improve daily life for customers and internal teams. I am especially energized by mentoring
		engineers, shaping team norms, and creating environments where people can do their best work.
	</p>

	<h2 class="mt-6 mb-2 text-[clamp(1.25rem,3.2vw,1.85rem)]">Wins I've Shipped Into The Real World</h2>
	<ul class="mt-4 grid divide-y divide-(--line) pl-0">
		{#each shippedWins as win (win)}
			<li class="list-none py-3">{win}</li>
		{/each}
	</ul>

	<!-- <h2>How I Build Software</h2>
	<ul>
		<li>Agile, Kanban, XP-inspired iteration with clear stakeholder communication</li>
		<li>Strong testing culture: TDD, maintainable test suites, and quality-first delivery</li>
		<li>Architecture guided by SOLID, DRY, and practical design patterns</li>
		<li>CI/CD and observability to improve reliability and reduce regressions</li>
		<li>People-first engineering: mentoring, pairing, and team advocacy</li>
	</ul> -->

	<h2 class="mt-6 mb-2 text-[clamp(1.25rem,3.2vw,1.85rem)]">Going Beyond Work</h2>
	<p class="max-w-[72ch] text-[0.95rem]">
		Outside of software, I spend time with family, play disc golf, work on home DIY and woodworking
		projects, and enjoy games of all kinds. I also run passion projects and experiments that help me
		stay curious and continuously improve - like this website being built in SvelteKit.
	</p>
</section>
