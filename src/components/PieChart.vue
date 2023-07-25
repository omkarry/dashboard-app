<template>
    <Pie :data="chartData" :options="chartOptions" />
</template>
  
<script>
import { Pie } from 'vue-chartjs'
import transactions from '../data/transactions';
import {
    Chart as ChartJS,
    Tooltip,
    ArcElement,
    CategoryScale
} from 'chart.js'
ChartJS.register(Tooltip, ArcElement, CategoryScale)

export default {
    name: 'PieChart',
    components: { Pie },
    data() {
        return {
            chartData: {},
            chartOptions: {

                responsive: true,
                maintainAspectRatio: false,
                plugins: {
                    legend: {
                        display: false,
                    }
                }
            },
        }
    },
    beforeMount() {
        this.prepareChartData();
    },
    methods: {
        prepareChartData() {
            const purchaseTypeCounts = {};

            transactions.forEach((transaction) => {
                const { purchase_type } = transaction;
                purchaseTypeCounts[purchase_type] = purchaseTypeCounts[purchase_type]
                    ? purchaseTypeCounts[purchase_type] + 1
                    : 1;
            });
            const data = Object.values(purchaseTypeCounts);
            const labels = Object.keys(purchaseTypeCounts);
            this.chartData = {
                labels,
                datasets: [
                    {
                        backgroundColor: ["#E81A89", "#246CF8", "#FFCE56"],
                        data,
                    },
                ],
            };
        },
    },
};
</script>