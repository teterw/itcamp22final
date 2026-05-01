

<script>
	import chichipop from '$lib/assets/chichi-pop.png'
	import temple from '$lib/assets/templw.png'
	import catup from '$lib/assets/catup.png'
	import logo from '$lib/assets/logo.jpg'
</script>



<div class="items-center flex-col  bg-cover h-screen bg-center  " style="
background-image: url({chichipop}); ">
	<div class="bg-white/30 p-10 rounded-2xl h-screen w-[500px]">
		<div class="bg-white p-8 rounded-full">
			<img src="{logo}" alt="logo" class="rounded-full">
		</div>
		<div class="">
			<a class="m" href="/clickgame"><button class="m-4 duration-200 w-100 hover:bg-white/80 cursor-pointer bg-white text-xl  px-4 py-3 rounded-4xl">Chichi pop</button></a>
			<br>
			<a href="/gacha"><button class="m-4 duration-200 w-100 hover:bg-white/80 cursor-pointer bg-white text-xl  px-4 py-3 rounded-4xl">สุ่มดวง</button></a>
		</div>
	</div>

	
	
	<div class="absolute right-0 bottom-0">
		<img src="{catup}" alt="component" class="h-[90%] -ml-10">
	</div>

	<div class="absolute right-0">
		<img src="{temple}" alt="component" class="w-250  -ml-10">
	</div>
</div>