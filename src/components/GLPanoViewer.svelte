<script>
  import { onMount } from "svelte";
  import * as GL from "@sveltejs/gl";

  export let image;
  let w = 1;
  let h = 1;
  let d = 1;

  const logo = new GL.Texture(image);

  const from_hex = hex => parseInt(hex.slice(1), 16);

  const light = {};
  const sphereData = {};

  sphereData.rotation = 0;
  sphereData.speed = 0.1;

  onMount(() => {
    let frame;

    const loop = () => {
      frame = requestAnimationFrame(loop);

      sphereData.rotation += sphereData.speed;
    };

    loop();

    return () => cancelAnimationFrame(frame);
  });
  function onDocumentMouseEnter() {
    sphereData.speed = 0;
  }
  function onDocumentMouseLeave() {
    sphereData.speed = 0.1;
  }
</script>

<div
  on:mouseenter={onDocumentMouseEnter}
  on:mouseleave={onDocumentMouseLeave}>
  <GL.Scene backgroundOpacity={0}>
    <GL.Target id="center" location={[0, 1, 0]} />

    <GL.OrbitControls let:location minDistance={0} maxDistance={115}>
      <GL.PerspectiveCamera
        {location}
        fov={75}
        lookAt={[0, 1, 0]}
        near={0.001}
        far={1000} />
    </GL.OrbitControls>

    <GL.AmbientLight intensity={1} />

    <GL.Mesh
      geometry={GL.sphere({ turns: 36, bands: 36 })}
      location={[0, 1, 0]}
      scale={[-100, -100, -100]}
      rotation={[0, sphereData.rotation, 180]}
      uniforms={{ color: 0x336644, alpha: 1, colormap: logo }}
      transparent />
  </GL.Scene>
</div>
