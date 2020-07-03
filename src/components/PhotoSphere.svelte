<script>
  import * as THREE from "three";
  import { onMount } from "svelte";

  export let width = window.innerWidth;
  export let height = window.innerHeight;
  export let image;

  let content;

  let scene = new THREE.Scene();
  let camera = new THREE.PerspectiveCamera(75, width / height, 0.1, 1000);

  onMount(() => {
    let renderer = new THREE.WebGLRenderer({ alpha: true });
    renderer.setSize(width, height);

    content.appendChild(renderer.domElement);

    let texture = new THREE.TextureLoader().load(image);
    let geometry = new THREE.SphereGeometry(3, 50, 50, 0);
    let material = new THREE.MeshBasicMaterial({ map: texture });
    let sphere = new THREE.Mesh(geometry, material);
    scene.add(sphere);

    camera.position.z = 5;

    let animate = function() {
      requestAnimationFrame(animate);

    //   sphere.rotation.x += 0.0005;
      sphere.rotation.y -= 0.01;
      renderer.render(scene, camera);
    };

    animate();
  });
</script>

<div bind:this={content} />
