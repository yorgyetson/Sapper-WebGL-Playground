
# Sapper WebGL Playground

Sapper + Svelte + Svelte/GL + ThreeJS + Tailwindcss
 
## Demo 
[Click Here](https://stoic-volhard-3f59ef.netlify.app/)

### Running the project

  
```bash

git clone https://github.com/yorgyetson/Sapper-WebGL-Playground.git playground
cd playground
npm install
npm run dev

```

  

Open up [localhost:3000](http://localhost:3000) and start clicking around.

  
### Resouces
  
- [svelte.dev](https://svelte.dev)
- [sapper.svelte.dev](https://sapper.svelte.dev)
- [https://github.com/sveltejs/gl](https://github.com/sveltejs/gl)
- [https://tailwindcss.com/docs/](https://tailwindcss.com/docs/)
- [https://threejs.org](https://threejs.org)


### Other Info
This uses [GLSLify](https://github.com/glslify/glslify) in the rollup config. I just picked the first GLSL loader plugin I found, there might be a better alternative.
  
  
### Known issues
  - This is not at all mobile optimized.
  - SvelteGL Equirectangular Pano viewer does not wrap the texture the same as the ThreeJS component.
  - Background Transparency on sveltegl components doesn't seem to work
  - SvelteGL Scene uses the class name of `container` and TailwindCSS adds a max-width to `container`. I've disabled the `container` class inside of tailwind.config.js as a temporary fix.
 
 #### Why is ThreeJS in here?
 There are a lot of great examples of cool things ThreeJS can do that may or may not be possible with SvelteGL in its current state. The goal here is to identify the differences and/or limitations of SvelteGL in order to make it more robust. I've also found that working backwards from an existing ThreeJS example is helpful to figure out how to make things happen with SvelteGL.