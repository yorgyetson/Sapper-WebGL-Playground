<script>
  import { onMount } from "svelte";

  let BasicSvelteGL;

  onMount(async () => {
    const module = await import("../components/BasicSvelteGL.svelte");
    BasicSvelteGL = module.default;
  });
</script>

<svelte:head>
  <title>Svelte GL Basic REPL</title>
</svelte:head>

  <svelte:component this={BasicSvelteGL} />

