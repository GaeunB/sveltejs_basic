<!-- Reactivity -->
<script>
  <button on:click={increment}>
    Clicked {count}
    {count===1 ? 'time':'times'}
  </button>

  function increment() {
    count+=1;
  }
</script>

<!-- Declarations -->

let count=0;
$: doubled=count*2;

<button>

</button>
<p> {count}doubled is {doubled}</p>



let count=0;
$: console.log(`the count is ${count}`);


$: {
  console.log(`the count is ${count}`);
  console.log(`the will also be logged whenever count changes`);
}

<!-- Updating arrays and objects -->
<script>

 numbers=[numbers,numbers.length+1]; //걍 바로 추가하네 

  function addNumber() {
    numbers[numbers.length]=numbers.length+1; //걍 선언하는 거 없이 바로 추가하는 느낌
  }
</script>

<!-- Props -->

  <!-- Declaring props -->
<script>
  export let answer;
</script>

<!-- Binding -->
<script>
	let name=''
	let a=1;
	let b=3
</script>
<main>
<input bind:value={name}/>
<p>'{name}'</p>
<label>
	<input type='number' bind:value={a} min="0" max="10"/>
	<input type='range' bind:value={a} min="0" max="10"/>
</label>

<label>
	<input type="number" bind:value={b} min="0" max="10"/>
	<input type="range" bind:value={b} min="0" max="10"/>
</label>
</main>



