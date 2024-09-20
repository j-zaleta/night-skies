<script>
  import { Canvas } from "@threlte/core";
  import Scene from "$lib/components/scene.svelte";

  import Music from "$lib/components/music.svelte";
  import Confetti from "$lib/components/confetti.svelte";
  import Starfield from "$lib/components/starfield.svelte";
  import Javi from "$lib/components/javi.svelte";
  import Footer from "$lib/components/footer.svelte";
</script>

<div style="width: 100vw; height: 100vh;">
  <Canvas>
    <Scene />
  </Canvas>
</div>

<Music />
<Confetti />
<Starfield />
<Javi />
<Footer />
