<script lang="ts">
	import '../app.css';

	let { children } = $props();

	const navLinks = [
		{name: "home", link: "/"},
		{name: "projects", link: "/projects"},
		{name: "about", link: "/about"},
		{name: "contact", link: "/contact"}
	];
		
</script>

<nav>
	<ul class="style=none">
	{#each navLinks as link}
	<a href={link.link}><li>{link.name}</li></a>
	{/each}
	</ul>
</nav>

{@render children()}
