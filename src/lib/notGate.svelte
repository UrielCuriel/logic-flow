<script lang="ts">
	import { Node, generateOutput, generateInput, Anchor } from 'svelvet';
	export let id = 0;
	export let position = { x: 0, y: 0 };
	export let connetcionKey: [string | number, string | number] = [0, 0];
	let idNode = `not-${id}`;
	let idInput = `not-${id}-input`;
	let idOutput = `not-${id}-output`;
	let notOutput = false;
	const initalData = {
		[idInput]: false
	};
	type Inputs = {
		[x: string]: boolean;
	};

	const input = generateInput(initalData);

	const procesor = (inputs: Inputs) => {
		return !inputs[idInput];
	};

	const output = generateOutput(input, procesor);

	output.subscribe((value) => (notOutput = value));
</script>

<Node
	{position}
	id={idNode}
	locked={false}
	bgColor="transparent"
	outputs={1}
	borderWidth={0}
	width={158}
	height={87}
>
	<div class="input-anchors">
		<Anchor id={idInput} key={idInput} inputsStore={input} direction="west" input />
	</div>
	<svg viewBox="0 0 56 29" width="158" height="87">
		<path
			id="path6087"
			stroke-linecap="square"
			d="m 42.949933,14.498205 c 0,1.312254 -1.139778,2.364422 -2.544146,2.364422 -1.404369,0 -2.544146,-1.052168 -2.544146,-2.364422 0,-1.300432 1.139777,-2.364421 2.544146,-2.364421 1.404368,0 2.544146,1.063989 2.544146,2.364421 z M 13.05622,27.502524 V 1.4938866 L 37.207796,14.498205 Z M 42.949933,14.498205 h 11.448656 m -52.7910256,0 H 13.05622"
			style="fill:{notOutput
				? '#61ffca'
				: '#d71c4a'};fill-opacity:1;stroke:#48647f;stroke-width:3.7998;stroke-dasharray:none;stroke-linecap:round;stroke-linejoin:round"
		/>
	</svg>
	<div class="output-anchors">
		<Anchor id={idOutput} outputStore={output} direction="east" output connections={[connetcionKey]} />
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
