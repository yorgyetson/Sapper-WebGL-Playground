<script>
  import PanoramaEquirectangular from '../components/PanoramaEquirectangular.svelte';
</script>

<svelte:head>
	<title>About</title>
</svelte:head>

<h1>About this site</h1>

<p>This is the 'about' page. There's not much here.</p>
<div class="flex w-full flex-wrap justify-center">
<PanoramaEquirectangular width={500} height={250} image="pano1.jpg"/>
<PanoramaEquirectangular width={500} height={250} image="pano2.jpg"/>
<PanoramaEquirectangular width={500} height={250} image="pano3.jpg"/>
<PanoramaEquirectangular width={500} height={250} image="pano4.jpg"/>
</div>