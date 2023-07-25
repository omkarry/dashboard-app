<template>
    <div>
        <bar :data="chartData" :options="chartOptions" />
    </div>
</template>
  
<script>
import { Bar } from 'vue-chartjs'
import { Chart as ChartJS, Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale } from 'chart.js'
import transactions from '@/data/transactions'
ChartJS.register(Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale)
export default {
    components: {
        Bar,
    },
    data() {
        return {
            chartData: {},
            chartOptions: {
                responsive: true,
                maintainAspectRatio: false,
                scales: {
                    x: {
                        stacked: true,
                        title: {
                            display: true,
                            text: "Month",
                        },
                        grid: {
                            display: false,
                        }
                    },
                    y: {
                        stacked: true,
                        title: {
                            display: true,
                            text: "Revenue",
                        },
                        grid: {
                            display: false,
                        }
                    },
                },
                plugins: {
                    legend: {
                        display: false,
                        labels: {
                            color: 'rgb(255, 99, 132)'
                        }
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
            const revenueByMonth = {};

            transactions.forEach((transaction) => {
                const timestamp = new Date(transaction.timestamp);
                const monthYear = `${(timestamp.getMonth() + 1)
                    .toString()
                    .padStart(2, "0")}/${timestamp.getFullYear().toString().slice(2)}`;

                if (!revenueByMonth[monthYear]) {
                    revenueByMonth[monthYear] = { estimated: 0, actual: 0 };
                }

                const revenueType = transaction.purchase_type === "new" ? "estimated" : "actual";
                revenueByMonth[monthYear][revenueType] += parseFloat(transaction.amount);
            });

            const labels = Object.keys(revenueByMonth);
            const datasets = [
                {
                    label: "Estimated Revenue",
                    backgroundColor: "#E81F89",
                    data: labels.map((monthYear) => revenueByMonth[monthYear].estimated),
                },
                {
                    label: "Actual Revenue",
                    backgroundColor: "#246CF8",
                    data: labels.map((monthYear) => revenueByMonth[monthYear].actual),
                },
            ];

            this.chartData = {
                labels,
                datasets,
            };
        },
    },
};
</script>
  