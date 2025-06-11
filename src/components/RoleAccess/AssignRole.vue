<template>
  <div class="card h-100 p-0 radius-12">
    <div
      class="card-header border-bottom bg-base py-16 px-24 d-flex align-items-center flex-wrap gap-3 justify-content-between">
      <div class="d-flex align-items-center flex-wrap gap-3">
        <span class="text-md fw-medium text-secondary-light mb-0">Show</span>
        <select v-model="rolesPerPage" @change="changePage(1)"
          class="form-select form-select-sm w-auto ps-12 py-6 radius-12 h-40-px">
          <option v-for="n in 10" :key="n" :value="n">{{ n }}</option>
        </select>
        <form class="navbar-search" @submit.prevent>
          <input type="text" v-model="searchQuery" @input="changePage(1)" class="bg-base h-40-px w-auto"
            placeholder="Search" />
          <iconify-icon icon="ion:search-outline" class="icon"></iconify-icon>
        </form>
        <select v-model="statusFilter" @change="changePage(1)"
          class="form-select form-select-sm w-auto ps-12 py-6 radius-12 h-40-px">
          <option value="">Status</option>
          <option value="Active">Active</option>
          <option value="Inactive">Inactive</option>
        </select>
      </div>
    </div>

    <div class="card-body p-24">
      <div class="table-responsive scroll-sm">
        <table class="table bordered-table sm-table mb-0">
          <thead>
            <tr>
              <th scope="col">
                <div class="d-flex align-items-center gap-10">
                  <div class="form-check style-check d-flex align-items-center">
                    <input class="form-check-input radius-4 border input-form-dark" type="checkbox" v-model="selectAll"
                      @change="toggleSelectAll" />
                  </div>
                  S.L
                </div>
              </th>
              <th scope="col">Username</th>
              <th scope="col" class="text-center">Role Permission</th>
              <!-- <th scope="col" class="text-center">Status</th> -->
              <th scope="col" class="text-center">Action</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(user, index) in paginatedRoles" :key="user.id">
              <td>
                <div class="d-flex align-items-center gap-10">
                  <div class="form-check style-check d-flex align-items-center">
                    <input class="form-check-input radius-4 border border-neutral-400" type="checkbox" :value="user.id"
                      v-model="selectedUsers" />
                  </div>
                  {{ startIndex + index + 1 }}
                </div>
              </td>
              <td>
                <div class="d-flex align-items-center">
                  <img :src="user.image" alt=""
                    class="w-40-px h-40-px rounded-circle flex-shrink-0 me-12 overflow-hidden" />
                  <div class="flex-grow-1">
                    <span class="text-md mb-0 fw-normal text-secondary-light">{{ user.name }}</span>
                  </div>
                </div>
              </td>
              <td class="text-center">{{ user.role }}</td>
              <!-- <td class="text-center">{{ user.isActive ? 'Active' : 'Inactive' }}</td> -->
              <td class="text-center">
                <div class="dropdown">
                  <button class="btn btn-outline-primary-600 px-18 py-11 dropdown-toggle toggle-icon" type="button"
                    data-bs-toggle="dropdown" aria-expanded="false">
                    Assign Role
                  </button>
                  <ul class="dropdown-menu">
                    <li v-for="role in roleOptions" :key="role">
                      <a class="dropdown-item" href="javascript:void(0)" @click="assignRole(user.id, role)">
                        {{ role }}
                      </a>
                    </li>
                  </ul>
                </div>
              </td>
            </tr>
          </tbody>
        </table>
      </div>

      <Pagination :currentPage="currentPage" :totalPages="totalPages" :startIndex="startIndex" :endIndex="endIndex"
        :totalItems="filteredRoles.length" @page-changed="changePage" />
    </div>
  </div>
</template>

