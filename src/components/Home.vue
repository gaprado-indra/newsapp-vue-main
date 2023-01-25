<template>
    <div class="homepage-container">
        <data-table></data-table>
    </div>
</template>

<script>
import DataTable from "@/components/DataTable.vue"

export default {
    name: "HomeContainer",
    components: {
        DataTable,
    },
};
</script>