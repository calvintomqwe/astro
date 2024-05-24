<template>
    <div class="card-container">
      <div class="card w-96 bg-base-100 shadow-xl">
        <figure class="figure">
          <SpinningSphere :imageUrl="imageUrl" class="rounded-xl" />
        </figure>
        <div class="card-body">
          <h2 class="card-title">{{ title }}</h2>
          <p>{{ description }}</p>
          <div class="hidden-text">
            {{ longDesc }}
          </div>
        </div>
      </div>
    </div>
</template>

<script>
import SpinningSphere from './SpinningSphere.vue';

export default {
  name: 'CustomCard',
  components: {
    SpinningSphere
  },
  props: {
    imageUrl: {
      type: String,
      required: true
    },
    title: {
      type: String,
      default: 'Card Title'
    },
    description: {
      type: String,
      default: 'Card Description'
    },
    longDesc: {
      type: String,
      default: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit.'
    }
  },
  data() {
    return {
      showDetails: false,
    };
  },
  methods: {
    toggleDetails() {
      this.showDetails = !this.showDetails;
    },
  },
};
</script>

<style scoped>
.card-container {
  position: relative;
  padding: 5px;
  border: 2px solid lightblue;
  border-radius: 10px;
}

.hidden-text {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  color: white;
  display: flex;
  justify-content: center;
  align-items: center;
  opacity: 0;
  transition: opacity 0.3s ease;
  pointer-events: none;
  backdrop-filter: blur(10px);
  padding: 20px;
  box-sizing: border-box;
}

.card-container:hover .hidden-text {
  opacity: 1;
}

.card {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  height: 70vh; /* adjust as needed */
  width: 100%; /* Set desired width for the card */
}

.figure {
  width: 100%;
  height: 60%; /* adjust as needed */
}

.card-container {
  padding: 5px;
  border: 2px solid lightblue;
  border-radius: 10px;
}

.card-actions {
  display: flex;
  justify-content: flex-end;
}

.card-title {
  text-align: center;
}

.card {
  width: 100%; /* Set desired width for the card */
}

/* Add any necessary styles for SpinningSphere, card-body, etc. */
</style>