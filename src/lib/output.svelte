<script lang="ts">
	import { Node, generateOutput, generateInput, Anchor } from 'svelvet';
	export let id = 0;
	export let position = { x: 0, y: 0 };
	let idNode = `output-${id}`;
	let idInput = `output-${id}-input`;

	let finalOutput = false;
	const initalData = {
		[idInput]: false
	};
	type Inputs = {
		[x: string]: boolean;
	};

	const input = generateInput(initalData);

	const procesor = (inputs: Inputs) => {
		return inputs[idInput];
	};

	const output = generateOutput(input, procesor);

	output.subscribe((value) => (finalOutput = value));
</script>

<Node
	{position}
	id={idNode}
	locked={false}
	bgColor="transparent"
	outputs={1}
	borderWidth={0}
	width={158}
	height={158}
>
	<div class="input-anchors">
		<Anchor id={idInput} key={idInput} inputsStore={input} direction="west" input />
	</div>
	<svg viewBox="0 0 112 112" width="158" height="158">
		<circle
			style="fill:{finalOutput
				? '#61ffca'
				: '#d71c4a'};stroke:#48647f;stroke-width:7.15358;stroke-linejoin:round;-inkscape-stroke:none;stroke-opacity:1;fill-opacity:1"
			id="path1"
			cx="56"
			cy="56.048962"
			r="52.42321"
		/>
		{#if finalOutput}
			<path
				d="m 38.010323,26.1723 7.482432,-8.172301 H 73.989677 V 94.097925 H 59.820816 V 20.759477 l -21.704359,24.78224 z"
				id="text1"
				style="font-weight:bold;font-size:108.681px;font-family:N27;-inkscape-font-specification:'N27 Bold';text-align:center;text-anchor:middle;stroke-width:9.70366;stroke-linejoin:round;fill:#fefefe;fill-opacity:1"
				aria-label="1"
			/>
		{:else}
			<path
				d="M 28.590949,67.086876 V 45.011048 q 0,-12.789121 7.482433,-20.430754 7.535499,-7.6947 19.900085,-7.6947 12.364586,0 19.900085,7.6947 7.535499,7.641633 7.535499,20.430754 v 22.075828 q 0,12.789122 -7.535499,20.483822 -7.535499,7.641632 -19.900085,7.641632 -12.364586,0 -19.900085,-7.641632 -7.482433,-7.6947 -7.482433,-20.483822 z m 13.956594,0 q 0,14.540329 13.425924,14.540329 3.767749,0 6.474161,-1.167471 2.759479,-1.167472 4.192285,-3.237081 1.485873,-2.122676 2.122676,-4.563753 0.689869,-2.494144 0.689869,-5.572024 V 45.011048 q 0,-3.07788 -0.689869,-5.518957 -0.636803,-2.494144 -2.122676,-4.563753 -1.432806,-2.122675 -4.192285,-3.290147 -2.706412,-1.167472 -6.474161,-1.167472 -13.425924,0 -13.425924,14.540329 z M 49.287038,62.41699 V 48.937998 H 62.712963 V 62.41699 Z"
				id="text1-6"
				style="font-weight:bold;font-size:108.681px;font-family:N27;-inkscape-font-specification:'N27 Bold';text-align:center;text-anchor:middle;stroke-width:9.70366;stroke-linejoin:round;fill:#fefefe;fill-opacity:1"
				aria-label="0"
			/>
		{/if}
	</svg>
</Node>

<style>
	.input-anchors {
		display: flex;
		flex-direction: column;
		justify-content: space-between;
		gap: 10px;
	}
</style>
