<script>
  import { onMount } from "svelte";
  import * as GL from "@sveltejs/gl";

  export let image = "https://i.imgur.com/LqMsOvc.jpg";
  let w = 1;
  let h = 1;
  let d = 1;

  const logo = new GL.Texture(image);

  const from_hex = hex => parseInt(hex.slice(1), 16);

  const light = {};
  const sphereData = {};

  sphereData.rotation =0;

  onMount(() => {
    let frame;

    const loop = () => {
      frame = requestAnimationFrame(loop);

      sphereData.rotation += 0.1
    };

    loop();

    return () => cancelAnimationFrame(frame);
  });
</script>

<GL.Scene>
  <GL.Target id="center" location={[0, 1, 0]} />

  <GL.OrbitControls let:location>
    <GL.PerspectiveCamera {location} lookAt="center" near={0.1} far={1000} />
  </GL.OrbitControls>

  <GL.AmbientLight intensity={1} />


  <GL.Mesh
    geometry={GL.sphere({ turns: 36, bands: 36 })}
    location={[0, 1, 0]}
    scale={2.5}
    rotation={[0,sphereData.rotation,0]}
    uniforms={{ color: 0x336644, alpha: 1, colormap: logo }}
    transparent />

</GL.Scene>
