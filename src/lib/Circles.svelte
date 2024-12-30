<script lang='ts'>
  let { colors } = $props()
  let compose = $state(false)
</script>

<div class="circles">
  <div class={`circle cyan ${compose ? 'compose' : ''}`} style={`opacity: ${colors[0] / 100}`}></div>
  <div class={`circle magenta ${compose ? 'compose' : ''}`} style={`opacity: ${colors[1] / 100}`}></div>
  <div class={`circle yellow ${compose ? 'compose' : ''}`} style={`opacity: ${colors[2] / 100}`}></div>
</div>

<label>
  <input type="checkbox" name="" id="" bind:checked={compose}>
  Mix colors
</label>

<style>
  .circles {
    display: flex;
    width: 100%;
    height: 0;
    padding-top: 100%;
    position: relative;
    background-color: white;
  }

  .circle {
    border-radius: 50%;
    width: 30%;
    height: 30%;
    position: absolute;
    left: 35%;
    top: 35%;
    mix-blend-mode: multiply;
    transition: transform 0.25s;
    transform: rotate(0deg) translate(80%, 0);
  }

  .cyan {
    background-color: cyan;
    transform: rotate(0deg) translate(80%, 0);
  }
  .magenta {
    background-color: magenta;
    transform: rotate(120deg) translate(80%, 0);
  }
  .yellow {
    background-color: yellow;
    transform: rotate(240deg) translate(80%, 0);
  }

  .compose {
    transform: rotate(0) translate(0, 0);
  }
</style>