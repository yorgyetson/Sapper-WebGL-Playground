<script>
	export let segment;
</script>

<style>
	
</style>

<nav class="flex justify-between items-center bg-blue-400 py-4 px-2">
<div>logo</div>
	<ul class="flex">
		<li class="p-2"><a aria-current="{segment === undefined ? 'page' : undefined}" href=".">Svelte GL</a></li>
		<li class="p-2"><a aria-current="{segment === 'three' ? 'page' : undefined}" href="three">ThreeJS</a></li>

		<!-- for the blog link, we're using rel=prefetch so that Sapper prefetches
		     the blog data when we hover over the link or tap it on a touchscreen -->
		<!-- <li><a rel=prefetch aria-current="{segment === 'blog' ? 'page' : undefined}" href="blog">blog</a></li> -->
	</ul>
</nav>
