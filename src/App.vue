
<template>
  <div id="app">
    <nav class="navbar">
      <img src="@/assets/logo.png" alt="Logo" class="navbar-logo" />
      <h1 class="navbar-title">Astro</h1>
    </nav>
    <PlanetsCard
      v-for="planet in paginatedCards"
      :key="planet.id"
      :imageUrl="planet.imageUrl"
      :title="planet.title"
      :description="planet.description"
      :longDesc="planet.longDesc"
      class="planet-card"
      ref="card"
    />
    <div class="join grid grid-cols-2">
      <button class="join-item btn btn-outline" @click="previousPage">Telluric planets</button>
      <button class="join-item btn btn-outline" @click="nextPage">Gazeous planets</button>
    </div>
  </div>
</template>

<script>
import PlanetsCard from './components/PlanetsCard.vue';

export default {
  name: 'App',
  components: {
    PlanetsCard
  },
  data() {
    return {
      currentPage: 1,
      cardsPerPage: 4,
      planets: [
        {
          id: 1,
          imageUrl: require('@/assets/Mercury.png'),
          title: 'Mercury',
          description: 'Mercury is the first planet from the Sun and the smallest in the Solar System.',
          longDesc: 'Mercury, the closest planet to the Sun, has an average temperature of about 167°C (332°F) during the day and -173°C (-279°F) at night. It has a diameter of 4,880 kilometers (3,032 miles). Despite being the smallest planet, Mercury has a large iron core, making it extremely dense.',
        },
        {
          id: 2,
          imageUrl: require('@/assets/Venus.png'),
          title: 'Venus',
          description: 'Venus is the second planet from the Sun, it’s the hottest planet in our solar system.',
          longDesc: 'Venus, known for its thick, toxic atmosphere composed mainly of carbon dioxide, has a scorching average temperature of 462°C (864°F), hotter than Mercury despite being farther from the Sun. With a diameter of 12,104 kilometers (7,521 miles), Venus is similar in size to Earth, earning it the nickname "Earth\'s twin." Its surface pressure is 92 times that of Earth\'s, making it a truly inhospitable environment.',
        },
        {
          id: 3,
          imageUrl: require('@/assets/earth.png'),
          title: 'Earth',
          description: 'Earth is the only planet in the Solar System that has a large amount of liquid water on its surface.',
          longDesc: 'Earth, our home planet, has an average surface temperature of about 15°C (59°F). It has a diameter of 12,742 kilometers (7,918 miles). Earth is the only planet known to support life, thanks to its liquid water, protective atmosphere, and suitable climate.',
        },
        {
          id: 4,
          imageUrl: require('@/assets/Mars.png'),
          title: 'Mars',
          description: 'There are intriguing clues that billions of years ago Mars was even more Earth-like than today.',
          longDesc: 'Mars, the red planet, has an average temperature of -63°C (-81°F) and a diameter of 6,779 kilometers (4,212 miles). Mars is famous for its striking red color due to iron oxide on its surface. It hosts the largest volcano in the solar system, Olympus Mons, and a canyon system, Valles Marineris, that dwarfs Earths Grand Canyon.',
        },
        {
          id: 5,
          imageUrl: require('@/assets/Jupiter.png'),
          title: 'Jupiter',
          description: 'Jupiter is the largest planet in our solar system – if it were a hollow shell, 1,000 Earths could fit inside.',
          longDesc: 'Jupiter, the giant of the solar system, has an average temperature of -145°C (-234°F) and an enormous diameter of 139,820 kilometers (86,881 miles). Known for its Great Red Spot, a massive storm larger than Earth, Jupiter has a strong magnetic field and at least 79 moons, including Ganymede, the largest moon in the solar system.',
        },
        {
          id: 6,
          imageUrl: require('@/assets/Saturn.png'),
          title: 'Saturn',
          description: 'Saturn, ringed planet that is the second largest planet in the solar system in mass and size.',
          longDesc: 'Saturn, recognized by its stunning ring system, has an average temperature of -178°C (-288°F) and a diameter of 116,460 kilometers (72,366 miles). Saturn\'s rings are made of ice and rock particles. It has 83 confirmed moons, with Titan being the largest, possessing a thick atmosphere and lakes of liquid methane.',
        },
        {
          id: 7,
          imageUrl: require('@/assets/Uranus.png'),
          title: 'Uranus',
          description: 'Uranus is the first planet to be discovered that had not been recognized in prehistoric times.',
          longDesc: 'Uranus, an ice giant with a blue-green hue due to methane in its atmosphere, has an average temperature of -195°C (-319°F) and a diameter of 50,724 kilometers (31,518 miles). Uniquely, Uranus rotates on its side, making its axial tilt about 98 degrees, which results in extreme seasonal variations.',
        },
        {
          id: 8,
          imageUrl: require('@/assets/Neptune.png'),
          title: 'Neptune',
          description: "The planet’s rich blue color comes from methane in its atmosphere, which absorbs red wavelengths of light.",
          longDesc: 'Neptune, the farthest planet from the Sun, has an average temperature of -201°C (-330°F) and a diameter of 49,244 kilometers (30,598 miles). Known for its striking blue color and supersonic winds, Neptune has a large moon, Triton, which exhibits geysers of nitrogen gas and is believed to have a subsurface ocean.',
        },
      ],
    };
  },
  computed: {
    paginatedCards() {
      const start = (this.currentPage - 1) * this.cardsPerPage;
      const end = start + this.cardsPerPage;
      return this.planets.slice(start, end);
    },
  },
  methods: {
    nextPage() {
      if (this.currentPage * this.cardsPerPage < this.planets.length) {
        this.currentPage++;
      }
    },
    previousPage() {
      if (this.currentPage > 1) {
        this.currentPage--;
      }
    },
  },
};
</script>

<style scoped>

.navbar {
  width: 100%;
  background-color: transparent;
  padding: 20px;
  text-align: center;
}

.navbar-title {
  color: #fff;
  font-size: 2em;
  font-weight: bold;
}

.navbar-logo {
  height: 50px;
  margin-right: 10px;
}

#app {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
}

.planet-card {
  flex: 1 0 100%;
  margin: 10px;
}

@media (min-width: 0px) {
  .planet-card {
    flex: 1 0 calc(100% - 20px); /* subtract margins */
  }
}

@media (min-width: 600px) {
  .planet-card {
    flex: 1 0 calc(50% - 20px); /* subtract margins */
  }
}

@media (min-width: 1200px) {
  .planet-card {
    flex: 1 0 calc(25% - 20px); /* subtract margins */
  }
}
</style>