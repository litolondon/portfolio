<script lang="ts">
    import type { PageData } from './$types';
    import { contactBadges } from '$lib/badges';
	import { onMount } from 'svelte';

    let { data }: { data: PageData } = $props();

</script>