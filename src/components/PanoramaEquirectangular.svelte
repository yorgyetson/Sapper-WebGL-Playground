<script>
  import * as THREE from "three";
  import { onMount } from "svelte";

  let container;
  export let width;
  export let height;
  export let image;
  let isUserInteracting = false;

  let onPointerDownPointerX;
  let onPointerDownPointerY;

  let onPointerDownLon;
  let onPointerDownLat;

  onMount(() => {
    var camera, scene, renderer;

    var onMouseDownMouseX = 0,
      onMouseDownMouseY = 0,
      lon = 0,
      onMouseDownLon = 0,
      lat = 0,
      onMouseDownLat = 0,
      phi = 0,
      theta = 0;

    init();
    animate();

    function init() {
      var container, mesh;

      container = document.getElementById("container");

      camera = new THREE.PerspectiveCamera(75, width / height, 1, 1100);
      camera.target = new THREE.Vector3(0, 0, 0);

      scene = new THREE.Scene();

      var geometry = new THREE.SphereGeometry(500, 60, 40);
      geometry.scale(-1, 1, 1);

      var material = new THREE.MeshBasicMaterial({
        map: new THREE.TextureLoader().load(image)
      });

      mesh = new THREE.Mesh(geometry, material);

      scene.add(mesh);

      renderer = new THREE.WebGLRenderer();
      renderer.setPixelRatio(window.devicePixelRatio);
    //   renderer.setPixelRatio(1);
      renderer.setSize(width, height);
      container.appendChild(renderer.domElement);

      container.addEventListener("mousedown", onDocumentMouseDown, false);
      container.addEventListener("mousemove", onDocumentMouseMove, false);
      container.addEventListener("mouseup", onDocumentMouseUp, false);
      container.addEventListener("wheel", onDocumentMouseWheel, false);

      //

      container.addEventListener(
        "dragover",
        function(event) {
          event.preventDefault();
          event.dataTransfer.dropEffect = "copy";
        },
        false
      );

      container.addEventListener(
        "dragenter",
        function(event) {
          document.body.style.opacity = 0.5;
        },
        false
      );

      container.addEventListener(
        "dragleave",
        function(event) {
          document.body.style.opacity = 1;
        },
        false
      );

      container.addEventListener(
        "drop",
        function(event) {
          event.preventDefault();

          var reader = new FileReader();
          reader.addEventListener(
            "load",
            function(event) {
              material.map.image.src = event.target.result;
              material.map.needsUpdate = true;
            },
            false
          );
          reader.readAsDataURL(event.dataTransfer.files[0]);

          document.body.style.opacity = 1;
        },
        false
      );

      container.addEventListener("resize", onWindowResize, false)
    }

    function onWindowResize() {
      camera.aspect = width / height;
      camera.updateProjectionMatrix();

      renderer.setSize(width, height);
    }

    function onDocumentMouseDown(event) {
      event.preventDefault();

      isUserInteracting = true;

      onPointerDownPointerX = event.clientX;
      onPointerDownPointerY = event.clientY;

      onPointerDownLon = lon;
      onPointerDownLat = lat;
    }

    function onDocumentMouseMove(event) {
      if (isUserInteracting === true) {
        lon = (onPointerDownPointerX - event.clientX) * 0.1 + onPointerDownLon;
        lat = (event.clientY - onPointerDownPointerY) * 0.1 + onPointerDownLat;
      }
    }

    function onDocumentMouseUp(event) {
      isUserInteracting = false;
    }

    function onDocumentMouseWheel(event) {
      camera.fov += event.deltaY * 0.05;
      camera.updateProjectionMatrix();
    }

    function animate() {
      requestAnimationFrame(animate);
      update();
    }

    function update() {
      if (isUserInteracting === false) {
        lon += 0.1;
      }

      lat = Math.max(-85, Math.min(85, lat));
      phi = THREE.Math.degToRad(90 - lat);
      theta = THREE.Math.degToRad(lon);

      camera.target.x = 500 * Math.sin(phi) * Math.cos(theta);
      camera.target.y = 500 * Math.cos(phi);
      camera.target.z = 500 * Math.sin(phi) * Math.sin(theta);

      camera.lookAt(camera.target);

      /*
				// distortion
				camera.position.copy( camera.target ).negate();
				*/

      renderer.render(scene, camera);
    }
  });
</script>

<style>
  body {
    background-color: #000000;
    margin: 0px;
    overflow: hidden;
  }

  #info {
    position: absolute;
    top: 0px;
    width: 100%;
    color: #ffffff;
    padding: 5px;
    font-family: Monospace;
    font-size: 13px;
    font-weight: bold;
    text-align: center;
  }

  a {
    color: #ffffff;
  }
</style>

<meta charset="utf-8" />
<meta
  name="viewport"
  content="width=device-width, user-scalable=no, minimum-scale=1.0,
  maximum-scale=1.0" />

<div id="container" class="rounded-lg" bind:this={container} />
<div id="info">
  <a href="https://threejs.org" target="_blank">three.js webgl</a>
  - equirectangular panorama demo. photo by
  <a
    href="http://www.flickr.com/photos/jonragnarsson/2294472375/"
    target="_blank">
    Jón Ragnarsson
  </a>
  .
  <br />
  drag equirectangular texture into the page.
</div>
