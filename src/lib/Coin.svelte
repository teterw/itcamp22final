<script>
    import yen from "$lib/assets/yen.png";
    let coin = $state(0)
</script>

<div class="border fixed bottom-0 w-1/2">
    <div class="flex justify-start">
        <div class="border w-30 h-10 rounded-2xl"></div>
    </div>
</div>
<div class="border fixed bottom-0 w-full">
    <div class="flex justify-end">
        <div
            class="bg-black border w-70 h-20 rounded-full m-4 flex justify-end drop-shadow-xl/50"
        >
            <div class="text-[#FFB957] items-center flex mb-2">
                <h1 class="font-bold text-4xl text-shadow-2xs text-shadow-[#FFB957]">0</h1>
            </div>
            <div class="justify-end flex items-center">
                <img src={yen} alt="" class="w-20 h-20 m-2 mb-4.5" />
            </div>
        </div>
    </div>
</div>
