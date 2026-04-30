<script>
	let r=500;
	let cntSlices=9;
	let content=[
		"x4",
		"x3",
		"x3",
		"x2",
		"x2",
		"x2",
		"w",
		"x1",
		"white",
	];
	let rotation=$state(0);
	let rotationInc=$state(0);
	let contentRadius = r*4/5;
	let spinning = $state(false);
	let outerWidth=17;
	
	let sliceAngle=$derived(3.142*2/cntSlices);
	let sliceDegrees=$derived(360/cntSlices|0);
	let result=$derived((((270-rotation)/sliceDegrees)+cntSlices|0)%cntSlices);

	setInterval(()=>{
		if (rotationInc > 0.06) {
			rotation+=rotationInc;	
			rotationInc *= 0.99;
			if (rotation > 360) rotation-= 360;
		} else {
			if ( spinning ) {
				spinning=false;
			}
		}
	},10);
    function color(){
        let color = $state(content[idx%content.length])
        console.log(color)
    }



</script>

<!-- <button on:click={()=>{rotation+=sliceDegrees/2}}>Inc</button> -->
<button onclick={()=>{rotationInc=15+5*Math.random();spinning=true;}}>Spin</button><br>{rotation|0} {rotationInc*100|0} {content[result%content.length]} ({result})<br>

<svg viewbox="0 0 {r*2+outerWidth*2} {r*2+outerWidth*2}" width={r+outerWidth*2} height={r+outerWidth*2}>
	<g transform="translate({r+outerWidth} {r+outerWidth}) rotate({rotation}) translate({-r} {-r}) ">
	<circle r={r} cx={r} cy={r} fill="lightgray" stroke-width={outerWidth} stroke="red"/>
		{#each Array(cntSlices) as angle, idx}
			{@const x=Math.cos(sliceAngle*idx)}
			{@const y=Math.sin(sliceAngle*idx)}
			{@const x2=Math.cos(sliceAngle*(idx+1))}
			{@const y2=Math.sin(sliceAngle*(idx+1))}
			{@const tx=Math.cos(sliceAngle*(idx+.5))*contentRadius+r}
			{@const ty=Math.sin(sliceAngle*(idx+.5))*contentRadius+r}
			{@const contentRotation=90+(360/cntSlices*(idx+0.5))|0}
			{@const path = [
					`M ${x*r+r} ${y*r+r}`, // Move
					`A ${r} ${r} 0 0 1 ${x2*r+r} ${y2*r+r}`, // Arc   
					`L ${r} ${r}`, // Line
				].join(' ')}
			<path d={path} fill={"white"}/>}
			<g transform="translate({tx} {ty}) rotate({contentRotation}) translate({-tx} {-ty}) ">
				<text font-size={24} x={tx} y={ty} text-anchor ="middle">{content[idx%content.length]}</text>}
			</g>
		{/each}
	</g>
</svg>
<br>
