<script lang="ts">
	import '../app.css';
	import { page } from '$app/state';

	let currentPage = $state(page.url.pathname);

	let { children } = $props();

	const navLinks = [
		{name: "home", link: "/"},
		{name: "projects", link: "/projects"},
		{name: "about", link: "/about"},
		{name: "contact", link: "/contact"}
	];
	
</script>

<nav>
	<ul class="flex  gap-4 justify-center">
		{#each navLinks as link}
		<li class="underline hover:underline-offset-6"><a href={link.link}>{link.name}</a></li>
		{/each}
	</ul>
</nav>


{@render children()}
