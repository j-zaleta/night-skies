<script>
  import { onMount } from "svelte";

  /** @type {HTMLCanvasElement} */
  let canvas;

  /** @type {ShootingStar|null} */
  let currentStar = null;

  const starProps = { size: 1.5, speed: 2, tailLength: 100 };

  function getRandomColor() {
    const stellarPalette = [
      "#aabfff",
      "#9bb0ff",
      "#cad7ff",
      "#fff4e8",
      "#f9ecb7",
      "#ffdab4",
      "#ffb074",
    ];
    return stellarPalette[Math.floor(Math.random() * stellarPalette.length)];
  }

  class ShootingStar {
    /**
     * @param {HTMLCanvasElement} canvas
     */
    constructor(canvas) {
      this.canvas = canvas;
      this.x = Math.random() * canvas.width;
      this.y = -starProps.size;
      this.angle = Math.PI * (0.25 + Math.random() * 0.5);
      this.color = getRandomColor();
    }

    /**
     * @param {CanvasRenderingContext2D} ctx
     */
    draw(ctx) {
      this.x += starProps.speed * Math.cos(this.angle);
      this.y += starProps.speed * Math.sin(this.angle);

      ctx.beginPath();
      ctx.arc(this.x, this.y, starProps.size, 0, 2 * Math.PI);
      ctx.fillStyle = this.color;
      ctx.fill();

      const [tailEndX, tailEndY] = [
        this.x - starProps.tailLength * Math.cos(this.angle),
        this.y - starProps.tailLength * Math.sin(this.angle),
      ];

      const gradient = ctx.createLinearGradient(
        this.x,
        this.y,
        tailEndX,
        tailEndY
      );
      gradient.addColorStop(0, this.color);
      gradient.addColorStop(1, "transparent");

      ctx.beginPath();
      ctx.moveTo(this.x, this.y);
      ctx.lineTo(tailEndX, tailEndY);
      ctx.strokeStyle = gradient;
      ctx.lineWidth = starProps.size * 2;
      ctx.stroke();
    }

    isOutOfBounds() {
      return this.y > this.canvas.height + starProps.tailLength;
    }
  }

  /**
   * @param {CanvasRenderingContext2D} ctx
   */
  function renderStar(ctx) {
    ctx.clearRect(0, 0, canvas.width, canvas.height);

    if (!currentStar || currentStar.isOutOfBounds()) {
      currentStar = new ShootingStar(canvas);
    }

    currentStar.draw(ctx);

    requestAnimationFrame(() => renderStar(ctx));
  }

  onMount(() => {
    const ctx = canvas.getContext("2d");
    if (!ctx) return;

    const resizeCanvas = () => {
      canvas.width = window.innerWidth;
      canvas.height = window.innerHeight;
    };

    resizeCanvas();

    window.addEventListener("resize", resizeCanvas);

    renderStar(ctx);

    return () => {
      window.removeEventListener("resize", resizeCanvas);
    };
  });
</script>

<canvas
  bind:this={canvas}
  id="starfield"
  style="display: block; position: absolute; top: 0; left: 0; width: 100%; height: 100%; pointer-events: none; z-index: -1;"
/>
