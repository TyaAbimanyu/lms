<template>
  <div class="dashboard-main-body">
    <Breadcrumb title="Role & Access" :breadcrumbs="[{ name: 'Role & Access' }]" />

    <Role />
  </div>
</template>
<script setup>
import Breadcrumb from "@/components/breadcrumb/Breadcrumb.vue";
import Role from "@/components/RoleAccess/Role.vue";

// Define component name
const componentName = "RoleAcces";
</script>
