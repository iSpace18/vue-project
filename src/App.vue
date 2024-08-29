<template>
  <div id="app">
    <h1>График пользовательских оценок</h1>
    <RatingChart />
  </div>
</template>

<script>
// Импортируем компонент
import RatingChart from './components/RatingChart.vue';

export default {
  name: 'App',
  components: {
    RatingChart,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  margin-top: 50px;
}
</style>
