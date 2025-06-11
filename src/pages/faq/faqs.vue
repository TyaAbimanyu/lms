<template>
  <div class="dashboard-main-body">
    <Breadcrumb title="Faq" :breadcrumbs="[{ name: 'Faq' }]" />

    <FrequentlyQuestion />
  </div>
</template>
<script setup>
import Breadcrumb from "@/components/breadcrumb/Breadcrumb.vue";
import FrequentlyQuestion from "@/components/FAQs/FrequentlyQuestion.vue";

// Define component name
const componentName = "FAQs";
</script>
