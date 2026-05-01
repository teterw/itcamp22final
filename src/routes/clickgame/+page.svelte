<script>
   import chichipop from '$lib/assets/chichi-pop.png'
   import catup from '$lib/assets/catup.png'
   import catdown from '$lib/assets/catdown.png'
    let counter = $state(0)
    let coins = $state(0)

    
    let images = [
      catup,
      catdown
    ];
    let currentIndex = $state(0);
    
    function toggleImage() {
      currentIndex = (currentIndex + 1) % images.length;

      
      if (counter % 100 === 0 ) {
       coins += 10;
      //  localStorage.setItem('coins', ...)
      }
    }
    const increment =()=>{ 
        counter +=1
        toggleImage()
        if (counter >= 100){
          counter = 0
        }
    }

</script>



<div class="justify-center flex items-center flex-col  bg-cover h-screen bg-center  " style="
background-image: url({chichipop}); ">



  
  <div class="bg-white rounded-4xl text-4xl w-2xl h-[50px]">
  
  <div style="width: {counter}%;" class="bg-red-500 h-[50px] w-full rounded-4xl" ></div>
   <p>score = {counter}</p>
  </div>

  <a href="/"><button class="bg-red-500 px-10 py-3 rounded-xl text-white font-bold text-2xl absolute left-0 bottom-0 cursor-pointer m-10">Exit</button></a>


<!-- 
<style>
.box  {
  position:clearInterval;
  background-color:white;
  padding:10px;
  border-radius:50px;
  font-size:50px;
  width: 
}
</style> -->



  
  <div  class="cursor-pointer absolute bottom-0">
    <img class="h-[400px] w-[400px]" alt=""  src ='{images[currentIndex]}'  onclick={increment}/>
  </div>
  <!-- <a href="/"  >
      <button>กลับ</button></a> -->
</div>


