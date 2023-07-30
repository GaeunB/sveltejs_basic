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

<!-- Select bindings -->
<script>
	let questions = [
		{
			id: 1,
			text: `Where did you go to school?`
		},
		{
			id: 2,
			text: `What is your mother's name?`
		},
		{
			id: 3,
			text: `What is another personal fact that an attacker could easily find with Google?`
		}
	];

	let selected; //걍 선언.

	let answer = '';

	function handleSubmit() {
		alert(
			`answered question ${selected.id} (${selected.text}) with "${answer}"`
		);
	}
</script>

<h2>Insecurity questions</h2>

<form on:submit|preventDefault={handleSubmit}>
	<select
		bind:value={selected}
		on:change={() => (answer = '')}
	>
		{#each questions as question}
			<option value={question}>
				{question.text}
			</option>
		{/each}
	</select>

	<input bind:value={answer} />

	<button disabled={!answer} type="submit">
		Submit
	</button>
</form>

<p>
	selected question {selected
		? selected.id
		: '[waiting...]'}
</p>

<!-- Group Binding -->
<script>
	let scoops = 1;
	let flavours = [];

	const formatter = new Intl.ListFormat('en', { style: 'long', type: 'conjunction' });
</script>

<h2>Size</h2>

{#each [1, 2, 3] as number}
	<label>
		<input
			type="radio"
			name="scoops"
			value={number}
		/>

		{number} {number === 1 ? 'scoop' : 'scoops'}
	</label>
{/each}

<h2>Flavours</h2>

{#each ['cookies and cream', 'mint choc chip', 'raspberry ripple'] as flavour}
	<label>
		<input
			type="checkbox"
			name="flavours"
			value={flavour}
		/>

		{flavour}
	</label>
{/each}

{#if flavours.length === 0}
	<p>Please select at least one flavour</p>
{:else if flavours.length > scoops}
	<p>Can't order more flavours than scoops!</p>
{:else}
	<p>
		You ordered {scoops} {scoops === 1 ? 'scoop' : 'scoops'}
		of {formatter.format(flavours)}
	</p>
{/if}

<!-- CRUD -->
<!-- https://eugenkiss.github.io/7guis/tasks#crud -->

<script>
	let people = [
		{ first: 'Hans', last: 'Emil' },
		{ first: 'Max', last: 'Mustermann' },
		{ first: 'Roman', last: 'Tisch' }
	];

	let prefix = '';
	let first = '';
	let last = '';
	let i = 0;

	$: filteredPeople = prefix
		? people.filter((person) => {
				const name = `${person.last}, ${person.first}`;
				return name.toLowerCase().startsWith(prefix.toLowerCase());
		  })
		: people;

	$: selected = filteredPeople[i];

	$: reset_inputs(selected);

	function create() {
		people = people.concat({ first, last });
		i = people.length - 1;
		first = last = '';
	}

	function update() {
		selected.first = first;
		selected.last = last;
		people = people;
	}

	function remove() {
		// Remove selected person from the source array (people), not the filtered array
		const index = people.indexOf(selected);
		people = [...people.slice(0, index), ...people.slice(index + 1)];

		first = last = '';
		i = Math.min(i, filteredPeople.length - 2);
	}

	function reset_inputs(person) {
		first = person ? person.first : '';
		last = person ? person.last : '';
	}
</script>

<input placeholder="filter prefix" bind:value={prefix} />

<select bind:value={i} size={5}>
	{#each filteredPeople as person, i}
		<option value={i}>{person.last}, {person.first}</option>
	{/each}
</select>

<label><input bind:value={first} placeholder="first" /></label>
<label><input bind:value={last} placeholder="last" /></label>

<div class="b
uttons">
	<button on:click={create} disabled={!first || !last}>create</button>
	<button on:click={update} disabled={!first || !last || !selected}>update</button>
	<button on:click={remove} disabled={!selected}>delete</button>
</div>

<style>
	* {
		font-family: inherit;
		font-size: inherit;
	}

	input {
		display: block;
		margin: 0 0 0.5em 0;
	}

	select {
		float: left;
		margin: 0 1em 1em 0;
		width: 14em;
	}

	.buttons {
		clear: both;
	}
</style>


