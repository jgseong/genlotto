<script>
	let pivotNumbers = [];
  let extractedNumbers = [];

  function extractNumbers() {
    let numbers = Array.from({ length: 45 }, (_, i) => i + 1);
    for (let i = 0; i < 5; i++) {
      let randomIndex = Math.floor(Math.random() * numbers.length);
      pivotNumbers = [...pivotNumbers, numbers[randomIndex]];
      numbers.splice(randomIndex, 1);
    }
		for (let i = 1; i <= 45; i++) {
			let tmpNumbers = [...pivotNumbers];
			if (tmpNumbers.includes(i)) {
				continue;
			}
			tmpNumbers = [...tmpNumbers, i];
			tmpNumbers = tmpNumbers.sort((a, b) => a - b);
			console.log(tmpNumbers);
			extractedNumbers = [...extractedNumbers, tmpNumbers];
		}
  }
</script>

<main>
  <h1>Random Number Extractor</h1>
  <button on:click={extractNumbers}>Extract Numbers</button>

  {#if extractedNumbers.length > 0}
    <h2>Extracted Numbers</h2>
    <ul>
      {#each extractedNumbers as number}
        <li>{number.join(' ')}</li>
      {/each}
    </ul>
  {/if}
</main>

<style>
  ul {
    list-style: none;
    padding: 0;
  }

  li {
    margin: 0.5rem;
  }
</style>
