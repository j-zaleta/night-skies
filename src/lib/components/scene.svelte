<script>
  import { T } from "@threlte/core";
  import { OrbitControls, Stars } from "@threlte/extras";
  import { onMount } from "svelte";

  /**
   * @typedef {import("three").Group & {
   *   rotation: { z: number }
   * }} CameraRef
   */

  /**
   * @type {CameraRef}
   */
  let camera;

  onMount(() => {
    if (camera) {
      const animate = () => {
        camera.rotation.z -= 0.001;
        requestAnimationFrame(animate);
      };

      animate();
    }
  });
</script>

<T.PerspectiveCamera
  makeDefault
  fov={75}
  position={[0, 0, 50]}
  on:create={({ ref }) => {
    ref.lookAt(0, 0, 0);
  }}
>
  <OrbitControls minDistance={8} maxDistance={150} />
</T.PerspectiveCamera>

<T.Group bind:ref={camera}>
  <!-- Look at the stars, look how they shine for you -->
  <Stars count={8000} factor={5} fade={true} speed={1} />
</T.Group>
