<template>
  <div class="card border border-gray-100">
    <div class="card-body p-8">
      <router-link :to="course.link" class="bg-main-100 rounded-8 overflow-hidden text-center mb-8 h-164 flex-center p-8">
        <img :src="course.image" :alt="course.title">
      </router-link>
      <div class="p-8">
        <span :class="course.categoryClass">{{ course.category }}</span>
        <h5 class="mb-0">
          <router-link :to="course.link" class="hover-text-main-600">{{ course.title }}</router-link>
        </h5>
        
        <div class="flex-align gap-8 mt-12">
          <span class="text-main-600 flex-shrink-0 text-13 fw-medium">{{ course.progress }}%</span>
          <div class="progress w-100 bg-main-100 rounded-pill h-8">
            <div class="progress-bar bg-main-600 rounded-pill" :style="{ width: `${course.progress}%` }"></div>
          </div>
        </div>

        <div class="flex-align gap-8 flex-wrap mt-16">
          <img :src="course.creatorImage" class="w-32 h-32 rounded-circle object-fit-cover" alt="Creator">
          <div>
            <span class="text-gray-600 text-13">
              Created by 
              <router-link to="/profile" class="fw-semibold text-gray-700 hover-text-main-600 hover-text-decoration-underline">
                {{ course.creator }}
              </router-link>
            </span>
            <div class="flex-align gap-4">
              <span class="text-15 fw-bold text-warning-600 d-flex"><i class="ph-fill ph-star"></i></span>
              <span class="text-13 fw-bold text-gray-600">{{ course.rating }}</span>
              <span class="text-13 fw-bold text-gray-600">({{ course.reviews }})</span>
            </div>
          </div>
        </div>
        <router-link to="/live-class" class="btn btn-outline-main rounded-pill py-9 w-100 mt-24">
          Continue Watching
        </router-link>
      </div>
    </div>
  </div>
</template>

<script setup>
defineProps({
  course: {
    type: Object,
    required: true
  }
})
</script>
