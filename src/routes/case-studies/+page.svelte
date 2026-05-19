<section class="content-page case-study-page">
	<h1>Deep Dives</h1>
	<p class="lead">Case studies into architecture, product decisions, and measurable outcomes.</p>

	<article class="project-card case-study-card">
		<p class="eyebrow">Case Study 01</p>
		<h2>AnalytiKill</h2>
		<p>
			Community analytics platform for a draft-based esports league. This page is intentionally
			structured as a reusable boilerplate so additional case studies can follow the same format.
		</p>
		<p>
			<a href="https://analytikill.com" target="_blank" rel="noreferrer">Visit analytikill.com</a>
		</p>

		<h3>1. Problem</h3>
		<p>
			League members needed a single source of truth for performance trends, matchup insights, and
			community engagement data spread across multiple external services.
		</p>

		<h3>2. Constraints</h3>
		<ul>
			<li>Unstable or rate-limited third-party APIs</li>
			<li>Weekly release cadence with limited maintainer bandwidth</li>
			<li>Need for low operational overhead and cost-conscious hosting</li>
		</ul>

		<h3>3. Solution</h3>
		<ul>
			<li>React + TypeScript frontend with React Query for cache-aware data fetching</li>
			<li>Express + TypeScript API with Prisma ORM and PostgreSQL</li>
			<li>Discord SSO for streamlined authentication</li>
			<li>Background jobs and caching to reduce third-party API pressure</li>
		</ul>

		<h3>4. Architecture Snapshot</h3>
		<div class="case-study-diagram" role="img" aria-label="AnalytiKill architecture overview">
			<p>Client (React) -> API (Express) -> PostgreSQL</p>
			<p>Integrations: Core, Faceit, Twitch, Discord APIs</p>
			<p>Ops: PM2 + cron jobs + GitHub Actions CI/CD</p>
		</div>

		<h3>5. Outcome</h3>
		<ul>
			<li>Supported a league ecosystem of 22 franchises and 80+ teams</li>
			<li>Delivered a weekly Pick'em experience to increase community participation</li>
			<li>Improved reliability with caching and automated operational tasks</li>
		</ul>

		<h3>6. What I Would Improve Next</h3>
		<ul>
			<li>Add tracing + richer observability dashboards for external dependency health</li>
			<li>Introduce queue-backed ingestion for more resilient API synchronization</li>
			<li>Expand test coverage around analytics aggregation logic</li>
		</ul>

		<h3>Template Notes</h3>
		<p>
			Use this same section flow for additional case studies: Problem, Constraints, Solution,
			Architecture, Outcome, Next Improvements.
		</p>
	</article>
</section>
