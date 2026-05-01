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

      
      if (counter %100 === 0 ) {
       coins += 10;
      }
    }
    const increment =()=>{ 
        counter +=1
        toggleImage() 
    }

</script>



<div class="justify-center flex items-center  bg-cover h-screen bg-center  " style="
background-image: url({chichipop}); ">


<div class="absolute bottom-0 ">
  
  <div class="box">
  <p>score = {counter}</p>
  
</div>



<style>
.box  {
  position:clearInterval;
  background-color:white;
  padding:10px;
  border-radius:50px;
  font-size:50px;
  

}
</style>



  
  <div  class="cursor-pointer">
    <img class="h-[400px] w-[400px]" alt=""  src ='{images[currentIndex]}'  onclick={increment}/>
  </div>
  <!-- <a href="/"  >
      <button>กลับ</button></a> -->
</div>



</div>