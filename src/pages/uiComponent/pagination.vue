<template>
    <div class="dashboard-main-body">

        <Breadcrumb title="Pagination" :breadcrumbs="[
            { name: 'Components / Pagination' }
        ]" />

        <PaginationData />
    </div>
</template>
<script setup>
import Breadcrumb from '@/components/breadcrumb/Breadcrumb.vue';
import PaginationData from '@/components/UiComponent/PaginationData.vue'

// Define component name
const componentName = "Pagination";
</script>