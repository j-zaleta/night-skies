<script>
  import { onMount } from "svelte";
  import Confetti from "js-confetti";

  const spaceEmojis = [
    "🪐",
    "🔭",
    "👽",
    "🛸",
    "✨",
    "🌎",
    "🌌",
    "🌞",
    "🌝",
    "🚀",
  ];

  /**
   * @type {Confetti | null}
   */
  let confetti;

  function launchConfetti() {
    confetti?.addConfetti({ emojis: spaceEmojis });
  }

  onMount(() => {
    confetti = new Confetti();

    return () => {
      confetti = null;
    };
  });
</script>

<div class="w-full h-full items-center">
  <button
    on:click={launchConfetti}
    class="fixed top-4 right-4 px-2 py-1 text-sm font-medium text-black bg-white border border-white rounded-md cursor-pointer"
  >
    Launch confetti 🎉
  </button>
</div>
