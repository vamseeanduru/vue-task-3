<template>
  <div class="container">
    <div>
      <table
        class="table table-hover table-bordered table-responsive table-success"
      >
        <thead class="table-dark">
          <tr>
            <th>Planet Name</th>
            <th>Planet Climate</th>
            <th>Planet Terrain</th>
            <th>Planet Population</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td>{{ selectedPlanet.name }}</td>
            <td>{{ selectedPlanet.climate }}</td>
            <td>{{ selectedPlanet.terrain }}</td>
            <td>{{ selectedPlanet.population }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  props: {
    selectedPlanet: Object,
  },
  data() {
    return {};
  },
  created() {
    console.log(this.selectedPlanet);
  },
};
</script>

<style>
@import "~bootstrap/dist/css/bootstrap.css";
@import "~bootstrap-vue/dist/bootstrap-vue.css";
h1 {
  font-size: 50px;
}
</style>
