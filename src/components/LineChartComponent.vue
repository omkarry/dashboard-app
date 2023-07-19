<template>
  <LineChart :data="chartData" :options="chartOptions" />
</template>
  
<script>
import { Line as LineChart } from 'vue-chartjs'
import transactions from '@/data/transactions';
import {
  Chart as ChartJS,
  Title,
  Tooltip,
  Legend,
  LineElement,
  LinearScale,
  CategoryScale,
  PointElement,
} from 'chart.js'

ChartJS.register(
  Title,
  Tooltip,
  Legend,
  LineElement,
  LinearScale,
  CategoryScale,
  PointElement,
)

export default {
  name: 'LineChartComponent',
  components: { LineChart },
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
            beginAtZero: true,
            grid: {
              display: false,
            }
          },
        },
        plugins: {
          legend: {
            display: false,
          },
        },
        elements: {
          point: {
            radius: 0, // Set the radius to 0 to remove point circles
          },
        },
        interaction: {
          mode: 'index',
          intersect: false,
        },
        spanGaps: true,
        animation: false,
      }
    }
  },
  beforeMount() {
    this.prepareChartData();
  },
  methods: {
    prepareChartData() {
      const sortedTransactions = transactions.sort(
        (a, b) => new Date(a.timestamp) - new Date(b.timestamp)
      );

      const labels = sortedTransactions
        .map((transaction) => this.formatDate(transaction.timestamp))
        .slice(-30);

      const data = sortedTransactions
        .map((transaction) => transaction.amount)
        .slice(-30);

      this.chartData = {
        labels,
        datasets: [
          {
            label: "Amount",
            backgroundColor: "#E81F89",
            borderColor: "#246CF8",
            data,
          },
        ],
      };
    },

    formatDate(timestamp) {
      const date = new Date(timestamp);
      return date.toLocaleString("default", { month: "2-digit", year: "2-digit" });
    },
    updateChartSize() {
      if (this.$refs.lineChart) {
        this.$refs.lineChart.resize();
      }
    },
  },
};
</script>