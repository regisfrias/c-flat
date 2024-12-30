<script lang='ts'>
    import Canvas from './lib/Canvas.svelte';
  import Circles from './lib/Circles.svelte'
  import Sliders from './lib/Sliders.svelte'

  const toRGB = (colors: number[]) => {
    const [c, m, y] = colors
    const r = 2.55 * (100 - c)
    const g = 2.55 * (100 - m)
    const b = 2.55 * (100 - y)

    return `rgb(${r}, ${g}, ${b})`
  }

  let colors: number[] = $state([100, 100, 100])
</script>

<main>
  <h1>Color mixer</h1>

  <div class='wrapper'>
    <div class='mixer'>
      <Circles {colors} />
      <Sliders bind:colors={colors} />
    </div>
  
    <Canvas color={toRGB(colors)} />
  </div>
</main>

<style>
  .wrapper {
    display: grid;
    gap: 2rem;
  }

  .mixer {
    display: flex;
    flex-direction: column;
    gap: 2rem;
  }

  @media (min-width: 800px) {
    .wrapper {
      grid-template-columns: 2fr 5fr;
      gap: 2rem;
    }
  }
</style>