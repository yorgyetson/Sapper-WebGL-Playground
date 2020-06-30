<script>
  import PhotoSphere from '../components/PhotoSphere.svelte';

</script>

<svelte:head>
	<title>Sapper project template</title>
</svelte:head>

<div class="flex justify-center bg-gray-400">
<h1>Great success!</h1>
</div>

<p></p>
<div class="flex justify-center">
 <PhotoSphere width={500} height={500} image="pano1.jpg"/> 
 <PhotoSphere width={500} height={500} image="pano2.jpg"/> 
 <PhotoSphere width={500} height={500} image="pano3.jpg"/> 
 </div>
<div class="flex justify-center">
 <PhotoSphere width={500} height={500} image="pano4.jpg"/> 
 </div>