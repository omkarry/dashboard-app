<template>
    <v-card>
        <div class="text-muted p-2 h5">
            Transactions
        </div>
        <v-data-table :headers="headers" :items="transactions" :fixed-header="true" :height="tableHeight"
            :items-per-page="itemsPerPage" :search="search" :loading="loading" @update:page="updatePage"
            @update:items-per-page="updateItemsPerPage">
            <!-- :hide-default-footer="true" -->
            <template v-slot:[`item.timestamp`]="{ item }">
                {{ formatDate(item.timestamp) }}
            </template>
        </v-data-table>
    </v-card>
</template>

<script>
import transactions from "../data/transactions";

export default {
    data() {
        return {
            transactions: [],
            headers: [
                { text: "Timestamp", value: "timestamp", sortable: true },
                { text: "First Name", value: "first_name", sortable: true },
                { text: "Last Name", value: "last_name", sortable: true },
                { text: "Email", value: "email", sortable: true },
                { text: "Company", value: "company", sortable: true },
                { text: "Amount", value: "amount", sortable: true },
                { text: "License Type", value: "license_type", sortable: true },
                { text: "Purchase Type", value: "purchase_type", sortable: true },
            ],
            search: "",
            loading: false,
            itemsPerPage: 25,
            currentPage: 1,
            tableHeight: 500,
        };
    },
    mounted() {
        this.transactions = transactions;
    },
    computed: {
        slicedTransactions() {
            const start = (this.currentPage - 1) * this.itemsPerPage;
            const end = start + this.itemsPerPage;
            return this.transactions.slice(start, end);
        },
    },
    methods: {
        updatePage(page) {
            this.currentPage = page;
        },
        updateItemsPerPage(itemsPerPage) {
            this.itemsPerPage = itemsPerPage;
        },
        formatDate(timestamp) {
            const date = new Date(timestamp);
            return date.toLocaleDateString();
        },
    },
};
</script>
