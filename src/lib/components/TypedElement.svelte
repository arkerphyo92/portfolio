<script lang="ts">
	import { onMount } from 'svelte';
	import Typed from 'typed.js';

	export let strings: string[] = [];
	export let typeSpeed: number = 100;
	export let backSpeed: number = 50;
	export let backDelay: number = 2000;
	export let loop = true;

	let typedElement: HTMLSpanElement;

	onMount(() => {
		const options = {
			strings,
			typeSpeed,
			backSpeed,
			backDelay,
			loop
		};

		const typed = new Typed(typedElement, options);

		return () => {
			typed.destroy();
		};
	});
</script>

<span class="typed" bind:this={typedElement}></span>
