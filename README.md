
# Sapper WebGL Playground

Sapper + Svelte + Svelte/GL + ThreeJS + Tailwindcss
 
  

### Running the project

  
```bash

git clone https://github.com/yorgyetson/Sapper-WebGL-Playground.git playground

cd playground

npm install

npm run dev

```

  

Open up [localhost:3000](http://localhost:3000) and start clicking around.

  

[svelte.dev](https://svelte.dev)

[sapper.svelte.dev](https://sapper.svelte.dev)

[https://github.com/sveltejs/gl](https://github.com/sveltejs/gl)

[https://tailwindcss.com/docs/](https://tailwindcss.com/docs/)

[https://threejs.org](https://threejs.org)


  ## Known issues
  
  - SvelteGL Equirectangular Pano viewer does not wrap the texture the same as the ThreeJS component.
  - Background Transparency on sveltegl components doesn't seem to work
  - SvelteGL Scene uses the class name of `container` and TailwindCSS adds a max-width to `container`. I've disabled the `container` class inside of tailwind.config.js as a temporary fix.
 