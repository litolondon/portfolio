<script lang="ts">
    import type { PageData } from '../contact/$types';
    import { contactBadges } from '$lib/badges';

    let { data }: { data: PageData } = $props();
</script>

<h1 class="text-3xl flex justify-center">contact</h1>
{#each contactBadges as badge}
<a href={badge.href}><img src={badge.src} alt={badge.alt}></a>
{/each}