<template>
    <div class="dashboard-main-body">

        <Breadcrumb title="Add User" :breadcrumbs="[
            { name: 'Add User' }
        ]" />

        <AddUser />

        
    </div>
</template>
<script setup>
import Breadcrumb from '@/components/breadcrumb/Breadcrumb.vue';
import AddUser from '@/components/Users/AddUser.vue'

// Define component name
const componentName = "AddUsers";
</script>