<script>
    import { badges } from "$lib/badges";
</script>

<h1 class="text-3xl flex justify-center mt-2 mb-2">carlito london</h1>

<div id="badges" class="flex gap-1 bg-gray-500  flex-wrap justify-center-safe ml-8 mr-8 p-2 pl-3 pr-3 rounded-sm">
    {#each badges as badge}
    <img class="flex align-middle h-7 rounded-md " src={badge.src} alt={badge.alt}>
    {/each}
</div>