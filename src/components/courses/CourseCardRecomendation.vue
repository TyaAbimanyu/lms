<template>
  <div class="card border border-gray-100 course-card">
    <div class="card-body p-8">
      <router-link
        :to="course.link"
        class="course-image-container bg-main-100 rounded-8 overflow-hidden text-center mb-8 flex-center"
      >
        <img :src="course.image" :alt="course.title" class="course-image" />
      </router-link>
      <div class="p-8">
        <span :class="course.categoryClass">{{ course.category }}</span>
        <h5 class="mb-0">
          <router-link :to="course.link" class="hover-text-main-600">{{
            course.title
          }}</router-link>
        </h5>

        <div class="flex-align gap-8 flex-wrap mt-16">
          <div>
            <img
              :src="course.creatorImage"
              class="w-32 h-32 rounded-circle object-fit-cover"
              alt="Creator"
            />
            <button @click="toggleFavorite" aria-label="Favorite">
              <i
                :class="[
                  'ph-fill',
                  'ph-heart',
                  isFavorite ? 'text-danger-600' : 'text-gray-400',
                ]"
                style="font-size: 24px"
              ></i>
            </button>
          </div>
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
            <div class="flex-align gap-4">
              <span class="text-15 fw-bold text-warning-600 d-flex"
                ><i class="ph-fill ph-star"></i
              ></span>
              <span class="text-13 fw-bold text-gray-600">{{ course.rating }}</span>
              <span class="text-13 fw-bold text-gray-600">({{ course.reviews }})</span>
            </div>
          </div>
        </div>

        <div class="row justify-content-between align-items-center mt-3">
          <div class="col-auto">40 Hours {{ course.duration }}</div>
          <div class="col-auto d-flex align-items-center gap-2">
            <Star :size="18" weight="fill" class="text-warning-600" />
            <span class="fw-bold text-gray-700">{{ course.rating }}</span>
          </div>
        </div>
        <router-link
          to="/live-class"
          class="btn btn-primary rounded-pill py-9 w-100 mt-24"
        >
          Continue Watching
        </router-link>
      </div>
    </div>
  </div>
</template>

<script setup>
import { PhStar as Star } from "@phosphor-icons/vue";

defineProps({
  course: {
    type: Object,
    required: true,
  },
});
</script>

<style scoped>
.course-card {
  width: 100%;
  height: 550px;
}

.course-image-container {
  width: 100%;
  height: 180px;
  min-height: 180px;
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
}

.course-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
}
</style>
