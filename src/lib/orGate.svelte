<script lang="ts">
	import { Node, generateOutput, generateInput, Anchor } from 'svelvet';
	export let id = 0;
	export let position = { x: 0, y: 0 };
	export let inputs: string[] = [];
	let orOutput = false;
	const initalData = inputs
		.map((input) => {
			return {
				[input]: false
			};
		})
		.reduce((acc, curr) => {
			return {
				...acc,
				...curr
			};
		}, {});

	type Inputs = {
		[x: string]: boolean;
	};

	const input = generateInput(initalData);

	const procesor = (inputs: Inputs) => {
		return Object.values(inputs).reduce((acc, curr) => {
			return acc || curr;
		});
	};

	const output = generateOutput(input, procesor);

	output.subscribe((value) => (orOutput = value));
</script>

<Node
	{position}
	{id}
	locked={false}
	bgColor="transparent"
	outputs={1}
	borderWidth={0}
	width={158}
	height={87}
>
	<div class="input-anchors">
		{#each inputs as key}
			<Anchor id={key} {key} inputsStore={input} direction="west" input />
		{/each}
	</div>
	<svg viewBox="0 0 56 29" width="158" height="87">
		<path
			id="path6087"
			stroke-linecap="square"
			d="m 8.4776355,1.8860246 v 0.060234 c 2.2301135,3.7063291 3.5180825,7.9868235 3.5180825,12.5694594 0,4.581663 -1.287969,8.862158 -3.5180825,12.566544 v 0.05829 H 22.137207 c 9.745971,0 18.25468,-5.08588 22.81835,-12.624835 C 40.391887,6.9757908 31.883178,1.8860246 22.137207,1.8860246 Z M 44.986996,14.515718 h 9.12734 M 1.8856676,8.200871 H 11.013008 M 1.8856676,20.830564 h 9.1273404"
			style="fill:{orOutput
				? '#61ffca'
				: '#d71c4a'};fill-opacity:1;stroke:#48647f;stroke-width:3.7998;stroke-dasharray:none;stroke-linecap:round;stroke-linejoin:round"
		/>
	</svg>
	<div class="output-anchors">
		<Anchor outputStore={output} direction="east" output connections={[['output', `or-${id}`]]} />
	</div>
</Node>

<style>
	.input-anchors {
		display: flex;
		flex-direction: column;
		justify-content: space-between;
		gap: 10px;
	}
</style>
