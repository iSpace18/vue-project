<!-- <script setup>
import TodoList from './components/TodoList.vue'
// import shoes_cart from './components/shoes_cart.vue'

</script>
<template>
  <div id="app">
    <TodoList />
  </div>
</template>

<script>
import TodoList from './components/TodoList.vue';

export default {
  components: {
    TodoList
  }
};
</script> -->
<template>
  <div id="app">
    <ShoeCard :shoe="shoeData" />
  </div>
</template>

<script>
import ShoeCard from './components/shoes_cart.vue';

export default {
  components: {
    ShoeCard
  },
  data() {
    return {
      shoeData: {
        brand: 'Nike',
        model: 'Air Max',
        price: 150,
        colors: ['#FF6347', '#4682B4', '#32CD32'] 
      }
    };
  }
};
</script>

<style>

</style>