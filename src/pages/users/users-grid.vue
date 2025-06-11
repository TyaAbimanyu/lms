<template>
    <div class="dashboard-main-body">

        <Breadcrumb title="Users Grid" :breadcrumbs="[
            { name: 'Users Grid' }
        ]" />

        <UserGrid />
    </div>
</template>
<script setup>
import Breadcrumb from '@/components/breadcrumb/Breadcrumb.vue';
import UserGrid from '@/components/Users/UserGrid.vue'

// Define component name
const componentName = "UsersGrid";
</script>