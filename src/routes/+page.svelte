<script>
    import { badges } from "$lib/badges";
	import { redirect } from "@sveltejs/kit";

    function contactButton() {
            redirect(308, "/contact")
    }

    
</script>



<div id="badges" class="flex gap-1 bg-gray-500  flex-wrap justify-center-safe ml-8 mr-8 p-2 pl-3 pr-3 rounded-sm">
    {#each badges as badge}
    <img class="flex align-middle h-7 rounded-md " src={badge.src} alt={badge.alt}>
    {/each}
</div>

<h1 class="text-3xl flex justify-center mt-2 font-bold">carlito london,</h1>
<h2 class="text-2xl flex justify-center">web developer. problem solver. lifelong learner</h2>
<p class="text-lg flex justify-center">an aspiring web developer dedicated to mastering the craft of building for the web</p>

<button onclick={contactButton} class="hover:cursor-pointer">reach out</button>