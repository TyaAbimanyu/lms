<template>
    <div class="dashboard-main-body">

        <Breadcrumb title="Role & Access" :breadcrumbs="[
            { name: 'Role & Access' }
        ]" />

        <AssignRole />
    </div>
</template>
<script setup>
import Breadcrumb from '@/components/breadcrumb/Breadcrumb.vue';
import AssignRole from '@/components/RoleAccess/AssignRole.vue';

// Define component name
const componentName = "RolesAssign";
</script>