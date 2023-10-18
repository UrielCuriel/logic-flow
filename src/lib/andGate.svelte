<script lang="ts">
	import { Node, generateOutput, generateInput, Anchor } from 'svelvet';
	export let id = 0;
	export let position = { x: 0, y: 0 };
	export let inputs: string[] = [];
	let andOutput = false;
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
		return Object.values(inputs).every((input) => input);
	};

	const output = generateOutput(input, procesor);

	output.subscribe((value) => (andOutput = value));
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
			d="M 31.099308,27.100103 H 11.285425 V 1.90184 L 31.099308,1.8999 c 7.483393,0 13.556869,5.6448449 13.556869,12.600101 0,6.955256 -6.073476,12.6001 -13.556869,12.6001 z M 44.656177,14.500002 h 9.443924 M 1.8999,8.199952 h 9.385525 M 1.8999,20.800052 h 9.385525"
			style="fill:{andOutput
				? '#61ffca'
				: '#d71c4a'};fill-opacity:1;stroke:#48647f;stroke-width:3.7998;stroke-dasharray:none;stroke-linecap:round;stroke-linejoin:round"
		/>
	</svg>
	<div class="output-anchors">
		<Anchor outputStore={output} direction="east" output connections={[['output', `and-${id}`]]} />
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
