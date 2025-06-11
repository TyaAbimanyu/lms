<template>
  <div class="card border border-gray-100 course-card">
    <div class="card-body p-4">
      <router-link
        :to="course.link"
        class="bg-main-100 rounded-8 overflow-hidden text-center mb-4 h-120 flex-center p-6"
      >
        <img :src="course.image" :alt="course.title" />
      </router-link>
      <div class="p-4">
        <span :class="course.categoryClass">{{ course.category }}</span>
        <p>
          <router-link :to="course.link" class="hover-text-main-600">{{
            truncateText(course.title)
          }}</router-link>
        </p>

        <div class="flex-align gap-4 mt-8">
          <span class="text-main-600 flex-shrink-0 text-13 fw-medium"
            >{{ course.progress }}%</span
          >
          <div class="progress w-100 bg-main-100 rounded-pill h-8">
            <div
              class="progress-bar bg-main-600 rounded-pill"
              :style="{ width: `${course.progress}%` }"
            ></div>
          </div>
        </div>

        <div class="flex-align gap-4 flex-wrap mt-12">
          <img
            :src="course.creatorImage"
            class="w-24 h-24 rounded-circle object-fit-cover"
            alt="Creator"
          />
          <div class="d-flex justify-content-between align-items-center w-100">
            <div class="d-flex gap-8 align-items-center">
              <div>
                <span class="text-gray-600 text-13">
                  Created by
                  <router-link
                    to="/profile"
                    class="fw-semibold text-gray-700 hover-text-main-600 hover-text-decoration-underline"
                  >
                    {{ course.creator }}
                  </router-link>
                </span>
              </div>
            </div>
            <div class="flex-align gap-4">
              <span class="text-15 fw-bold text-warning-600 d-flex"
                ><i class="ph-fill ph-star"></i
              ></span>
              <span class="text-13 fw-bold text-gray-600">{{ course.rating }}</span>
              <span class="text-13 fw-bold text-gray-600">({{ course.reviews }})</span>
            </div>
          </div>
        </div>
        <router-link
          to="/live-class"
          class="btn-primary btn-outline-main rounded-pill py-6 w-100 mt-16 text-center"
        >
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
    required: true,
  },
});

function truncateText(text, maxLength = 25) {
  if (!text) return "";
  return text.length > maxLength ? text.slice(0, maxLength) + "..." : text;
}
</script>

<style scoped>
.course-card {
  max-width: 320px;
}

@media screen and (max-width: 768px) {
  .course-card {
    max-width: 90%;
    margin: 0 auto;
  }
}
</style>
