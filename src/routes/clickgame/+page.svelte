<script>
    let counter =$state(0)
    let index = $state(0)

    const increment =()=>{
        counter +=1
        if (index === 0) {

        }
    }

 let images = [
    'https://img.freepik.com/free-vector/english-alphabets_1308-2901.jpg?semt=ais_hybrid&w=740&q=80',
    'https://m.media-amazon.com/images/I/71VdS8tkVNL.jpg'
  ];
  let currentIndex = 0;

  function toggleImage() {
    currentIndex = (currentIndex + 1) % images.length;
  }

</script>


<p>{counter}</p>


<button onclick={increment}> Tab </button>

<a href="#"  >
    <button> Go back to lobby</button></a>
