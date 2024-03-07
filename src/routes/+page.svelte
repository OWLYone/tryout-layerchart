<script>
	import { Chart, Svg, Axis, Group, Spline, Points } from "layerchart";
	import {
		curveLinearClosed,
		curveCatmullRomClosed,
		curveCatmullRom,
	} from "d3-shape";

	import { scaleBand } from "d3-scale";
	export let data;

	const pitchData = [
		{ name: "fastball", value: 10 },
		{ name: "change", value: 0 },
		{ name: "slider", value: 4 },
		{ name: "cutter", value: 8 },
		{ name: "curve", value: 5 },
	];
	let curve = curveLinearClosed;
</script>

<h1>Welcome to SvelteKit</h1>
<p>
	Visit <a href="https://kit.svelte.dev">kit.svelte.dev</a> to read the documentation
</p>

<div class="h-[300px] p-4 border rounded">
	<Chart
		data={pitchData}
		x="name"
		xScale={scaleBand()}
		xDomain={pitchData.map((d) => d.name)}
		xRange={[0, 2 * Math.PI]}
		y="value"
		yRange={({ height }) => [0, height / 2]}
		yPadding={[0, 10]}
		padding={{ top: 32, bottom: 8 }}
	>
		<Svg>
			<Group center>
				<Axis
					placement="radius"
					grid={{ class: "stroke-surface-content/20 fill-surface-200/50" }}
					ticks={[0, 5, 10]}
					format={(d) => ""}
				/>
				<Axis placement="angle" grid={{ class: "stroke-surface-content/20" }} />
				<Spline radial {curve} class="stroke-primary fill-primary/20" />
				<Points radial class="fill-primary stroke-surface-200" />
			</Group>
		</Svg>
	</Chart>
</div>
