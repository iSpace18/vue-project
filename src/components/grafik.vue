<template>
  <div>
    <h2>{{ chartData.header }}</h2>
    <canvas ref="myChart"></canvas>
    <div>
      <button @click="addData">Добавить данные</button>
      <button @click="removeData">Удалить данные</button>
    </div>
  </div>
</template>

<script>
import { onMounted, ref } from 'vue';
import Chart from 'chart.js/auto';

export default {
  name: 'RatingChart',
  setup() {
    const chartInstance = ref(null);
    const ctx = ref(null);

    const chartData = ref({
      header: 'User rating',
      maxvalue: 254,
      data: [
        { title: '5 stars', value: 150 },
        { title: '4 stars', value: 63 },
        { title: '3 stars', value: 15 },
        { title: '2 stars', value: 6 },
        { title: '1 star', value: 20 },
      ],
    });

    const renderChart = () => {
      // Уничтожаем предыдущий график
      if (chartInstance.value) {
        chartInstance.value.destroy();
      }

      // Создаем новый график
      chartInstance.value = new Chart(ctx.value, {
        type: 'bar',
        data: {
          labels: chartData.value.data.map(item => item.title),
          datasets: [{
            label: chartData.value.header,
            data: chartData.value.data.map(item => item.value),
            backgroundColor: chartData.value.data.map(item => {
              const percentage = (item.value / chartData.value.maxvalue) * 100;
              return `rgba(54, 162, 235, ${percentage / 100})`;
            }),
            borderColor: 'rgba(54, 162, 235, 1)',
            borderWidth: 1,
          }],
        },
        options: {
          indexAxis: 'y',
          scales: {
            x: {
              beginAtZero: true,
              max: chartData.value.maxvalue,
            },
          },
        },
      });
    };

    const addData = () => {
      const newData = { title: `${chartData.value.data.length + 1} stars`, value: Math.floor(Math.random() * chartData.value.maxvalue) };
      chartData.value.data.push(newData);
      renderChart();
    };

    const removeData = () => {
      chartData.value.data.pop();
      renderChart();
    };

    onMounted(() => {
      ctx.value = document.querySelector('canvas').getContext('2d');
      renderChart();
    });

    return {
      chartData,
      addData,
      removeData,
    };
  },
};
</script>

<style scoped>
button {
  margin: 5px;
}
</style>
