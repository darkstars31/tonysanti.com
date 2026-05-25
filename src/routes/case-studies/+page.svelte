<section class="grid gap-4">
	<h1 class="mb-4 max-w-[16ch] text-[clamp(2rem,6vw,3.8rem)] leading-[1.08] max-[700px]:max-w-none">Deep Dives</h1>
	<p class="mb-[1.8rem] max-w-[62ch] text-[1rem] text-(--muted)">
		Case studies into architecture, product decisions, and measurable outcomes.
	</p>

	<article class="rounded-xl border border-(--line) bg-(--card) p-5 leading-[1.75] transition-[transform,box-shadow] duration-200 ease-in-out hover:-translate-y-1 hover:shadow-[0_4px_10px_rgba(0,0,0,0.2)]">
		<p class="m-0 font-['IBM_Plex_Mono',monospace] text-[0.73rem] uppercase tracking-wider text-(--muted)">Case Study 01</p>
		<h2 class="mt-2 mb-2 text-[1.2rem]">AnalytiKill</h2>
		<p class="max-w-[72ch] text-[0.95rem]">
			Community analytics platform for a draft-based esports league. This page is intentionally
			structured as a reusable boilerplate so additional case studies can follow the same format.
		</p>
		<p class="max-w-[72ch] text-[0.95rem]">
			<a href="https://analytikill.com" target="_blank" rel="noreferrer">Visit analytikill.com</a>
		</p>

		<h3 class="mb-[0.35rem] mt-[1.2rem] text-[1.02rem] tracking-[0.01em]">1. Problem</h3>
		<p class="max-w-[72ch] text-[0.95rem]">
			League members needed a single source of truth for performance trends, matchup insights, and
			community engagement data spread across multiple external services.
		</p>

		<h3 class="mb-[0.35rem] mt-[1.2rem] text-[1.02rem] tracking-[0.01em]">2. Constraints</h3>
		<ul class="max-w-[72ch] pl-[1.2rem]">
			<li>Unstable or rate-limited third-party APIs</li>
			<li>Weekly release cadence with limited maintainer bandwidth</li>
			<li>Need for low operational overhead and cost-conscious hosting</li>
		</ul>

		<h3 class="mb-[0.35rem] mt-[1.2rem] text-[1.02rem] tracking-[0.01em]">3. Solution</h3>
		<ul class="max-w-[72ch] pl-[1.2rem]">
			<li>React + TypeScript frontend with React Query for cache-aware data fetching</li>
			<li>Express + TypeScript API with Prisma ORM and PostgreSQL</li>
			<li>Discord SSO for streamlined authentication</li>
			<li>Background jobs and caching to reduce third-party API pressure</li>
		</ul>

		<h3 class="mb-[0.35rem] mt-[1.2rem] text-[1.02rem] tracking-[0.01em]">4. Architecture Snapshot</h3>
		<div
			class="mt-[0.4rem] rounded-[0.7rem] border border-dashed border-(--line) bg-[color-mix(in_srgb,var(--card)_90%,var(--bg-accent))] px-[0.9rem] py-[0.8rem]"
			role="img"
			aria-label="AnalytiKill architecture overview"
		>
			<p class="my-[0.1rem] font-['IBM_Plex_Mono',monospace] text-[0.84rem] text-(--muted)">
				Client (React) -> API (Express) -> PostgreSQL
			</p>
			<p class="my-[0.1rem] font-['IBM_Plex_Mono',monospace] text-[0.84rem] text-(--muted)">
				Integrations: Core, Faceit, Twitch, Discord APIs
			</p>
			<p class="my-[0.1rem] font-['IBM_Plex_Mono',monospace] text-[0.84rem] text-(--muted)">
				Ops: PM2 + cron jobs + GitHub Actions CI/CD
			</p>
		</div>

		<h3 class="mb-[0.35rem] mt-[1.2rem] text-[1.02rem] tracking-[0.01em]">5. Outcome</h3>
		<ul class="max-w-[72ch] pl-[1.2rem]">
			<li>Supported a league ecosystem of 22 franchises and 80+ teams</li>
			<li>Delivered a weekly Pick'em experience to increase community participation</li>
			<li>Improved reliability with caching and automated operational tasks</li>
		</ul>

		<h3 class="mb-[0.35rem] mt-[1.2rem] text-[1.02rem] tracking-[0.01em]">6. What I Would Improve Next</h3>
		<ul class="max-w-[72ch] pl-[1.2rem]">
			<li>Add tracing + richer observability dashboards for external dependency health</li>
			<li>Introduce queue-backed ingestion for more resilient API synchronization</li>
			<li>Expand test coverage around analytics aggregation logic</li>
		</ul>

		<h3 class="mb-[0.35rem] mt-[1.2rem] text-[1.02rem] tracking-[0.01em]">Template Notes</h3>
		<p class="max-w-[72ch] text-[0.95rem]">
			Use this same section flow for additional case studies: Problem, Constraints, Solution,
			Architecture, Outcome, Next Improvements.
		</p>
	</article>
</section>
