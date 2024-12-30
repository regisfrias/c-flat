<script lang='ts'>
  import Slider from './Slider.svelte'
  let { colors = $bindable() } = $props()
</script>

<div class='sliders'>
  <Slider backgroundColor='cyan' range={{min: 0, max: 100}} bind:value={colors[0]} />
  <Slider backgroundColor='magenta' range={{min: 0, max: 100}} bind:value={colors[1]} />
  <Slider backgroundColor='yellow' range={{min: 0, max: 100}} bind:value={colors[2]} />
</div>

<style>
  .sliders {
    display: flex;
    flex-direction: column;
    gap: 1rem;
  }
</style>
