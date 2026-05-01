<script>
	import Coin from "$lib/Coin.svelte";
	import { nonpassive } from "svelte/legacy";

	let r = 500;
	let cntSlices = 14;
	let content = [
		"x1.5",
		"x0.7",
		"x1",
		"x3",
		"x1",
		"x2",
		"x1",
		"x2",
		"x1",
		"x1.5",
		"x0",
		"x1",
		"x0.5",
		"x2",
	];
	let colorsave = [];
	let value = [];
	let len = content.length;
	let rotation = $state(0);
	let rotationInc = $state(0);
	let contentRadius = (r * 4) / 5;
	let spinning = $state(false);
	let outerWidth = 17;
	let betamount = $state(0);
	let sliceAngle = $derived((3.142 * 2) / cntSlices);
	let sliceDegrees = $derived((360 / cntSlices) | 0);
	let result = $derived(
		(((270 - rotation) / sliceDegrees + cntSlices) | 0) % cntSlices,
	);
	let score = $state(0);

	setInterval(() => {
		if (rotationInc > 0.06) {
			rotation += rotationInc;
			rotationInc *= 0.99;
			if (rotation > 360) rotation -= 360;
		} else {
			if (spinning) {
				spinning = false;
				betcalc(value, betamount);
			}
		}
	}, 10);
	function color(content, colorsave) {
		for (let i = 0; i < len; i++) {
			if (content[i] == "x0") {
				colorsave.push("#00714e");
			} else if (content[i] == "x0.5") {
				colorsave.push("#007c88");
			} else if (content[i] == "x0.7") {
				colorsave.push("#0083c5");
			} else if (content[i] == "x1") {
				colorsave.push("#0082f3");
			} else if (content[i] == "x1.5") {
				colorsave.push("#6573ff");
			} else if (content[i] == "x2") {
				colorsave.push("#d051eb");
			} else if (content[i] == "x3") {
				colorsave.push("#ff00b2");
			}
		}
	}
	function valuetranslate(content, value) {
		for (let i = 0; i < len; i++) {
			if (content[i] == "x0") {
				value.push(0);
			} else if (content[i] == "x0.5") {
				value.push(0.5);
			} else if (content[i] == "x0.7") {
				value.push(0.7);
			} else if (content[i] == "x1") {
				value.push(1);
			} else if (content[i] == "x1.5") {
				value.push(1.5);
			} else if (content[i] == "x2") {
				value.push(2);
			} else if (content[i] == "x3") {
				value.push(3);
			}
		}
	}
	valuetranslate(content, value);
	color(content, colorsave);
	console.log(colorsave);
	function buttonclick(betamount) {
		console.log(betamount);
		rotationInc = 20 + 5 * Math.random();
		spinning = true;
	}

	function betcalc(value, betamount) {
		score = Math.round(betamount * value[result % content.length]);
		console.log(score);
		
	}
</script>

<!-- <button on:click={()=>{rotation+=sliceDegrees/2}}>Inc</button> -->
<div class="flex flex-col w-full h-screen">
	<div class="justify-center grid">
		<svg
			fill="#000000"
			version="1.1"
			id="Capa_1"
			xmlns="http://www.w3.org/2000/svg"
			xmlns:xlink="http://www.w3.org/1999/xlink"
			width="20px"
			height="20px"
			viewBox="0 0 96.154 96.154"
			xml:space="preserve"
		>
			<g>
				<path
					d="M0.561,20.971l45.951,57.605c0.76,0.951,2.367,0.951,3.127,0l45.956-57.609c0.547-0.689,0.709-1.716,0.414-2.61
		c-0.061-0.187-0.129-0.33-0.186-0.437c-0.351-0.65-1.025-1.056-1.765-1.056H2.093c-0.736,0-1.414,0.405-1.762,1.056
		c-0.059,0.109-0.127,0.253-0.184,0.426C-0.15,19.251,0.011,20.28,0.561,20.971z"
				/>
			</g>
		</svg>
	</div>
	<div class="grid justify-center">
		<svg
			viewbox="0 0 {r * 2 + outerWidth * 2} {r * 2 + outerWidth * 2}"
			width={r + outerWidth * 2}
			height={r + outerWidth * 2}
		>
			<g
				transform="translate({r + outerWidth} {r +
					outerWidth}) rotate({rotation}) translate({-r} {-r}) "
			>
				<circle
					{r}
					cx={r}
					cy={r}
					fill="lightgray"
					stroke-width={outerWidth}
					stroke="gray"
				/>
				{#each Array(cntSlices) as angle, idx}
					{@const x = Math.cos(sliceAngle * idx)}
					{@const y = Math.sin(sliceAngle * idx)}
					{@const x2 = Math.cos(sliceAngle * (idx + 1))}
					{@const y2 = Math.sin(sliceAngle * (idx + 1))}
					{@const tx =
						Math.cos(sliceAngle * (idx + 0.5)) * contentRadius + r}
					{@const ty =
						Math.sin(sliceAngle * (idx + 0.5)) * contentRadius + r}
					{@const contentRotation =
						(90 + (360 / cntSlices) * (idx + 0.5)) | 0}
					{@const path = [
						`M ${x * r + r} ${y * r + r}`, // Move
						`A ${r} ${r} 0 0 1 ${x2 * r + r} ${y2 * r + r}`, // Arc
						`L ${r} ${r}`, // Line
					].join(" ")}
					<path d={path} fill={colorsave[idx % colorsave.length]} />}
					<g
						transform="translate({tx} {ty}) rotate({contentRotation}) translate({-tx} {-ty}) "
					>
						<text font-size={70} x={tx} y={ty} text-anchor="middle"
							>{content[idx % content.length]}</text
						>}
					</g>
				{/each}
			</g>
		</svg>
	</div>
	<div class="justify-center grid">
		<p class="text-center">bet amount</p>
		<div class="flex">
			<input
				bind:value={betamount}
				type="number"
				class="p-1 border rounded-2xl"
			/>
		</div>
		<button
			onclick={() => {
				buttonclick(betamount);
			}}
			class="m-5 inline-flex h-12 items-center justify-center rounded-md bg-neutral-950 px-6 font-medium text-neutral-50 transition active:scale-110"
			>Spin</button
		>
	</div>

	<div class="">
		<Coin />
	</div>
</div>
