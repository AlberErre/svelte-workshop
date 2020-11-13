<script>
  // Copy and paste this code into https://svelte.dev/repl
  //
  // Requirements:
  // 1. Filling an input should select the next input
  // 2. Focusing an input should select its content
  // 3. Pressing backspace should focus and select the contents of the previous input
  // 4. Pasting the code in the first input should paste each digit in the correct input
  // 5. Auto submit the form if all fields are filled after a paste

  let form;

  const handleFormKeydown = (event) => {
    if (event.code === "Backspace") {
      event.preventDefault();
      event.target.value = "";

      const previousInput = document.activeElement.previousElementSibling;
      if (previousInput) previousInput.focus();
    }
  };

  const handleInput = (event) => {
    const nextInput = event.target.nextElementSibling;

    if (!nextInput) return;

    nextInput.focus();
  };

  const handleFocus = (event) => {
    event.target.select();
  };

  const populateInputs = (input, values) => {
    if (values.length === 0) return;

    input.value = values[0];

    const nextInput = input.nextElementSibling;
    if (!nextInput) {
      form.submit();
      return;
    }

    populateInputs(nextInput, values.slice(1));
  };

  const handlePaste = (event) => {
    const nextInput = event.target.nextElementSibling;
    const pastedValues = event.clipboardData.getData("Text").split("");
    populateInputs(nextInput, pastedValues.slice(1));
  };

  const inputs = ["n1", "n2", "n3", "n4", "n5", "n6"];
</script>

<style>
  * {
    box-sizing: border-box;
  }
  form {
    border: 1px solid black;
    padding: 20px;
    width: 500px;
  }
  .inputs {
    display: grid;
    gap: 10px;
    grid-template-columns: repeat(6, 1fr);
    margin-bottom: 10px;
  }
  .inputs > * {
    border: 1px solid black;
    width: 100%;
    padding: 20px;
    text-align: center;
    font-size: 20px;
    line-height: 1;
  }
  button {
    border: 1px solid black;
    line-height: 1;
    background: black;
    color: white;
    font-size: 20px;
    padding: 20px;
    width: 100%;
    text-align: center;
  }
  button:focus {
    border-color: blue;
  }
</style>

<form bind:this={form} on:keydown={handleFormKeydown}>
  <div class="inputs">
    {#each inputs as inputName, index}
      <input
        type="text"
        name={inputName}
        maxlength="1"
        on:paste={index === 0 ? handlePaste : undefined}
        on:input={handleInput}
        on:focus={handleFocus} />
    {/each}
  </div>

  <button type="submit">Verify</button>
</form>
