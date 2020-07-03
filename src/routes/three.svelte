<script>
  import PanoramaEquirectangular from "../components/PanoramaEquirectangular.svelte";
  import PhotoSphere from "../components/PhotoSphere.svelte";
</script>

<svelte:head>
  <title>ThreeJS Examples</title>
</svelte:head>


<div class="flex flex-wrap bg-blue-700 w-full">

  <div class=" w-1/2">
    <PanoramaEquirectangular image="pano3.jpg" />
  </div>
  <div class="flex justify-center items-center w-1/2">
    <PhotoSphere width={500} height={432} image="pano2.jpg" />
  </div>
</div>
<div class="flex w-full flex-wrap justify-center">
  <div class="w-1/4">
    <PanoramaEquirectangular width={500} height={250} image="pano1.jpg" />
  </div>
  <div class="w-1/4">
    <PanoramaEquirectangular width={500} height={250} image="pano2.jpg" />
  </div>
  <div class="w-1/4">
    <PanoramaEquirectangular width={500} height={250} image="pano3.jpg" />
  </div>
  <div class="w-1/4">
    <PanoramaEquirectangular width={500} height={250} image="pano4.jpg" />
  </div>
</div>
