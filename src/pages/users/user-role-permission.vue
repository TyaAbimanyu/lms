<template>
  <div class="dashboard-main-body">
    <Breadcrumb
      title="User Roles & Permissions"
      :breadcrumbs="[{ name: 'User Roles & Permissions' }]"
    />
    <RolesPermission />
  </div>
</template>
<script setup>
import Breadcrumb from "@/components/breadcrumb/Breadcrumb.vue";
import RolesPermission from "@/components/Users/RolesPermission.vue";

// Define component name
const componentName = "Roles&Permission";
</script>
