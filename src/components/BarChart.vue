<template>
  <Bar :data="chartData" :options="chartOptions" class="font-family-poppins"/>
</template>

<script>
import { Bar } from 'vue-chartjs'
import { Chart as ChartJS, Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale } from 'chart.js'
import transactions from '@/data/transactions'
ChartJS.register(Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale)

export default {
  name: 'BarChart',
  components: { Bar },
  data() {
    return {
      chartData: {},
      chartOptions: {
        responsive: true,
        maintainAspectRatio: false,
        scales: {
          x: {
            title: {
              display: true,
              text: "Month",
            },
            grid: {
              display: false,
            }
          },
          y: {
            title: {
              display: true,
              text: "Sales Number",
            },
            grid: {
              display: false,
            }
          },
        }
      }
    }
  },
  beforeMount() {
    this.prepareChartData();
  },
  methods: {
    prepareChartData() {
      const salesByMonth = {};

      transactions.forEach((transaction) => {
        const timestamp = new Date(transaction.timestamp);
        const monthYear = `${(timestamp.getMonth() + 1)
          .toString()
          .padStart(2, "0")}/${timestamp.getFullYear().toString().slice(2)}`;

        if (salesByMonth[monthYear]) {
          salesByMonth[monthYear] += 1;
        } else {
          salesByMonth[monthYear] = 1;
        }
      });

      const labels = Object.keys(salesByMonth);
      const data = Object.values(salesByMonth);

      this.chartData = {
        labels,
        datasets: [
          {
            label: "Sales Number",
            backgroundColor: "#E81A89",
            data,
          },
        ],
      };
    },
  },
}
</script>

<style>
.font-family-poppins{
  font-family: Poppins, serif;
}
</style>