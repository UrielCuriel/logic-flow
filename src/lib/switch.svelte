<script lang="ts">
	import { Node, generateOutput, generateInput, Anchor } from 'svelvet';

	export let id = 0;
	export let position = { x: 0, y: 0 };
	export let isOn = false;
	export let connetcionKey: [string | number, string | number] = [0, 0];
	let idNode = `switch-${id}`;
	let idOutput = `switch-${id}-output`;

	const initalData = {
		isOn: isOn
	};

	type Inputs = {
		isOn: boolean;
	};

	const input = generateInput(initalData);

	const procesor = (inputs: Inputs) => inputs.isOn;

	const output = generateOutput(input, procesor);

	const toggle = () => {
		input.update((currentInputs) => {
			currentInputs?.isOn?.update &&
				currentInputs.isOn.update((currentValue) => {
					return !currentValue;
				});

			return currentInputs;
		});
	};
	$input.isOn.subscribe((value) => (isOn = value));
</script>

<Node
	on:nodeClicked={toggle}
	{position}
	id={idNode}
	locked={true}
	bgColor="transparent"
	outputs={1}
	borderWidth={0}
	width={112}
	height={58}
>
	<svg id="svg2" viewBox="0 0 56 29" version="1.0" width="112" height="58">
		<rect
			style="fill:#d71c4a;fill-opacity:1;stroke:none;stroke-width:1.34948;stroke-linecap:square;stroke-dasharray:none;stroke-opacity:1"
			id="rect2-6"
			width="27"
			height="27"
			x="28"
			y="1"
		/>
		<path
			style="font-weight:bold;font-size:24px;font-family:N27;-inkscape-font-specification:'N27 Bold';text-align:center;text-anchor:middle;fill:#ffffff;stroke-linecap:square"
			d="m 35.447266,16.9375 v -4.875 q 0,-2.8242187 1.652343,-4.5117188 1.664063,-1.6992187 4.394532,-1.6992187 2.730468,0 4.394531,1.6992187 1.664062,1.6875001 1.664062,4.5117188 v 4.875 q 0,2.824219 -1.664062,4.523437 -1.664063,1.6875 -4.394531,1.6875 -2.730469,0 -4.394532,-1.6875 -1.652343,-1.699218 -1.652343,-4.523437 z m 3.082031,0 q 0,3.210937 2.964844,3.210937 0.832031,0 1.429687,-0.257812 0.609375,-0.257813 0.925781,-0.714844 0.328125,-0.46875 0.46875,-1.007812 0.152344,-0.550782 0.152344,-1.230469 v -4.875 q 0,-0.679687 -0.152344,-1.21875 -0.140625,-0.550781 -0.46875,-1.0078125 -0.316406,-0.46875 -0.925781,-0.7265625 -0.597656,-0.2578125 -1.429687,-0.2578125 -2.964844,0 -2.964844,3.2109375 z m 1.488281,-1.03125 v -2.976562 h 2.964844 v 2.976562 z"
			id="text2"
			aria-label="0"
		/>
		<g id="g3" transform="translate(1,1)">
			<rect
				style="fill:#61ffca;fill-opacity:1;stroke:none;stroke-width:1.34948;stroke-linecap:square;stroke-dasharray:none;stroke-opacity:1"
				id="rect2"
				width="27"
				height="27"
				x="0"
				y="0"
			/>
			<path
				style="font-weight:bold;font-size:24px;font-family:N27;-inkscape-font-specification:'N27 Bold';text-align:center;text-anchor:middle;fill:#ffffff;stroke-linecap:square"
				d="M 9.5273438,6.9023437 11.179688,5.0976562 h 6.292968 V 21.902344 H 14.34375 V 5.7070312 L 9.5507813,11.179688 Z"
				id="text2-3"
				aria-label="1"
			/>
		</g>
		<g id="g7" transform={isOn ? 'translate(27, 0)' : 'translate(0, 0)'}>
			<rect
				style="fill:#ffffff;fill-opacity:1;stroke:none;stroke-width:2.96363;stroke-linecap:square;stroke-dasharray:none;stroke-opacity:1"
				id="rect5"
				width="27"
				height="27"
				x="1"
				y="1"
			/>
			<rect
				style="fill:#48647f;fill-opacity:1;stroke:none;stroke-width:2.02396;stroke-linecap:square;stroke-dasharray:none;stroke-opacity:1"
				id="rect5-1"
				width="17"
				height="20"
				x="6"
				y="4.5"
			/>
		</g>
		<rect
			style="fill:none;fill-opacity:1;stroke:#48647f;stroke-width:1.04576;stroke-linecap:square;stroke-dasharray:none;stroke-opacity:1"
			id="rect1"
			width="54.95425"
			height="27.954245"
			x="0.52288002"
			y="0.52288002"
		/>
	</svg>
	<div class="output-anchors">
		<Anchor
			bgColor={isOn ? '#61ffca' : '#d71c4a'}
			output
			direction="east"
			id={idOutput}
			outputStore={output}
			connections={[connetcionKey]}
		/>
	</div>
</Node>

<style>
	:root[svelvet-theme='light'] {
		--shadow-color: transparent;
		--shadow-elevation-medium: none;
	}
	:global(.svelvet-node > div:nth-child(1)) {
		display: flex !important;
		gap: 0.1rem;
		align-items: center;
	}
</style>
