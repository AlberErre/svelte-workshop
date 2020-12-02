<script lang="ts">
  // Copy and paste this code into https://svelte.dev/repl
  //
  // Requirements:
  // 1. Filling an input should select the next input
  // 2. Focusing an input should select its content
  // 3. Pressing backspace should focus and select the contents of the previous input
  // 4. Pasting the code in the first input should paste each digit in the correct input
  // 5. Auto submit the form if all fields are filled after a paste

  let typehead;
  let activeOption;

  let showList = false;

  const countries = ["Spain", "France"];

  let text = "";

  $: filteredCountries = countries.filter(
    (country) => text && country.toLowerCase().includes(text.toLowerCase())
  );
</script>

<style>
  * {
    box-sizing: border-box;
  }
</style>

<div
  bind:this={typehead}
  class="typehead"
  role="combobox"
  aria-haspopup
  aria-owns="countryList"
  aria-expanded={showList}>
  <input
    bind:value={text}
    type="text"
    name="Country"
    aria-autocomplete="list"
    aria-controls="countryList"
    aria-activedescendant={activeOption} />

  <ul id="countryList" aria-labelledby="countryList" role="listbox">
    {#each filteredCountries as country, i}
      <li role="option" aria-selected="false">{country}</li>
    {/each}
  </ul>
</div>
