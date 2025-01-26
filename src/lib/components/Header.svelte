<script lang="ts">
	import { page } from '$app/state';
	import { onMount } from 'svelte';

	// Reactive variable to track header visibility
	let headerVisible: boolean = false;

	/**
	 * Toggles the visibility of the header
	 */
	const toggleHeader = (): void => {
		headerVisible = !headerVisible;
	};

	/**
	 * Hides the mobile navigation menu when a hash link is clicked
	 */
	const hideNavOnHashLinkClick = (): void => {
		if (headerVisible) {
			toggleHeader();
		}
	};

	/**
	 * Adds event listeners for dropdown menus
	 */
	onMount(() => {
		const dropdownToggles: NodeListOf<HTMLElement> = document.querySelectorAll(
			'.navmenu .toggle-dropdown'
		);

		dropdownToggles.forEach((toggle) => {
			toggle.addEventListener('click', (e: MouseEvent) => {
				e.preventDefault();
				const parent = toggle.parentNode as HTMLElement | null;
				const nextSibling = toggle.nextElementSibling as HTMLElement | null;

				if (parent) parent.classList.toggle('active');
				if (nextSibling) nextSibling.classList.toggle('dropdown-active');

				e.stopImmediatePropagation();
			});
		});
	});
</script>

<header
	id="header"
	class="header dark-background d-flex flex-column {headerVisible ? 'header-show' : ''}"
>
	<!-- Toggle Button -->
	<button
		aria-label="MenuToggle"
		class="header-toggle d-xl-none bi {headerVisible ? 'bi-x' : 'bi-list'} btn"
		on:click={toggleHeader}
	></button>

	<!-- Profile Image -->
	<div class="profile-img">
		<img src="/lib/img/arkarphyo-profile.jpg" alt="Profile" class="img-fluid rounded-circle" />
	</div>

	<!-- Logo -->
	<a href="/" class="logo d-flex align-items-center justify-content-center">
		<h1 class="sitename">Arkar Phyo</h1>
	</a>

	<!-- Social Links -->
	<div class="social-links text-center">
		<a href="https://github.com/arkerphyo92" aria-label="github" class="github">
			<i class="bi bi-github"></i>
		</a>
		<a href="mailto:arkerphyo92@gmail.com" aria-label="email" class="email">
			<i class="bi bi-envelope"></i>
		</a>
		<a
			href="https://www.linkedin.com/in/arker-phyo-351360211/"
			aria-label="linkedin"
			class="linkedin"
		>
			<i class="bi bi-linkedin"></i>
		</a>
	</div>

	<!-- Navigation Menu -->
	<nav id="navmenu" class="navmenu">
		<ul>
			<li>
				<a
					href="#hero"
					class={page.url.hash === '#hero' ? 'active' : ''}
					on:click={hideNavOnHashLinkClick}
				>
					<i class="bi bi-house navicon"></i>Home
				</a>
			</li>
			<li>
				<a
					href="#about"
					class={page.url.hash === '#about' ? 'active' : ''}
					on:click={hideNavOnHashLinkClick}
				>
					<i class="bi bi-person navicon"></i> About
				</a>
			</li>
			<li>
				<a
					href="#resume"
					class={page.url.hash === '#resume' ? 'active' : ''}
					on:click={hideNavOnHashLinkClick}
				>
					<i class="bi bi-file-earmark-text navicon"></i> Resume
				</a>
			</li>
			<li>
				<a
					href="#portfolio"
					class={page.url.hash === '#portfolio' ? 'active' : ''}
					on:click={hideNavOnHashLinkClick}
				>
					<i class="bi bi-images navicon"></i> Portfolio
				</a>
			</li>
			<li>
				<a
					href="#contact"
					class={page.url.hash === '#contact' ? 'active' : ''}
					on:click={hideNavOnHashLinkClick}
				>
					<i class="bi bi-envelope navicon"></i> Contact
				</a>
			</li>
		</ul>
	</nav>
</header>

<style>
</style>
