<script>
  import * as THREE from "three";
  import { onMount, beforeUpdate, afterUpdate } from "svelte";

  let container;
  export let width;
  export let height;
  export let image;

  export let rotateX = 0.1;

  let isUserInteracting = false;

  let onPointerDownPointerX;
  let onPointerDownPointerY;

  let onPointerDownLon;
  let onPointerDownLat;

  let camera, scene, renderer;

  let onMouseDownMouseX = 0,
    onMouseDownMouseY = 0,
    lon = 0,
    onMouseDownLon = 0,
    lat = 0,
    onMouseDownLat = 0,
    phi = 0,
    theta = 0;

  onMount(() => {
    console.log(container.getBoundingClientRect());
    width = width ? width : container.offsetWidth;
    width = container.offsetWidth;
    height = height ? height : width * 0.5625;
    // height = width * 0.5625
    init();
    animate();
  });

  function init() {
    let mesh;

    //   container = document.getElementById("container");

    camera = new THREE.PerspectiveCamera(75, width / height, 1, 1100);
    camera.target = new THREE.Vector3(0, 0, 0);

    scene = new THREE.Scene();

    let geometry = new THREE.SphereGeometry(500, 60, 40);
    geometry.scale(-1, 1, 1);

    let material = new THREE.MeshBasicMaterial({
      map: new THREE.TextureLoader().load(image)
    });

    mesh = new THREE.Mesh(geometry, material);

    scene.add(mesh);

    renderer = new THREE.WebGLRenderer();
    renderer.setPixelRatio(window.devicePixelRatio);
    renderer.setSize(width, height);
    container.appendChild(renderer.domElement);
  }

  function onWindowResize() {
    camera.aspect = width / height;
    camera.updateProjectionMatrix();

    renderer.setSize(width, height);
  }

  function onDocumentMouseEnter() {
    rotateX = 0;
  }
  function onDocumentMouseLeave() {
    rotateX = 0.1;
    isUserInteracting = false;
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
  function onDocumentDragOver(event) {
    event.preventDefault();
    event.dataTransfer.dropEffect = "copy";
  }
  function onDocumentDragEnter(event) {
    document.body.style.opacity = 0.5;
  }
  function onDocumentDragLeave(event) {
    document.body.style.opacity = 1;
  }

  function animate() {
    requestAnimationFrame(animate);
    update();
  }

  function update() {
    if (isUserInteracting === false) {
      lon += rotateX;
    }

    lat = Math.max(-85, Math.min(85, lat));
    phi = THREE.Math.degToRad(90 - lat);
    theta = THREE.Math.degToRad(lon);

    camera.target.x = 500 * Math.sin(phi) * Math.cos(theta);
    camera.target.y = 500 * Math.cos(phi);
    camera.target.z = 500 * Math.sin(phi) * Math.sin(theta);

    camera.lookAt(camera.target);

    // distortion
    // camera.position.copy( camera.target ).negate();

    renderer.render(scene, camera);
  }
</script>

<div
  bind:this={container}
  on:mousemove={onDocumentMouseMove}
  on:mousedown={onDocumentMouseDown}
  on:mouseup={onDocumentMouseUp}
  on:wheel={onDocumentMouseWheel}
  on:mouseenter={onDocumentMouseEnter}
  on:mouseleave={onDocumentMouseLeave}
  on:dragover={onDocumentDragOver}
  on:dragenter={onDocumentDragEnter}
  on:dragleave={onDocumentDragLeave}
  on:resize={onWindowResize} />
