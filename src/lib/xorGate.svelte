<script lang="ts">
	import { Node, generateOutput, generateInput, Anchor } from 'svelvet';
	export let id = 0;
	export let position = { x: 0, y: 0 };
	export let connetcionKey: [string | number, string | number] = [0, 0];
	let idNode = `xor-${id}`;
	let idInput = `xor-${id}-input`;
	let idOutput = `xor-${id}-output`;
	let xorOutput = false;
	const initalData = {
		[`${idInput}-0`]: false,
		[`${idInput}-1`]: false
	};
	type Inputs = {
		[x: string]: boolean;
	};

	const input = generateInput(initalData);

	const procesor = (inputs: Inputs) => {
		return Object.values(inputs).reduce((acc, curr) => {
			return acc !== curr;
		});
	};

	const output = generateOutput(input, procesor);

	output.subscribe((value) => (xorOutput = value));
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
		{#each Object.keys(initalData) as key}
			<Anchor id={key} {key} inputsStore={input} direction="west" input />
		{/each}
	</div>
	<svg viewBox="0 0 56 29" width="158" height="87">
		<path
			id="path6087"
			stroke-linecap="square"
			d="m 12.451844,1.7769901 v 0.068509 c 2.041217,3.7288198 3.220093,8.0448553 3.220093,12.6544984 0,4.61943 -1.178876,8.935467 -3.220093,12.664285 v 0.05873 h 12.502575 c 8.920465,0 16.708467,-5.118564 20.885583,-12.723008 C 41.662886,6.9053407 33.874884,1.7769901 24.954419,1.7769901 Z m -4.6412407,0.068509 c 2.0412177,3.7288198 3.2200927,8.0448553 3.2200927,12.6544984 0,4.61943 -1.178875,8.935467 -3.2200927,12.664285 M 45.868778,14.499997 h 8.354234 M 1.7769901,8.1384937 H 10.131224 M 1.7769901,20.8615 h 8.3542339"
			style="fill:{xorOutput
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
