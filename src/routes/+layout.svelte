<script lang="ts">
	import '../app.css';

	let { children } = $props();

	import { goto, pushState } from "$app/navigation";
    import { badges } from "$lib/badges";
    import { texts } from "$lib/typewriter";
	import { onMount } from "svelte";

    const typingSpeed = 50;
    const pauseDuration = 2000;

	
    let twIndex = $state(0);
    let displayText = $state('');
    let isTyping = $state(false);
    let terminal: HTMLInputElement;
    let command = $state();
    let screens = $state([]);

    const navLinks = [
		{name: "home", link: "/"},
		{name: "projects", link: "/projects"},
		{name: "about", link: "/about"},
		{name: "contact", link: "/contact"}
	];
    
    function terminalSubmit(event: SubmitEvent) {
        event.preventDefault();

        screens.push(command);

        if (command === 'projects') {
            goto('/projects');
        } else if (command === 'about'){
            goto('/about')
        } else if (command === 'contact'){
            goto('/contact')
        } else {
            screens.push('Invaid Route or Command');
        }

		command = null;
    }

    function contactButton() {
            goto("/contact");
    }

    onMount(() => {
        function nextPhrase() {
        const text = texts[twIndex];
        let pos = 0;
        isTyping = true;

        function step() {
            if (pos < text.length) {
            pos++;
            displayText = text.slice(0, pos);
            setTimeout(step, typingSpeed);
            } else {
            isTyping = false;
            setTimeout(() => {
                displayText = '';
                twIndex = (twIndex + 1) % texts.length;
                nextPhrase();
            }, pauseDuration);
            }
        }

        step();
        }

        nextPhrase();

        //focus terminal
        terminal.focus();
    });

</script>

<main class="m-2 bg-zinc-950 font-roboto text-green-600 p-7 flex h-98">
<div class="flex-column justify-between h-fit">
    <section class="flex-column justify-items-start h-26 w-144">
        <h1 class="text-2xl mt-1">carlito london,</h1>
        <div>
            <h2 class="text-2xl inline-block">{displayText}</h2>
            <span class="animate-twcursor inline-block">|</span>
        </div>
    </section>
    <br>
    <ul class="gap-4 font-roboto text-green-600">
        {#each navLinks as link}
        <li class=" text-xl hover:text-green-300 hover: cursor-pointer"><a href={link.link}>{link.name}</a></li>
        {/each}
    </ul>
    <br>
    <br>

    <form name="terminal" onsubmit={terminalSubmit}>
        <label for="terminal">carlitolondon.org ~ %</label>
        <input
            type="text"
            bind:this={terminal}
            bind:value={command}
            placeholder="type a command…"
            class="border-b-2"
        />
    </form>
</div>

<div class="border-3 b h-full w-full p-2 overflow-y-scroll">
{#each screens as screen}
<p>carlitolondon.org ~ % {screen}</p>
{/each}
</div>

<!-- <div id="badges" class="flex gap-3 flex-wrap justify-between p-2 pl-6 pr-6 m-2 rounded-sm border-green-750 border-4 w-72">
    {#each badges as badge}
    <img class="flex align-middle h-7 rounded-md border-dashed border-green-900 border-1 flex-auto" src={badge.src} alt={badge.alt}>
    {/each}
</div> -->

</main>


<style>
    * { 
        font-family: 'Space Grotesk';
        font-family: 'Roboto', sans-serif;
    }
</style>


{@render children()}
