<script lang="ts">
  import { onMount } from 'svelte';
  import * as THREE from 'three';
  import { GLTFLoader } from 'three/examples/jsm/loaders/GLTFLoader.js';
  import { OrbitControls } from 'three/examples/jsm/controls/OrbitControls.js';

  let container: HTMLElement;
  let loadingProgress = 0;
  
  onMount(() => {
    // Scene setup
    const scene = new THREE.Scene();
    scene.background = new THREE.Color('#111111');

    // Camera setup
    const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
    camera.position.set(3, 3, 3); // Adjusted camera position

    // Renderer setup
    const renderer = new THREE.WebGLRenderer({ antialias: true });
    renderer.setSize(container.clientWidth, container.clientHeight);
    renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));
    renderer.shadowMap.enabled = true;
    renderer.shadowMap.type = THREE.PCFSoftShadowMap;
    container.appendChild(renderer.domElement);

    // Lighting
    const ambientLight = new THREE.AmbientLight(0xffffff, 0.5);
    scene.add(ambientLight);

    const mainLight = new THREE.DirectionalLight(0xffffff, 1);
    mainLight.position.set(5, 5, 5);
    mainLight.castShadow = true;
    mainLight.shadow.mapSize.width = 2048;
    mainLight.shadow.mapSize.height = 2048;
    scene.add(mainLight);

    // Animated point lights
    const pointLight1 = new THREE.PointLight(0x049ef4, 2);
    const pointLight2 = new THREE.PointLight(0xff0066, 2);
    scene.add(pointLight1);
    scene.add(pointLight2);

    // Controls
    const controls = new OrbitControls(camera, renderer.domElement);
    controls.enableDamping = true;
    controls.dampingFactor = 0.05;
    controls.screenSpacePanning = false;
    controls.minDistance = 2;
    controls.maxDistance = 5;
    controls.maxPolarAngle = Math.PI / 2;
    controls.target.set(0, 0.5, 0);

    // Loading manager
    const manager = new THREE.LoadingManager();
    manager.onProgress = (url, itemsLoaded, itemsTotal) => {
      loadingProgress = (itemsLoaded / itemsTotal) * 100;
    };

    // GLTF Loader
    const loader = new GLTFLoader(manager);
    let model: THREE.Group;
    let mixer: THREE.AnimationMixer;

    // Load the model
    loader.load(
      '/models/voxel_dog.glb',
      (gltf) => {
        model = gltf.scene;
        model.scale.set(0.5, 0.5, 0.5); // Reduced scale
        model.position.set(0, 0, 0);
        
        // Setup animations if they exist
        if (gltf.animations && gltf.animations.length) {
          mixer = new THREE.AnimationMixer(model);
          const action = mixer.clipAction(gltf.animations[0]);
          action.play();
        }

        model.traverse((child) => {
          if (child instanceof THREE.Mesh) {
            child.castShadow = true;
            child.receiveShadow = true;
          }
        });
        scene.add(model);
      },
      (progress) => {
        console.log('Loading model...', (progress.loaded / progress.total) * 100, '%');
      },
      (error) => {
        console.error('Error loading model:', error);
      }
    );

    // Ground plane
    const groundGeometry = new THREE.CircleGeometry(2, 32);
    const groundMaterial = new THREE.MeshStandardMaterial({ 
      color: 0x111111,
      roughness: 0.8,
      metalness: 0.2
    });
    const ground = new THREE.Mesh(groundGeometry, groundMaterial);
    ground.rotation.x = -Math.PI / 2;
    ground.position.y = -0.001;
    ground.receiveShadow = true;
    scene.add(ground);

    // Clock for animations
    const clock = new THREE.Clock();

    // Animation loop
    function animate() {
      requestAnimationFrame(animate);
      
      const delta = clock.getDelta();

      if (mixer) {
        mixer.update(delta);
      }

      if (model) {
        model.rotation.y += 0.005;
      }

      // Animate point lights in a circle
      const time = Date.now() * 0.001;
      pointLight1.position.x = Math.sin(time) * 2;
      pointLight1.position.z = Math.cos(time) * 2;
      pointLight1.position.y = 2;
      
      pointLight2.position.x = Math.sin(time + Math.PI) * 2;
      pointLight2.position.z = Math.cos(time + Math.PI) * 2;
      pointLight2.position.y = 2;

      controls.update();
      renderer.render(scene, camera);
    }

    // Handle container resize
    function handleResize() {
      const width = container.clientWidth;
      const height = container.clientHeight;

      camera.aspect = width / height;
      camera.updateProjectionMatrix();
      renderer.setSize(width, height);
    }

    const resizeObserver = new ResizeObserver(handleResize);
    resizeObserver.observe(container);

    animate();

    return () => {
      resizeObserver.disconnect();
      container.removeChild(renderer.domElement);
      scene.traverse((object) => {
        if (object instanceof THREE.Mesh) {
          object.geometry.dispose();
          object.material.dispose();
        }
      });
      renderer.dispose();
    };
  });
</script>

<div bind:this={container} class="scene-container">
  {#if loadingProgress < 100}
    <div class="loading-overlay">
      <div class="loading-spinner" />
      <div class="loading-text">Loading {loadingProgress.toFixed(0)}%</div>
    </div>
  {/if}
</div>

<style>
  .scene-container {
    width: 100%;
    height: 100%;
    position: relative;
  }

  .loading-overlay {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: rgba(0, 0, 0, 0.8);
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    color: white;
  }

  .loading-spinner {
    width: 40px;
    height: 40px;
    border: 3px solid var(  --light-sky-blue);
    border-top: 3px solid transparent;
    border-radius: 50%;
    animation: spin 1s linear infinite;
    margin-bottom: 1rem;
  }

  .loading-text {
    font-size: 1rem;
    color: var(  --light-sky-blue);
  }

  @keyframes spin {
    0% { transform: rotate(0deg); }
    100% { transform: rotate(360deg); }
  }
</style>