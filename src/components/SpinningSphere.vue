<template>
  <div class="sphere-container">
    <canvas ref="canvas"></canvas>
  </div>
</template>

<script>
import * as THREE from 'three';

export default {
  name: 'SpinningSphere',
  props: {
    imageUrl: {
      type: String,
      required: true
    }
  },
  mounted() {
    this.init();
    this.resize();
    this.animate();
  },
  methods: {
    init() {
      // Initialize renderer and enable shadows with alpha
      this.renderer = new THREE.WebGLRenderer({ canvas: this.$refs.canvas, alpha: true });
      this.renderer.shadowMap.enabled = true;
      this.renderer.shadowMap.type = THREE.PCFSoftShadowMap;

      // Initialize camera
      this.camera = new THREE.PerspectiveCamera(70, 1, 1, 100);
      this.camera.position.set(0, 0, 30); // Set the camera position to be centered horizontally

      // Initialize scene
      this.scene = new THREE.Scene();

      // Create sphere geometry and material with transparency
      const geometry = new THREE.SphereGeometry(10, 100, 100);
      const material = new THREE.MeshStandardMaterial({
        map: new THREE.TextureLoader().load(this.imageUrl),
        roughness: 0.5,
        metalness: 0
      });

      // Create mesh and enable shadows
      this.mesh = new THREE.Mesh(geometry, material);
      this.mesh.castShadow = false; // Disable shadow casting
      this.mesh.receiveShadow = true;
      this.scene.add(this.mesh);

      // Add directional light for lighting effects
      const directionalLight = new THREE.DirectionalLight(0xffffff, 1.5);
      directionalLight.position.set(20, 20, 20);
      directionalLight.castShadow = true;
      this.scene.add(directionalLight);

      // Optionally, add a spotlight to enhance lighting effects
      const spotlight = new THREE.SpotLight(0xffffff, 1.0);
      spotlight.position.set(50, 50, 50);
      spotlight.castShadow = true;
      this.scene.add(spotlight);

      // Add a plane to receive shadows
      const planeGeometry = new THREE.PlaneGeometry(200, 200);
      const planeMaterial = new THREE.ShadowMaterial({ opacity: 0.6 });
      const plane = new THREE.Mesh(planeGeometry, planeMaterial);
      plane.rotation.x = -Math.PI / 2;
      plane.position.y = -11;
      plane.receiveShadow = true;
      this.scene.add(plane);
    },
    resize() {
      if (this.$refs.canvas) {
        const width = this.$refs.canvas.clientWidth;
        const height = this.$refs.canvas.clientHeight;
        this.renderer.setSize(width, height, false);
        this.camera.aspect = width / height;
        this.camera.updateProjectionMatrix();
      }
    },
    animate() {
      this.resize();
      this.mesh.rotation.y -= 0.005;
      this.renderer.render(this.scene, this.camera);
      requestAnimationFrame(this.animate);
    }
  }
};
</script>

<style scoped>
.sphere-container {
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}
canvas {
  width: 100%;
  height: 100%;
}
</style>