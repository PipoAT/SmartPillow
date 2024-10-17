<script>
	import { onMount } from 'svelte';
	import { Cloud as CloudIcon, Cloudy as CloudyIcon, Moon } from 'lucide-svelte'; // Import both Cloud and Cloudy icons

	let clouds = new Array(5).fill().map((_, i) => {
		return {
			size: Math.random() * (100 - 50) + 50, // Random size between 50px and 100px
			x: 100 + Math.random() * 20, // Start off-screen right
			y: Math.random() * 50, // Random vertical position (0% to 50%)
			r: 0.5 + Math.random() * 1 // Random scale
		};
	});
  let cloudys = new Array(5).fill().map((_, i) => {
		return {
			size: Math.random() * (100 - 50) + 50, // Random size between 50px and 100px
			x: 100 + Math.random() * 20, // Start off-screen right
			y: Math.random() * 50, // Random vertical position (0% to 50%)
			r: 0.5 + Math.random() * 1 // Random scale
		};
	});

	let moonPosition = { x: Math.random() * 100, y: Math.random() * 10 }; // Position for the moon

	onMount(() => {
		let frame;

		function loop() {
			frame = requestAnimationFrame(loop);

			clouds = clouds.map(cloud => {
				cloud.x -= 0.1 * cloud.r; // Move left
				if (cloud.x < -10) cloud.x = 110; // Reset to the right side when off-screen
				return cloud;
			});

      cloudys = cloudys.map(cloud => {
				cloud.x -= 0.1 * cloud.r; // Move left
				if (cloud.x < -10) cloud.x = 110; // Reset to the right side when off-screen
				return cloud;
			});

		}

		loop();

		return () => cancelAnimationFrame(frame);
	});
</script>

<style>

</style>

<div class="background-cloud">
	<div>
		<h1>Sleepy Vibes</h1>
		<p>Relax and unwind with this soothing purple gradient theme.</p>
	</div>
	
	{#each clouds as cloud}
		<CloudyIcon
			class="cloud"
			style="
				width: {cloud.size}px; 
				height: {cloud.size}px; 
				left: {cloud.x}%; 
				top: {cloud.y}%; 
				transform: scale({cloud.r});
			"
		/>
	{/each}

  {#each cloudys as cloud}
  <CloudIcon
    class="cloud"
    style="
      width: {cloud.size}px; 
      height: {cloud.size}px; 
      left: {cloud.x}%; 
      top: {cloud.y}%; 
      transform: scale({cloud.r});
    "
  />
  {/each}

</div>
