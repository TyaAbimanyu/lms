<template>
  <div class="dashboard-main-body">
    <Breadcrumb title="View Profile" :breadcrumbs="[{ name: 'View Profile' }]" />

    <ViewProfiles />
  </div>
</template>
<script setup>
import Breadcrumb from "@/components/breadcrumb/Breadcrumb.vue";
import ViewProfiles from "@/components/Users/ViewProfile.vue";

// Define component name
const componentName = "ViewProfile";
</script>
