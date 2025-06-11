<template>
    <div class="dashboard-main-body">

        <Breadcrumb title="Input Form" :breadcrumbs="[
            { name: 'Input Form' }
        ]" />

        <InputFrom />
    </div>

</template>
<script setup>
import Breadcrumb from '@/components/breadcrumb/Breadcrumb.vue';
import InputFrom from '@/components/Forms/Form.vue'

// Define component name
const componentName = "Forms";
</script>