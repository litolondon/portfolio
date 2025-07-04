<script lang="ts">
	import '../app.css';

	let { children } = $props();

	import { goto, pushState } from "$app/navigation";
    import { badges, contactBadges } from "$lib/badges";
    import { texts } from "$lib/typewriter";
	import { onMount } from "svelte";
	import { page } from '$app/state';

    const typingSpeed: number = 50;
    const pauseDuration: number = 2000;

	
    let twIndex: number = $state(0);
    let displayText: string = $state('');
    let isTyping: boolean = $state(false);
    let isHome: boolean = $state(true);
    let isProjects: boolean = $state(false);
    let isContact: boolean = $state(false);


    function handleHome(){
        isHome = true;
        isContact = false;
        isProjects = false;
    }
    function handleProjects(){
        isHome = false;
        isContact = false;
        isProjects = true;
    }
    function handleContact(){
        isHome = false;
        isContact = true;
        isProjects = false;
    }



    const navLinks = [
		{name: "home", link: "/",},
		{name: "projects", link: "/projects"},
		{name: "contact", link: "/contact"}
	];
    
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

<main class="m-2 bg-zinc-950 font-roboto text-green-600 p-7 flex-column" style="height: 90dvh;">

<div class="flex-column justify-between h-fit">
    <section class="flex-column justify-items-start h-26 w-144">
        <h1 class="text-4xl mt-1">i'm carlito london,</h1>
        <div>
            <h2 class="text-2xl inline-block">{displayText}</h2>
            <span class="animate-twcursor inline-block">|</span>
        </div>
    </section>
    <br>
    <ul class="gap-4 font-roboto text-green-600">
        <li class=" text-xl hover:text-green-300 hover: cursor-pointer" onclick={handleHome}><p href="/">home</p></li>
        <li class=" text-xl hover:text-green-300 hover: cursor-pointer" onclick={handleProjects}><p href="/projects">projects</p></li>
        <li class=" text-xl hover:text-green-300 hover: cursor-pointer" onclick={handleContact}><p href="/contact">contact</p></li>
    </ul>
    <br>
    <br>
</div>

<div class="absolute top-8 right-16">
<h1 class="text-center font-bold text-green-300">Skills</h1>
<div id="badges" class="flex gap-3 flex-wrap justify-between p-2 pl-6 pr-6 m-2 rounded-sm border-green-750 border-4 w-72">
    {#each badges as badge}
    <img class="flex align-middle h-7 rounded-md border-dashed border-green-900 border-1 flex-auto" src={badge.src} alt={badge.alt}>
    {/each}
</div>
</div>


{#if isHome}
<div>
    <p>A entry-level web developer, based in Little Rock, Arkansas.</p>
    <p>Turning ideas into reality, led to coding. While coding itself, led to a hunger for learning.</p>
</div>

{/if}

{#if isProjects}
<div class="border"></div>
{/if}
{#if isContact}
<div class="border">
    <h1 class="flex">contact</h1>
    {#each contactBadges as badge}
    <a href={badge.href}><img src={badge.src} alt={badge.alt}></a>
    {/each}
</div>
{/if}




</main>




<style>
    * { 
        font-family: 'Space Grotesk';
        font-family: 'Roboto', sans-serif;
        
    }
</style>


{@render children()}
