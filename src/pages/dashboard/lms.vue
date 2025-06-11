<template>
    <div class="dashboard-main-body">

        <Breadcrumb title="Dashboard" :breadcrumbs="[
            { name: 'LMS / Learning System' }
        ]" />

        <div class="row gy-4 mb-24">
            <!-- ======================= First Row Cards Start =================== -->
            <EnrollmentRate />
            <TrafficSources />
            <!-- ======================= First Row Cards End =================== -->

            <!-- ================== Second Row Cards Start ======================= -->
            <!-- Top Categories Card Start -->
            <Categories />
            <!-- Top Categories Card End -->

            <!-- Instructor Card Start -->
            <Instructors />
            <!-- Instructor Card End -->


            <!-- Student Progress Card Start -->
            <StudentProgress />
            <!-- Student Progress Card End -->
            <!-- ================== Second Row Cards End ======================= -->


            <!-- ================== Third Row Cards Start ======================= -->
            <Courses />
            <CourseActivityChart />
            <!-- ================== Third Row Cards End ======================= -->

        </div>

    </div>
</template>

<script setup>
import Breadcrumb from '@/components/breadcrumb/Breadcrumb.vue';
import ApexCharts from "vue3-apexcharts";
import { Icon } from "@iconify/vue"; 
import EnrollmentRate from "@/components/dashboard/Lms/EnrollmentRate.vue"
import TrafficSources from "@/components/dashboard/Lms/TrafficSources.vue"
import Categories from "@/components/dashboard/Lms/Categories.vue"
import Instructors from "@/components/dashboard/Lms/Instructors.vue"
import StudentProgress from "@/components/dashboard/Lms/StudentProgress.vue"
import Courses from "@/components/dashboard/Lms/Courses.vue"
import CourseActivityChart from "@/components/dashboard/Lms/CourseActivityChart.vue"

// No need to define components or name in Vue 3 Composition API with <script setup>
// Components are automatically registered from imports
</script>