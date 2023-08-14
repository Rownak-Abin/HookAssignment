<script>
import { ref, onMounted,onBeforeUnmount } from 'vue';
import { Chart,registerables } from 'chart.js';
Chart.register(...registerables)

export default {
  setup() {
    let pieChartCanvas = ref(null);

    onMounted(() => {
      if (pieChartCanvas.value) {
        const ctx = pieChartCanvas.value.getContext('2d');
        new Chart(ctx, {
          type: 'pie',
          data: {
            labels: ['Red', 'Blue', 'Yellow','pink','cyan'],
            datasets: [{
              data: [10, 20, 30,50,60],
              backgroundColor: ['red', 'blue', 'yellow','pink','cyan']
            }]
          }
        });
      }
    });

    onBeforeUnmount(() => {
        pieChartCanvas = null;
        console.log("Pie-chart onBeforeUnmount called");
    });

    return {
      pieChartCanvas
    };
  }
};
</script>

<template>
  <div align="center" style="height:500px">
    <canvas ref="pieChartCanvas"></canvas>
  </div>
</template>

<style scoped>

</style>