<script lang="ts">
	import { resolve } from '$app/paths';
	import faceProfile from '$lib/assets/faceprofile.png';
</script>

<section class="hero">
	<div class="hero-content">
		<p class="eyebrow">Software Engineer • Developer • Tinkerer</p>
		<h1>Anthony M Santi</h1>
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

	<div class="hero-image-wrap">
		<img class="hero-image" src={faceProfile} alt="Portrait of Anthony Santi" />
	</div>
</section>
