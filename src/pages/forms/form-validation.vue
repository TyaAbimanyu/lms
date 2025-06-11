<template>
    <div class="dashboard-main-body">

        <Breadcrumb title="Form Validation" :breadcrumbs="[
            { name: 'Form Validation' }
        ]" />

        <FormValidationData />
    </div>
</template>
<script setup>
import Breadcrumb from '@/components/breadcrumb/Breadcrumb.vue';
import FormValidationData from '@/components/Forms/FormValidation.vue';

// Define component name
const componentName = "FormValidation";
</script>