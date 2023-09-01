<script>
	import { fade, slide } from 'svelte/transition';
	import { quintOut } from 'svelte/easing';
	import Star from './star.svelte';
    import { starss } from './stores.js';
	
	// User rating states
	let rating = null;
	let hoverRating = null;
	
	// form interaction states
	let collectFeedback = false;
	let feedbackCompleted = false
	
	// using curried function to initialize hover with id
	const handleHover = (id) => () => {
		hoverRating = id;
	}
	const handleRate = (id) => (event) => {
		if (collectFeedback && 
				rating && 
				rating.toString() === event.srcElement.dataset.starid
		) {
			collectFeedback = false;
			return;
		}
		rating = id;
		collectFeedback = true;
	}
	
	let stars = [
		{ id: 1, title: 'One Star' },
		{ id: 2, title: 'Two Stars' },
		{ id: 3, title: 'Three Stars' },
		{ id: 4, title: 'Four Stars' },
		{ id: 5, title: 'Five Stars' },
	]
    $: starss.set(rating);
</script>
<style>
	.starContainer {
		display: inline-block;
		transition: background .2s ease-out;
		border-radius: 8px;
		padding: 4px 6px 0;
	}
	:global(button) {
		cursor: pointer;
	}
</style>

<div class="feedback"> 
		<span class="starContainer">
		{#each stars as star (star.id)}
			<Star 
					filled={hoverRating ? (hoverRating >= star.id) : (rating >= star.id)} 
					starId={star.id}
					on:mouseover={handleHover(star.id)} 
					on:mouseleave={() => hoverRating = null}
					on:click={handleRate(star.id)}
				/>
		{/each}
  </span>
</div>