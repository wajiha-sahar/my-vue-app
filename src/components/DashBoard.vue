<template>
  <div class="dashboard">
    <div class="chart-container">
      <h2>Line Chart</h2>
      <LineChart @chartRendered="onChartRendered(1)" />
    </div>
    <div class="chart-container">
      <h2>Donut Chart</h2>
      <DonutChart v-if="currentChart > 0" @chartRendered="onChartRendered(2)" />
    </div>
    <div class="chart-container">
      <h2>Column Chart</h2>
      <ColumnChart v-if="currentChart > 1" @chartRendered="onChartRendered(3)" />
    </div>
  </div>
</template>

<script>
import { markRaw } from 'vue';
import LineChart from './LineChart.vue';
import DonutChart from './DonutChart.vue';
import ColumnChart from './ColumnChart.vue';

export default {
  name: 'DashBoard',
  components: {
    LineChart: markRaw(LineChart),
    DonutChart: markRaw(DonutChart),
    ColumnChart: markRaw(ColumnChart)
  },
  data() {
    return {
      currentChart: 0 // Start with the first chart
    }
  },
  methods: {
    onChartRendered(chartPriority) {
      console.log("chart rendered", chartPriority);
      if (this.currentChart < chartPriority) {
        setTimeout(() => {
          this.currentChart = chartPriority;
        }, 1000)

      }
    }
  }
}
</script>

<style scoped>
.dashboard {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 2rem;
}

.chart-container {
  width: 80%;
  max-width: 600px;
  display: flex;
  flex-direction: column;
  align-items: center;
}

h2 {
  margin-bottom: 0;
}
</style>
