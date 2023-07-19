<template>
    <v-container>
        <v-row>
            <v-col cols="6" sm="6" md="4" class="p-2 pt-3">
                <v-card class="text-center" shaped>
                    <v-card-text>
                        <div class="total">
                            <div :class="$vuetify.breakpoint.mdAndDown ? 'h6' : 'h5'">Total Sales This Month</div>
                            <div class="amount" :class="$vuetify.breakpoint.mdAndDown ? 'h5' : 'h4'">${{
                                totalSalesThisMonth }}</div>
                        </div>
                    </v-card-text>
                </v-card>
            </v-col>

            <v-col cols="6" sm="6" md="4" class="p-2 pt-3">
                <v-card class="text-center" shaped>
                    <v-card-text>
                        <div class="total">
                            <div :class="$vuetify.breakpoint.mdAndDown ? 'h6' : 'h5'">Total Sales This Year</div>
                            <div class="amount" :class="$vuetify.breakpoint.mdAndDown ? 'h5' : 'h4'">${{
                                totalSalesThisYear }}</div>
                        </div>
                    </v-card-text>
                </v-card>
            </v-col>

            <v-col cols="6" sm="6" md="4" class="p-2 pt-3">
                <v-card class="text-center" shaped>
                    <v-card-text>
                        <div class="total">
                            <div :class="$vuetify.breakpoint.mdAndDown ? 'h6' : 'h5'">Change In Customers</div>
                            <div class="amount" :class="$vuetify.breakpoint.mdAndDown ? 'h5' : 'h4'">{{
                                changeInCustomers }}%</div>
                        </div>
                    </v-card-text>
                </v-card>
            </v-col>
        </v-row>

        <v-row class="">
            <v-col cols="12" md="4" class="p-2">
                <v-card class="chart-card border-radius">
                    <div class="text-muted p-2 h5">
                        Latest Transaction
                    </div>
                    <div>
                        <LineChartComponent />
                    </div>
                </v-card>
            </v-col>
            <v-col cols="12" md="2" class="p-2">
                <v-card class="chart-card border-radius">
                    <PieChart />
                </v-card>
            </v-col>
            <v-col cols="12" md="6" class="p-2">
                <v-card class="chart-card border-radius text-center">
                    <div class="text-muted p-2 h5">
                        Sales Number by Month
                    </div>
                    <div>
                        <BarChart />
                    </div>
                </v-card>
            </v-col>
        </v-row>

        <v-row>
            <v-col cols="12" md="6" class="p-2">
                <v-card class="chart-card text-center border-radius">
                        <div class="text-muted p-2 h5">
                            Projected Revenue
                        </div>
                        <div>
                            <StackedBarChart />
                        </div>
                </v-card>
            </v-col>
            <v-col cols="12" md="6" class="p-2">
                <v-card class="chart-card text-center border-radius">
                    <div class="text-muted p-2 h5">
                        Projected Revenue
                    </div>
                    <div>
                        <GroupedBarChart />
                    </div>
                </v-card>
            </v-col>
        </v-row>
        <v-row class="p-2">
            <TransactionTable class="border-radius"></TransactionTable>
        </v-row>
    </v-container>
</template>
  
<script>
import BarChart from '@/components/BarChart.vue';
import LineChartComponent from '@/components/LineChartComponent.vue';
import PieChart from '@/components/PieChart.vue';
import TransactionTable from "@/components/TransactionTable.vue";
import GroupedBarChart from '@/components/GroupedBarChart.vue';
import StackedBarChart from '@/components/StackedBarChart.vue';

export default {
    data() {
        return {
            totalSalesThisMonth: 237488,
            totalSalesThisYear: 3495859,
            changeInCustomers: 10,
            messages: 10,
        }
    },
    components: {
        BarChart,
        LineChartComponent,
        PieChart,
        TransactionTable,
        GroupedBarChart,
        StackedBarChart
    },
}
</script>
  
<style>
.d-flex.align-center.justify-content-between.mx-2 {
    justify-content: flex-start;
}

.chart-card {
    display: block;
    height: 200px;
}

.border-radius {
    border-radius: 10px !important;
}
.amount{
    color: #246CF8;
}
</style>
  