<script>
	import { Background, Svelvet } from 'svelvet';
	import AndGate from '$lib/andGate.svelte';
	import Switch from '$lib/switch.svelte';
	import XorGate from '$lib/xorGate.svelte';
	import NotGate from '$lib/notGate.svelte';
	import Output from '$lib/output.svelte';

	let initialNodes = [
		{
			id: 1,
			position: { x: 27, y: 27 },
			component: Switch,
			isOn: true,
			connetcionKey: ['and-10', 'and-10-input-0']
		},
		{
			id: 2,
			position: { x: 27, y: 139 },
			component: Switch,
			isOn: true,
			connetcionKey: ['and-11', 'and-11-input-1']
		},
		{
			id: 3,
			position: { x: 27, y: 251 },
			component: Switch,
			isOn: true,
			connetcionKey: ['and-12', 'and-12-input-1']
		},
		{
			id: 4,
			position: { x: 27, y: 363 },
			component: Switch,
			isOn: false,
			connetcionKey: ['not-9', 'not-9-input']
		},
		{
			id: 5,
			position: { x: 27, y: 475 },
			component: Switch,
			isOn: true,
			connetcionKey: ['xor-13', 'xor-13-input-1']
		},
		{
			id: 6,
			position: { x: 27, y: 587 },
			component: Switch,
			isOn: true,
			connetcionKey: ['and-14', 'and-14-input-1']
		},
		{
			id: 7,
			position: { x: 27, y: 699 },
			component: Switch,
			isOn: true,
			connetcionKey: ['and-15', 'and-15-input-1']
		},
		{
			id: 8,
			position: { x: 27, y: 811 },
			component: Switch,
			isOn: true,
			connetcionKey: ['and-16', 'and-16-input-1']
		},
		{
			id: 9,
			position: { x: 195, y: 348 },
			component: NotGate,
			connetcionKey: ['and-10', 'and-10-input-1']
		},
		{
			id: 10,
			position: { x: 475, y: 18 },
			component: AndGate,
			connetcionKey: ['and-11', 'and-11-input-0']
		},
		{
			id: 11,
			position: { x: 727, y: 118 },
			component: AndGate,
			connetcionKey: ['and-12', 'and-12-input-0']
		},
		{
			id: 12,
			position: { x: 979, y: 230 },
			component: AndGate,
			connetcionKey: ['xor-13', 'xor-13-input-0']
		},
		{
			id: 13,
			position: { x: 1231, y: 454 },
			component: XorGate,
			connetcionKey: ['and-14', 'and-14-input-0']
		},
		{
			id: 14,
			position: { x: 1483, y: 566 },
			component: AndGate,
			connetcionKey: ['and-15', 'and-15-input-0']
		},
		{
			id: 15,
			position: { x: 1735, y: 677 },
			component: AndGate,
			connetcionKey: ['and-16', 'and-16-input-0']
		},
		{
			id: 16,
			position: { x: 1987, y: 790 },
			component: AndGate,
			connetcionKey: ['output-17', 'output-17-input']
		},
		{ id: 17, position: { x: 2239, y: 776 }, component: Output }
	];
	let zoom = 0.5;
</script>

<Svelvet height={800} controls {zoom} locked fitView>
	{#each initialNodes as { component, ...node }}
		<svelte:component this={component} {...node} />
	{/each}
	<Background dotColor="#48647f" bgColor="#cbd4de" gridWidth={14} dotSize={1.4} slot="background" />
</Svelvet>
