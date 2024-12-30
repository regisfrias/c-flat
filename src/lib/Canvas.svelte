<script lang='ts'>
  import { onMount } from "svelte"
    import Slider from "./Slider.svelte";

  let { color } = $props()
  let lineWidth = $state(50)
  let radius = $derived(lineWidth / 2)
  let circleStroke = $derived(radius / 50 + 1)
  let drawing = false
  let canvas: HTMLCanvasElement
  let pMouse: {x: number | null, y: number | null} = { x: null, y: null }

  const draw = (ctx: CanvasRenderingContext2D, x1: number, y1: number, x2: number, y2: number, color: string) => {
    ctx.beginPath()
    ctx.moveTo(x1, y1)
    ctx.lineTo(x2, y2)
    ctx.strokeStyle = color
    ctx.lineWidth = lineWidth
    ctx.lineCap = 'round'
    ctx.stroke()
  }

  onMount(() => {
    canvas = document.querySelector('.canvas') as HTMLCanvasElement
    const ctx = canvas.getContext('2d')

    if (ctx) {
      canvas.width = canvas.clientWidth
      canvas.height = canvas.clientHeight
    }
  })
</script>

<div class="wrapper">
  <canvas
    class="canvas"
    style={
      `
        --cursor: url("data:image/svg+xml,%3Csvg width='100' height='100' viewBox='0 0 100 100' fill='none' xmlns='http://www.w3.org/2000/svg'%3E%3Ccircle cx='${radius + 1}' cy='${radius + 1}' r='${radius}' stroke-width='${circleStroke}' stroke='black'/%3E%3C/svg%3E%0A") ${radius} ${radius}, auto;
      `
    }
    onmousedown={() => drawing = true}
    onmouseup={() => {
      drawing = false
      pMouse = { x: null, y: null }
    }}
    onmousemove={(e) => {
      if (drawing) {
        const ctx = canvas.getContext('2d')
        const { offsetX, offsetY } = e
  
        if (ctx) {
          if (pMouse.x !== null && pMouse.y !== null) {
            draw(ctx, offsetX, offsetY, pMouse.x, pMouse.y, color)
          }
          pMouse = { x: offsetX, y: offsetY }
        }
      }
    }}
  ></canvas>
  <div class="controls">
    <div class="brushSize">
      <div class="slider">
        <Slider backgroundColor='white' range={{min: 1, max: 100}} bind:value={lineWidth} />
      </div>
    </div>
    <button onclick={() => {
      const ctx = canvas.getContext('2d')
      if (ctx) {
        ctx.clearRect(0, 0, canvas.width, canvas.height)
      }
    }}>Clear</button>
  </div>
</div>

<style>
  .wrapper {
    display: grid;
    gap: 2rem;
  }

  .canvas {
    width: 60vw;
    height: 35vw;
    background-color: white;
    cursor: var(--cursor);
  }
  
  .brushSize {
    flex-grow: 1;
    display: flex;
    gap: 1rem;
  }

  .slider {
    width: 100%;
  }

  .controls {
    display: flex;
    gap: 1rem;
  }
</style>
