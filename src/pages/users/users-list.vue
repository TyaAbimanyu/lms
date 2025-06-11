<template>
    <div class="dashboard-main-body">

        <Breadcrumb title="Users List" :breadcrumbs="[
            { name: 'Users List' }
        ]" />

        <UserList />
    </div>
</template>
<script setup>
// import Breadcrumb from '@/components/breadcrumb/Breadcrumb.vue';
// import UserList from '@/components/Users/UserList.vue'
import Breadcrumb from '@/components/breadcrumb/Breadcrumb.vue';
import UserList from '@/components/Users/UserList.vue';

// Define component name
const componentName = "UsersList";
</script>