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

  const BACKSPACE_KEYCODE = 8;

  function handleKeydown(event) {
    const previousInput = document.activeElement.previousElementSibling;

    if (event.keyCode === BACKSPACE_KEYCODE) {
      event.preventDefault();

      event.target.value = "";
      if (previousInput) previousInput.focus();
    }
  }

  function handleInput(event) {
    const nextInput = event.target.nextElementSibling;

    if (!nextInput) {
      form.submit();
      return;
    }

    nextInput.focus();
  }

  function handleFocus(event) {
    event.target.select();
  }
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

<svelte:window on:keydown={handleKeydown} />

<form bind:this={form}>
  <div class="inputs">
    <input
      type="text"
      name="n1"
      maxlength="1"
      on:input={handleInput}
      on:focus={handleFocus} />
    <input
      type="text"
      name="n2"
      maxlength="1"
      on:input={handleInput}
      on:focus={handleFocus} />
    <input
      type="text"
      name="n3"
      maxlength="1"
      on:input={handleInput}
      on:focus={handleFocus} />
    <input
      type="text"
      name="n4"
      maxlength="1"
      on:input={handleInput}
      on:focus={handleFocus} />
    <input
      type="text"
      name="n5"
      maxlength="1"
      on:input={handleInput}
      on:focus={handleFocus} />
    <input
      type="text"
      name="n6"
      maxlength="1"
      on:input={handleInput}
      on:focus={handleFocus} />
  </div>
  <button type="submit">Verify</button>
</form>
