<template>
  <div id="app">
    <div class="container">
      <h1>Star Wars Planets</h1>
      <br />
      <div>
        <table
          class="table table-hover table-bordered table-responsive table-primary"
        >
          <thead class="table-dark">
            <tr class="animated fadeIn fadeOut">
              <th scope="col">Name</th>
              <th scope="col">Climate</th>
              <th scope="col">Terrain</th>
              <th scope="col">Population</th>
            </tr>
          </thead>
          <tbody>
            <tr
              v-for="planet in planetsList"
              :key="planet.name"
              class="animated fadeIn fadeOut"
            >
              <td @click="clicked(planet)">{{ planet.name }}</td>
              <td>
                {{ planet.climate }}
              </td>
              <td>
                {{ planet.terrain }}
              </td>
              <td>
                {{ planet.population }}
              </td>
            </tr>
          </tbody>
        </table>
      </div>
      <b-pagination
        v-model="currentPage"
        @change="changePageNumber($event)"
        :total-rows="planetsLength"
        :per-page="perPage"
        first-number
        last-number
      ></b-pagination>
    </div>
    <hello-world v-if="selectedPlanet" :selectedPlanet="selectedPlanet">
    </hello-world>
  </div>
</template>

<script>
import axios from "axios";
import HelloWorld from "./components/HelloWorld.vue";

export default {
  name: "App",
  components: {
    HelloWorld,
  },

  data() {
    return {
      perPage: 5,
      currentPage: 1,
      planetsList: [],
      selectedPlanet: null,
    };
  },
  created() {
    this.getPlanetsList();
  },
  methods: {
    async getPlanetsList() {
      let vm = this;
      vm.planetsList = [];
      await axios
        .get("https://swapi.dev/api/planets")
        .then((res) => {
          vm.planetsList = res.data.results;
        })
        .catch((err) => {
          console.log(err);
        });
    },
    clicked(planet) {
      this.selectedPlanet = planet;
    },
    changePageNumber(value) {
      if (this.currentPage !== value) this.currentPage = value;
    },
  },
  computed: {
    planetsLength() {
      return this.planetsList.length;
    },
  },
};
</script>

<style lang="scss">
@import "~bootstrap/dist/css/bootstrap.css";
@import "~bootstrap-vue/dist/bootstrap-vue.css";
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
h1 {
  font-size: 50px;
}
table {
  cursor: pointer;
}
</style>
