<script>
	import Vote from '$lib/components/Vote.svelte';
	import Chart from '$lib/components/Chart.svelte';
	import Option from '$lib/components/Option.svelte';

	import { pets } from '$lib/stores/votes.js';

	$: total_votes = $pets.map((pet) => pet.votes).reduce((total, next) => total + next, 0);
</script>

<svelte:head>
	<title>Serverless Voting App</title>
</svelte:head>

<div class="navbar bg-base-100">
	<div class="flex-1">
		<div class="normal-case text-sm md:text-4xl font-bold">What is your favorite coffee?</div>
	</div>
	<p class="px-2 text-sm md:text-xl font-bold">
		Total votes: {new Intl.NumberFormat().format(total_votes)}
	</p>
	<Option />
</div>

<div class="flex flex-col md:flex-row">
	{#each $pets as pet}
		<Vote vote={pet} bind:value={pet.votes} />
	{/each}
</div>

<div class="h-96 shadow-xl my-4 bg-base-100 rounded-2xl p-5 border-4">
	<Chart data={$pets} />
</div>
