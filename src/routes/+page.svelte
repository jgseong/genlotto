<script>
  //import Tailwindcss from "$lib/tailwindcss.svelte";
  import { t, locale, locales } from '$lib/i18n.js';

  let pivotNumbers = [];
  let extractedNumbers = [];

  function extractNumbers() {
    pivotNumbers = [];
    extractedNumbers = [];
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

  $locale = 'ko';
</script>

<main>
  <p>
    <select bind:value={$locale}>
      {#each locales as l}
        <option value={l}>{l}</option>
      {/each}
    </select>
  </p>
  <h1 class="text-center text-base font-semibold leading-7 text-gray-900"
  >{$t('home.title')}</h1>
  <div class="text-center">
    <button class="bg-gray-900 text-white rounded-md px-3 py-2 text-sm font-medium"
      on:click={extractNumbers}
    >{$t('home.button')}</button>
  </div>
  {#if extractedNumbers.length > 0}
    <h2 class="mt-10 text-center text-2xl font-bold leading-9 tracking-tight text-gray-900"
    >{$t('home.outtitle')}</h2>
    <ul class='text-center'>
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
