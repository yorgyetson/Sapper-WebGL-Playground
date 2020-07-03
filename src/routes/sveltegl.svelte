<script>
  import { onMount } from "svelte";

  let GLPanoViewer;
  let GLPanoSphere;

  onMount(async () => {
    const GLPanoViewerModule = await import(
      "../components/GLPanoViewer.svelte"
    );
    GLPanoViewer = GLPanoViewerModule.default;
    const GLPanoSphereModule = await import(
      "../components/GLPanoSphere.svelte"
    );
    GLPanoSphere = GLPanoSphereModule.default;
  });
</script>

<svelte:head>
  <title>Svelte GL Examples</title>
</svelte:head>

<div class="flex w-full bg-gray-500">
  <div class="w-full">
    <svelte:component this={GLPanoViewer} image="pano2.jpg" />
  </div>
  <div class="w-full">
    <svelte:component this={GLPanoSphere} image="pano3.jpg" />
  </div>
</div>
<div class="flex">
<div class="w-full">
    <svelte:component this={GLPanoViewer} image="pano1.jpg" />
  </div>
<div class="w-full">
    <svelte:component this={GLPanoViewer} image="pano2.jpg" />
  </div>
<div class="w-full">
    <svelte:component this={GLPanoViewer} image="pano3.jpg" />
  </div>
<div class="w-full">
    <svelte:component this={GLPanoViewer} image="pano4.jpg" />
  </div>
</div>

