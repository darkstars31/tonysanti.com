<script lang="ts">
	import { resolve } from '$app/paths';

	const resumeDocId = '1aFArVVI2q56f_wfbotfhuxWqTtM0LjeOmTIXRTL4msM';
	const resumeDriveUrl = `https://docs.google.com/document/d/${resumeDocId}/edit?usp=sharing`;
	const resumePdfUrl = `https://docs.google.com/document/d/${resumeDocId}/export?format=pdf`;
</script>

<section class="content-page resume-page">
	<div class="mb-3 flex items-center justify-between gap-3">
		<h1 class="m-0">Resume</h1>
		<div class="flex items-center gap-2">
			<a
				class="inline-flex h-9 w-9 items-center justify-center rounded-full border border-(--line) bg-(--card) text-(--text) transition-colors hover:border-(--highlight)"
				href={resumeDriveUrl}
				target="_blank"
				rel="noreferrer"
				title="Open Resume in Google Drive"
				aria-label="Open Resume in Google Drive"
			>
				<svg
					viewBox="0 0 87.3 78"
					aria-hidden="true"
					class="h-4 w-4"
					fill="none"
					xmlns="http://www.w3.org/2000/svg"
				>
					<path d="M6.6 65.4 0 54 18.7 21.6h13.2L6.6 65.4Z" fill="#0F9D58" />
					<path d="M80.7 78H43.3l-6.6-11.4h44.1L87.3 78h-6.6Z" fill="#4285F4" />
					<path d="m49.9 0 37.4 64.8H74.1L36.7 0h13.2Z" fill="#F4B400" />
				</svg>
			</a>
			<a
				class="inline-flex h-9 w-9 items-center justify-center rounded-full border border-(--line) bg-(--card) text-(--text) transition-colors hover:border-(--highlight)"
				href={resumePdfUrl}
				target="_blank"
				rel="noreferrer"
				download="Anthony-Santi-Resume.pdf"
				title="Download Resume PDF"
				aria-label="Download Resume PDF"
			>
				<svg viewBox="0 0 24 24" fill="none" aria-hidden="true" class="h-4 w-4" xmlns="http://www.w3.org/2000/svg">
					<path d="M12 3V14" stroke="currentColor" stroke-width="2" stroke-linecap="round"/>
					<path d="M8.5 10.5L12 14L15.5 10.5" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
					<path d="M4 17.5H20" stroke="currentColor" stroke-width="2" stroke-linecap="round"/>
				</svg>
			</a>
		</div>
	</div>

	<div class="resume-header">
		<p class="resume-name">Anthony M Santi</p>
		<p class="resume-contact">
			<a href="mailto:TonyMSanti@gmail.com">TonyMSanti@gmail.com</a>
			•
			<a href="https://github.com/darkstars31" target="_blank" rel="noreferrer">GitHub</a>
			•
			<a href="https://www.linkedin.com/in/anthony-santi/" target="_blank" rel="noreferrer">LinkedIn</a>
		</p>
		<p class="resume-summary">
			Senior Full-Stack Software Engineer and Team Lead with 10+ years building and scaling
			customer-facing products across fintech, SaaS, and mortgage domains. Strengths include
			React/TypeScript platforms, Node/NestJS and Python services, cloud architecture on AWS/Azure,
			and mentoring high-performing distributed teams. Known for shipping measurable outcomes,
			including $12M annual savings and 50% CI/CD runtime reductions.
		</p>
	</div>

	<h2 class="resume-section-title">Professional Experience</h2>

	<article class="project-card resume-entry">
		<h2>NBH Bank (2Unifi)</h2>
		<p class="resume-meta">
			<strong>Senior Full-Stack Software Engineer - Team Lead (Remote)</strong> • October 2024 - Present
		</p>
		<ul>
			<li>
				Improved team delivery consistency by leading distributed onshore and offshore engineers
				through async planning, sprint coordination, and clear execution standards
			</li>
			<li>
				Stabilized a transitioning engineering organization by defining and rolling out core
				engineering norms, workflows, and collaboration practices
			</li>
			<li>
				Reduced rework and requirement churn by leading cross-functional requirements discovery and
				translating business logic into clear technical implementation plans
			</li>
			<li>
				Accelerated growth of junior and mid-level engineers through structured mentorship, pairing,
				and actionable code-review feedback
			</li>
			<li>
				Expanded core banking platform capabilities by extending NestJS microservices with TypeORM,
				Liquibase migrations, Azure MSSQL, and Cosmos DB
			</li>
			<li>
				Delivered production features for React web and React Native SMB banking applications using
				Next.js routing, Redux/RTK, and MUI
			</li>
			<li>
				Increased deployment throughput by optimizing Azure DevOps CI/CD pipelines and cutting build
				run times by 50%
			</li>
		</ul>
	</article>

	<article class="project-card resume-entry">
		<h2>EquipmentShare</h2>
		<p class="resume-meta"><strong>Software Engineer 3 (Remote/Hybrid)</strong> • March 2020 - September 2024</p>
		<ul>
			<li>
				Improved roadmap predictability by partnering with product, design, and engineering to scope
				and estimate quarterly initiatives
			</li>
			<li>
				Delivered a payment processor integration that reduced transaction costs and generated
				$12M/year in savings
			</li>
			<li>
				Built and maintained customer-facing SaaS capabilities using React, TypeScript, Elastic UI,
				and Python FastAPI services
			</li>
			<li>
				Enabled data-driven field decisions by surfacing historical and real-time telematics across
				300,000+ assets
			</li>
			<li>
				Led a team delivering cloud communication workflows using AWS Lambda, TypeScript, and Twilio
				for rental alerts and notifications
			</li>
			<li>
				Improved frontend developer velocity by driving React Query adoption and reducing Redux
				boilerplate
			</li>
			<li>
				Reduced outages and improved user trust by implementing Datadog observability, Mezmo
				alerting, and Heap Analytics instrumentation
			</li>
			<li>
				Raised team effectiveness by mentoring engineers through code reviews, pair programming, and
				facilitated retrospectives
			</li>
		</ul>
	</article>

	<article class="project-card resume-entry">
		<h2>Veterans United Home Loans</h2>
		<p class="resume-meta"><strong>Application Developer</strong> • July 2014 - March 2020</p>
		<ul>
			<li>
				Helped scale full-stack platforms that supported growth to the #1 VA mortgage lender in the
				United States
			</li>
			<li>Delivered software under SDLC processes using Agile and XP delivery practices</li>
			<li>
				Built and launched the company’s first B2C mobile-focused web application using C#,
				JavaScript, and PHP
			</li>
			<li>
				Improved quality and cross-team alignment by collaborating daily with QA, architects, and
				stakeholders in a pair programming culture
			</li>
			<li>
				Increased release confidence by adopting TDD practices and configuring CI/CD project pipelines
			</li>
			<li>
				Strengthened hiring outcomes by leading candidate screening and pair-programming interview
				loops for software services
			</li>
			<li>
				Improved team engagement by helping form and represent a culture committee focused on
				community-building initiatives
			</li>
		</ul>
	</article>

	<h2 class="resume-section-title">Education</h2>
	<article class="project-card resume-entry">
		<h2>University of Missouri</h2>
		<p class="resume-meta"><strong>Bachelor of Science in Computer Science</strong> • August 2010 - May 2014</p>
	</article>

	<h2 class="resume-section-title">Selected Projects</h2>
	<article class="project-card resume-entry">
		<h2>AnalytiKill</h2>
		<p class="resume-meta">
			Founded and built a community esports analytics platform supporting 22 franchises and 80+ teams
		</p>
		<ul>
			<li>
				Developed React and TypeScript frontend with React Query and eCharts for advanced data
				visualization and weekly insights
			</li>
			<li>
				Implemented Discord SSO authentication and backend services with Express, Prisma, and
				PostgreSQL
			</li>
			<li>
				Improved platform performance with in-memory caching and automated operations via PM2 and cron
			</li>
		</ul>
	</article>

	<article class="project-card resume-entry">
		<h2>WebScoreboard and Gratitude Taco Bot</h2>
		<p class="resume-meta">Personal automation and engagement tooling</p>
		<ul>
			<li>
				Built a real-time Socket.IO scoreboard remotely controlled from mobile devices for group game
				experiences
			</li>
			<li>
				Created Slack and Discord gratitude bot variants to increase social recognition in remote
				teams
			</li>
		</ul>
	</article>

	<h2 class="resume-section-title">Skills and Tools</h2>
	<div class="resume-skill-groups">
		<p class="resume-skill-line"><strong>Languages:</strong> TypeScript, JavaScript, Python, C#</p>
		<p class="resume-skill-line">
			<strong>Frontend:</strong> React, Next.js, React Native, MUI, CSS, React Query, React Testing Library,
			Jest, Enzyme
		</p>
		<p class="resume-skill-line">
			<strong>Backend and APIs:</strong> Node.js, NestJS, FastAPI, Express, GraphQL, REST APIs, JWT,
			Authentication and Authorization, RabbitMQ, SQS
		</p>
		<p class="resume-skill-line">
			<strong>Cloud and DevOps:</strong> AWS, Azure, AWS CDK, CI/CD, Azure DevOps, Jenkins, LaunchDarkly,
			Git, GitLab
		</p>
		<p class="resume-skill-line">
			<strong>Data and Observability:</strong> PostgreSQL, MSSQL, MySQL, Cosmos DB, Prisma, TypeORM,
			Liquibase, Datadog, Splunk, Heap, Mezmo
		</p>
		<p class="resume-skill-line">
			<strong>Methods:</strong> Agile, XP, TDD, SOLID, DRY, software design patterns, pair programming,
			mentorship
		</p>
	</div>

	<div class="link-grid resume-links">
		<a class="tile-link" href={resolve('/projects')}>
			<strong>Passion Projects</strong>
			<span>See the project portfolio and technical experiments.</span>
		</a>
		<a class="tile-link" href="mailto:TonyMSanti@gmail.com">
			<strong>Email</strong>
			<span>TonyMSanti@gmail.com</span>
		</a>
		<a class="tile-link" href="https://www.linkedin.com/in/anthony-santi/" target="_blank" rel="noreferrer">
			<strong>LinkedIn Profile</strong>
			<span>linkedin.com/in/anthony-santi</span>
		</a>
		<a class="tile-link" href="https://github.com/darkstars31" target="_blank" rel="noreferrer">
			<strong>GitHub Profile</strong>
			<span>github.com/darkstars31</span>
		</a>
	</div>
</section>
