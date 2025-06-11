<template>
    <div class="dashboard-main-body">

        <Breadcrumb title="Input Layout" :breadcrumbs="[
            { name: 'Input Layout' }
        ]" />

        <InputLayout />
    </div>

</template>
<script setup>
import Breadcrumb from '@/components/breadcrumb/Breadcrumb.vue';
import InputLayout from '@/components/Forms/InputLayout.vue';

// Define component name
const componentName = "FormsLayout";
</script>