<script setup>
import user1 from '@/assets/images/user-list/user-list1.png'
import user2 from '@/assets/images/user-list/user-list2.png'
import user3 from '@/assets/images/user-list/user-list3.png'
import user4 from '@/assets/images/user-list/user-list4.png'
import user5 from '@/assets/images/user-list/user-list5.png'
import user6 from '@/assets/images/user-list/user-list6.png'
import user7 from '@/assets/images/user-list/user-list7.png'
import user8 from '@/assets/images/user-list/user-list8.png'
import user10 from '@/assets/images/user-list/user-list10.png'

import Pagination from '@/components/pagination/index.vue'
import { ref, computed, watch } from 'vue';

// Define component name
const componentName = 'UserRoleTable';

// Reactive state
const currentPage = ref(1);
const rolesPerPage = ref(10);
const searchQuery = ref('');
const statusFilter = ref('');
const selectAll = ref(false);
const selectedUsers = ref([]);
const roleOptions = ref(['Waiter', 'Manager', 'Project Manager', 'Game Developer', 'Head', 'Management']);
const roles = ref([
  { id: 1, name: 'Kathryn Murphy', role: 'Waiter', isActive: true, image: user1 },
  { id: 2, name: 'Annette Black', role: 'Manager', isActive: true, image: user2 },
  { id: 3, name: 'Ronald Richards', role: 'Project Manager', isActive: false, image: user3 },
  { id: 4, name: 'Eleanor Pena', role: 'Game Developer', isActive: true, image: user4 },
  { id: 5, name: 'Leslie Alexander', role: 'Head', isActive: false, image: user5 },
  { id: 6, name: 'Albert Flores', role: 'Management', isActive: false, image: user6 },
  { id: 7, name: 'Jacob Jones', role: 'Waiter', isActive: false, image: user7 },
  { id: 8, name: 'Jerome Bell', role: 'Waiter', isActive: false, image: user8 },
  { id: 9, name: 'Marvin McKinney', role: 'Waiter', isActive: false, image: user2 },
  { id: 10, name: 'Cameron Williamson', role: 'Admin', isActive: false, image: user10 },
  { id: 11, name: 'Williamson', role: 'Admin', isActive: false, image: user1 },
]);

// Computed properties
const filteredRoles = computed(() => {
  return roles.value.filter(role => {
    const matchSearch = searchQuery.value === '' || role.name.toLowerCase().includes(searchQuery.value.toLowerCase());
    const matchStatus = statusFilter.value === '' || (statusFilter.value === 'Active' && role.isActive) || (statusFilter.value === 'Inactive' && !role.isActive);
    return matchSearch && matchStatus;
  });
});

const paginatedRoles = computed(() => {
  const start = (currentPage.value - 1) * rolesPerPage.value;
  return filteredRoles.value.slice(start, start + rolesPerPage.value);
});

const totalPages = computed(() => {
  return Math.ceil(filteredRoles.value.length / rolesPerPage.value);
});

const startIndex = computed(() => {
  return (currentPage.value - 1) * rolesPerPage.value;
});

const endIndex = computed(() => {
  return Math.min(startIndex.value + rolesPerPage.value, filteredRoles.value.length);
});

// Watch
watch(selectedUsers, () => {
  selectAll.value = paginatedRoles.value.every(user => selectedUsers.value.includes(user.id));
});

// Methods
const changePage = (page) => {
  currentPage.value = page;
  selectAll.value = paginatedRoles.value.every(user => selectedUsers.value.includes(user.id));
};

const toggleSelectAll = () => {
  if (selectAll.value) {
    selectedUsers.value = paginatedRoles.value.map(user => user.id);
  } else {
    selectedUsers.value = selectedUsers.value.filter(id => !paginatedRoles.value.some(u => u.id === id));
  }
};

const assignRole = (userId, role) => {
  const index = roles.value.findIndex(u => u.id === userId);
  if (index !== -1) {
    roles.value.splice(index, 1, { ...roles.value[index], role });
  }
};
</script>