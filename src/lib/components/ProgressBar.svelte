<script lang="ts">
	export let skill: string;
	export let level: number;

	// Animation logic
	let progressStyle = '';

	// Animate progress bar width on mount
	import { onMount } from 'svelte';
	onMount(() => {
		setTimeout(() => {
			progressStyle = `width: ${level}%;`;
		}, 100); // Add a delay for smooth animation
	});
</script>

<div class="progress">
	<span class="skill">
		<span>{skill}</span>
		<i class="val">{level}%</i>
	</span>
	<div class="progress-bar-wrap">
		<div
			class="progress-bar"
			role="progressbar"
			style={progressStyle}
			aria-valuenow={level}
			aria-valuemin="0"
			aria-valuemax="100"
		></div>
	</div>
</div>

<style>
	.progress {
		margin-bottom: 1.5rem;
	}

	.skill {
		display: flex;
		justify-content: space-between;
		margin-bottom: 0.5rem;
		font-weight: bold;
		font-size: 1rem;
	}

	.progress-bar-wrap {
		background: #f3f3f3;
		border-radius: 20px;
		overflow: hidden;
		height: 10px;
		width: 100%;
	}

	.progress-bar {
		background: #4caf50;
		height: 100%;
		transition: width 1s ease;
	}
</style>
