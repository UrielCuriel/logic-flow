<script>
	import { Background, Svelvet } from 'svelvet';
	import AndGate from '$lib/andGate.svelte';
	import Switch from '$lib/switch.svelte';
	import XorGate from '$lib/xorGate.svelte';
	import NotGate from '$lib/notGate.svelte';
	import Output from '$lib/output.svelte';

	let initialNodes = [
		{ id: 1, position: { x: 27, y: 27 }, component: Switch, isOn: false },
		{ id: 2, position: { x: 27, y: 139 }, component: Switch, isOn: false },
		{ id: 3, position: { x: 27, y: 251 }, component: Switch, isOn: false },
		{ id: 4, position: { x: 27, y: 363 }, component: Switch, isOn: false },
		{ id: 5, position: { x: 27, y: 475 }, component: Switch, isOn: false },
		{ id: 6, position: { x: 27, y: 587 }, component: Switch, isOn: false },
		{ id: 7, position: { x: 27, y: 699 }, component: Switch, isOn: false },
		{ id: 8, position: { x: 27, y: 811 }, component: Switch, isOn: false },
		{ id: 9, position: { x: 195, y: 348 }, component: NotGate, inputKey: 'switch-4' },
		{ id: 10, position: { x: 475, y: 18 }, component: AndGate, inputs: ['not-9', 'switch-1'] },
		{ id: 11, position: { x: 727, y: 118 }, component: AndGate, inputs: ['switch-2', 'and-10'] },
		{ id: 12, position: { x: 979, y: 230 }, component: AndGate, inputs: ['switch-3', 'and-11'] },
		{ id: 13, position: { x: 1231, y: 454 }, component: XorGate, inputs: ['and-12', 'switch-5'] },
		{ id: 14, position: { x: 1483, y: 566 }, component: AndGate, inputs: ['xor-13', 'switch-6'] },
		{ id: 15, position: { x: 1735, y: 677 }, component: AndGate, inputs: ['switch-7', 'and-14'] },
		{ id: 16, position: { x: 1987, y: 790 }, component: AndGate, inputs: ['switch-8', 'and-15'] },
		{ id: 17, position: { x: 2239, y: 754 }, component: Output, inputKey: 'and-16' }
	];
</script>

<Svelvet height={800} controls>
	{#each initialNodes as { component, ...node }}
		<svelte:component this={component} {...node} />
	{/each}
	<Background dotColor="#48647f" bgColor="#cbd4de" gridWidth={14} dotSize={1.4} slot="background" />
</Svelvet>
