<script lang='ts'>
  let {
    backgroundColor,
    range,
    value = $bindable(),
  } = $props()

  const onUpdateColorPercentage = (event: Event) => {
    const target = event.target as HTMLInputElement
    if (target) {
      value = target.valueAsNumber
    }
  }
</script>

<div class={`label ${backgroundColor}`} style={`--background_color: ${backgroundColor}`}>
  <input bind:value={value} type='range' name={backgroundColor} id={backgroundColor} min={range.min} max={range.max} step={1}>
  <input type="number" name="" id="" min="0" max="100" onchange={onUpdateColorPercentage} onkeyup
  ={onUpdateColorPercentage} value={value}>
</div>

<style>
  .label {
    position: relative;
    display: grid;
    gap: 1rem;
    grid-template-columns: 1fr 50px;
  }

  .labelText {
    display: block;
  }

  input {
    background-color: transparent;
  }

  input[type=number] {
    color: black;
    border: 0;
    background-color: white;
  }

  input[type=range] {
    height: 30px;
    appearance: none;
    -webkit-appearance: none;
    margin: 0;
    width: 100%;
  }
  input[type=range]:focus {
    outline: none;
  }
  input[type=range]::-webkit-slider-runnable-track {
    width: 100%;
    height: 30px;
    cursor: pointer;
    background: var(--background_color);
    border-radius: 50px;
    border: 0;
  }
  input[type=range]::-webkit-slider-thumb {
    border: 0;
    height: 30px;
    width: 30px;
    border-radius: 30px;
    background: #000000;
    cursor: pointer;
    -webkit-appearance: none;
    margin-top: -1px;
  }
  input[type=range]:focus::-webkit-slider-runnable-track {
    background: var(--background_color);
  }
  input[type=range]::-moz-range-track {
    width: 100%;
    height: 30px;
    cursor: pointer;
    background: var(--background_color);
    border-radius: 50px;
    border: 0;
  }
  input[type=range]::-moz-range-thumb {
    border: 0;
    height: 30px;
    width: 30px;
    border-radius: 30px;
    background: #000000;
    cursor: pointer;
  }
  input[type=range]::-ms-track {
    width: 100%;
    height: 30px;
    cursor: pointer;
    background: transparent;
    border-color: transparent;
    color: transparent;
  }
  input[type=range]::-ms-fill-lower {
    background: var(--background_color);
    border: 0;
    border-radius: 100px;
  }
  input[type=range]::-ms-fill-upper {
    background: var(--background_color);
    border: 0;
    border-radius: 100px;
  }
  input[type=range]::-ms-thumb {
    margin-top: 1px;
    border: 0;
    height: 30px;
    width: 30px;
    border-radius: 30px;
    background: #000000;
    cursor: pointer;
  }
  input[type=range]:focus::-ms-fill-lower {
    background: var(--background_color);
  }
  input[type=range]:focus::-ms-fill-upper {
    background: var(--background_color);
  }

</style>