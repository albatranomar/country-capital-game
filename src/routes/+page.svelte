<script lang="ts">
	import ContryCapitalGame from './ContryCapitalGame.svelte';
</script>

<h1>Welcome to SvelteKit</h1>
<p>Visit <a href="https://kit.svelte.dev">kit.svelte.dev</a> to read the documentation</p>
<br />

<svelte:component
	this={ContryCapitalGame}
	data={{
		Germany: 'Berlin',
		Azerbaijan: 'Baku'
	}}
/>
