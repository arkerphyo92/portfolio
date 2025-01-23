<script lang="ts">
	import ProgressBar from './ProgressBar.svelte';

	const skills = [
		{ skill: 'Python (Django, Litestar, etc.)', level: 95 },
		{ skill: 'TailwindCSS / Bootstrap (HTML/CSS)', level: 90 },
		{ skill: 'Database (PostgreSQL, MYSQL, MSSQL, SQLITE)', level: 80 },
		{ skill: 'JavaScript (ReactJs, SvelteKit, TypeScript)', level: 80 },
		{ skill: 'WordPress/CMS', level: 90 },
		{ skill: 'Docker / GitHub', level: 75 }
	];
</script>

<section id="skills" class="skills section light-background">
	<div class="section-title">
		<h2>Skills</h2>
		<p>Necessitatibus eius consequatur ex aliquid fuga eum quidem sint consectetur velit</p>
	</div>

	<div class="skills-content">
		<div class="row">
			{#each skills as { skill, level }}
				<ProgressBar {skill} {level} />
			{/each}
		</div>
	</div>
</section>

<style>
	.section {
		padding: 2rem;
		background-color: #fff;
	}

	.section-title {
		text-align: center;
		margin-bottom: 2rem;
	}

	.row {
		display: flex;
		flex-wrap: wrap;
		gap: 1.5rem;
	}
</style>
