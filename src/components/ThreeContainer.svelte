<script>
  import * as THREE from "three";
  import { onMount } from "svelte";

  let content;

  export let width = window.innerWidth;
  export let height = window.innerHeight;
  export let boxColor = "#ffffff";
  export let image;

  onMount(() => {
    var scene = new THREE.Scene();
    var camera = new THREE.PerspectiveCamera(75, width / height, 0.1, 1000);

    var renderer = new THREE.WebGLRenderer({ alpha: true });
    renderer.setSize(width, height);

    content.appendChild(renderer.domElement);

    var geometry = new THREE.BoxGeometry();
    var material = new THREE.MeshBasicMaterial();
    material.color.setStyle(boxColor);
    var cube = new THREE.Mesh(geometry, material);
    scene.add(cube);

    var texture = new THREE.TextureLoader().load(image);

    // var geometry = new THREE.BoxBufferGeometry( 200, 200, 200 );
    // var	mesh = new THREE.Mesh( geometry, material );
    var geometry = new THREE.SphereGeometry(3, 50, 50, 0);
    var material = new THREE.MeshBasicMaterial({ map: texture });
    // var material = new THREE.MeshNormalMaterial();
    var cube = new THREE.Mesh(geometry, material);
    scene.add(cube);

    camera.position.z = 5;

    var animate = function() {
      requestAnimationFrame(animate);

      //   cube.rotation.x += 0.01;
      cube.rotation.y += 0.002;
      renderer.setClearColor( 0x000000, 0 );
      renderer.render(scene, camera);
    };

    animate();
  });
</script>

<style>
  .content {
    padding: 10px;
  }
</style>

<div bind:this={content} class="content" />
