<template>
    <div>
      <Doughnut :data="chartData" :options="chartOptions" />
    </div>
  </template>
  
  <script>
  import { Doughnut } from 'vue-chartjs'
  import { Chart as ChartJS, Title, Tooltip, Legend, ArcElement } from 'chart.js'
  
  ChartJS.register(Title, Tooltip, Legend, ArcElement)
  
  export default {
    name: 'DonutChart',
    components: { Doughnut },
    data() {
      return {
        chartData: {
          labels: ['Red', 'Blue', 'Yellow'],
          datasets: [{
            label: 'Dataset',
            data: [300, 50, 100],
            backgroundColor: ['#FF6384', '#36A2EB', '#FFCE56']
          }]
        },
        chartOptions: {
          responsive: true,
          plugins: {
            legend: {
              position: 'top'
            },
            tooltip: {
              callbacks: {
                label: (context) => `${context.label}: ${context.raw}`
              }
            }
          }
        }
      }
    },
    mounted() {
      this.$nextTick(() => {
        this.$emit('chartRendered');
      });
    }
  }
  </script>
  