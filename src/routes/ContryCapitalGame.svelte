<script lang="ts">
	export let data: Record<string, string>;

	type Option = {
		name: string;
		accept: string;
		color: 'Default' | 'Selected' | 'Wrong';
		display: boolean;
	};
	let status: Record<string, Option> = {};
	let prevSlection: Option | undefined;
	let isOver = false;
	Object.entries(data)
		.map((pair) => {
			return [
				{
					name: pair[0],
					accept: pair[1],
					color: 'Default',
					display: true
				},
				{
					name: pair[1],
					accept: pair[0],
					color: 'Default',
					display: true
				}
			] as Option[];
		})
		.flat()
		.sort(() => Math.random() - 0.5)
		.forEach((option) => (status[option.name] = option));

	console.log(status);
</script>

<div>
	{#if isOver}
		<h1>Congrats!</h1>
	{:else}
		{#each Object.values(status) as item, i (i)}
			{#if item.display}
				<button
					class={item.color}
					on:click={() => {
						if (!prevSlection) {
							for (const key in status) {
								if (Object.prototype.hasOwnProperty.call(status, key)) {
									status[key].color = 'Default';
								}
							}
						}
						if (item.color == 'Selected') {
							status[item.name].color = 'Default';
						} else {
							status[item.name].color = 'Selected';
							if (!prevSlection) return (prevSlection = item);
							if (status[item.name].accept == prevSlection.name) {
								status[item.name].display = false;
								status[prevSlection.name].display = false;
								let done = true;
								for (const key in status) {
									if (Object.prototype.hasOwnProperty.call(status, key)) {
										if (status[key].display) {
											done = false;
											break;
										}
									}
								}
								isOver = done;
							} else {
								status[item.name].color = 'Wrong';
								status[prevSlection.name].color = 'Wrong';
							}
							prevSlection = undefined;
						}
					}}
				>
					{item.name}
				</button>
			{/if}
		{/each}
	{/if}
</div>

<style>
	.Selected {
		background-color: blue;
		color: white;
	}
	.Wrong {
		background-color: red;
		color: white;
	}
</style>
