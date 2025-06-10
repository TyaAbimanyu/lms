<template>
  <div>
    <!-- Breadcrumb Start -->
    <nav aria-label="breadcrumb" class="breadcrumb mb-24">
      <ul class="flex-align gap-4">
        <li>
          <a
            href="#"
            class="text-gray-200 fw-normal text-15 hover-text-main-600"
            @click.prevent="$router.push({ path: '/' })"
          >
            Home
          </a>
        </li>
        <li>
          <span class="text-gray-500 fw-normal d-flex">
            <i class="ph ph-caret-right"></i>
          </span>
        </li>
        <li>
          <span class="text-main-600 fw-normal text-15">Student Courses</span>
        </li>
      </ul>
    </nav>
    <!-- Breadcrumb End -->

    <!-- Course Tab Start -->
    <div class="card">
      <div class="card-body">
        <div class="mb-24">
          <ul class="nav nav-pills common-tab gap-20" id="pills-tab" role="tablist">
            <li class="nav-item" role="presentation">
              <button class="nav-link" :class="{ active: activeTab === 'ongoing' }" 
                      @click="activeTab = 'ongoing'">
                Ongoing (08)
              </button>
            </li>
            <li class="nav-item" role="presentation">
              <button class="nav-link" :class="{ active: activeTab === 'completed' }" 
                      @click="activeTab = 'completed'">
                Completed (10)
              </button>
            </li>
            <li class="nav-item" role="presentation">
              <button class="nav-link" :class="{ active: activeTab === 'saved' }" 
                      @click="activeTab = 'saved'">
                Saved (12)
              </button>
            </li>
            <li class="nav-item" role="presentation">
              <button class="nav-link" :class="{ active: activeTab === 'favourite' }" 
                      @click="activeTab = 'favourite'">
                Favorite (25)
              </button>
            </li>
          </ul>
        </div>

        <div class="tab-content">
          <!-- Tab panes content here -->
          <div class="row g-20">
            <div v-for="(course, index) in courses" :key="index" class="col-xxl-3 col-lg-4 col-sm-6">
              <div class="card border border-gray-100">
                <div class="card-body p-8">
                  <a :href="course.link" class="bg-main-100 rounded-8 overflow-hidden text-center mb-8 h-164 flex-center p-8">
                    <img :src="course.image" :alt="course.title">
                  </a>
                  <div class="p-8">
                    <span :class="course.categoryClass">{{ course.category }}</span>
                    <h5 class="mb-0">
                      <a :href="course.link" class="hover-text-main-600">{{ course.title }}</a>
                    </h5>
                    <!-- Progress bar -->
                    <div class="flex-align gap-8 mt-12">
                      <span class="text-main-600 flex-shrink-0 text-13 fw-medium">{{ course.progress }}%</span>
                      <div class="progress w-100 bg-main-100 rounded-pill h-8">
                        <div class="progress-bar bg-main-600 rounded-pill" :style="{ width: course.progress + '%' }"></div>
                      </div>
                    </div>
                    <!-- Course creator info -->
                    <div class="flex-align gap-8 flex-wrap mt-16">
                      <img :src="course.creatorImage" class="w-32 h-32 rounded-circle object-fit-cover" alt="User Image">
                      <div>
                        <span class="text-gray-600 text-13">Created by 
                          <a href="profile.html" class="fw-semibold text-gray-700 hover-text-main-600 hover-text-decoration-underline">
                            {{ course.creator }}
                          </a>
                        </span>
                        <div class="flex-align gap-4">
                          <span class="text-15 fw-bold text-warning-600 d-flex"><i class="ph-fill ph-star"></i></span>
                          <span class="text-13 fw-bold text-gray-600">{{ course.rating }}</span>
                          <span class="text-13 fw-bold text-gray-600">({{ course.reviews }})</span>
                        </div>
                      </div>
                    </div>
                    <div class="col-12">
                        <b-button variant="outline-primary">Primary</b-button>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <!-- Course Tab End -->
    
    <!-- Recommended Course section would go here -->
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { useRouter } from 'vue-router'

const router = useRouter()
const activeTab = ref('ongoing')

const courses = ref([
  {
    title: 'Full Stack Web Development',
    category: 'Development',
    categoryClass: 'text-13 py-2 px-10 rounded-pill bg-success-50 text-success-600 mb-16',
    image: 'src/assets/images/logo.png',
    link: 'course-details.html',
    progress: 32,
    creator: 'Albert James',
    creatorImage: 'src/assets/images/logo.png',
    rating: '4.9',
    reviews: '12k'
  },
  // Add more course objects here
])
</script>

<style scoped>
/* Add any component-specific styles here */
</style>
