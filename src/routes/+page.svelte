<script lang=ts>
	import { goto } from "$app/navigation";
    import { badges } from "$lib/badges";
    import { texts } from "$lib/typewriter";
	import { onMount } from "svelte";

    const typingSpeed = 50;
    const pauseDuration = 2000;

	
    let twIndex = $state(0);
    let displayText = $state('');
    let isTyping = $state(false);
    let navInput = $state();

    
    if (navInput == 'projects'){
        goto("/projects");
    }

    const navLinks = [
		{name: "home", link: "/"},
		{name: "projects", link: "/projects"},
		{name: "about", link: "/about"},
		{name: "contact", link: "/contact"}
	];
    

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
    });
</script>

<main class="m-2 bg-zinc-950 font-roboto text-green-600 p-8">



<section class="flex-column justify-items-start">
    <h1 class="text-2xl mt-2">carlito london,</h1>
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

<form>
    <input type="text" id="nav" class="border-b-2" bind:this={navInput}  placeholder="type here...">
    <input type="submit" value="enter">
</form>


<!-- <div class="flex justify-center">
    <button onclick={contactButton} class="hover:cursor-pointer  border-2 rounded-sm p-1.5">reach out</button>
</div>

<div id="badges" class="flex gap-2 flex-wrap justify-center-safe p-2 pl-3 pr-3 m-2 ounded-sm border-green-750 border-4">
    {#each badges as badge}
    <img class="flex align-middle h-7 rounded-md border-dashed border-green-900 border-1" src={badge.src} alt={badge.alt}>
    {/each}
</div> -->

</main>


<style>
    * { 
        font-family: 'Space Grotesk';
        font-family: 'Roboto', sans-serif;
    }
</style>