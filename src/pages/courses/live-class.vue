<template>
  <div class="m-8">
    <!-- Breadcrumb Start -->
    <Breadcrumb
      title="Course Details"
      :breadcrumbs="[
        {
          name: 'Home',
          link: '/student-courses',
          icon: 'solar:home-smile-angle-outline',
        },
        { name: 'Course Details' },
      ]"
    />
    <!-- Breadcrumb End -->

    <div class="row gy-4">
      <div class="col-md-8">
        <div class="rounded-16 overflow-hidden position-relative">
          <span
            class="live-badge text-white bg-danger-600 rounded-8 text-15 px-32 py-10 position-absolute inset-block-start-0 inset-inline-start-0 z-1 ms-24 mt-24"
            >Live</span
          >
          <video ref="player" class="player" playsinline controls>
            <source
              src="https://cdn.plyr.io/static/demo/View_From_A_Blue_Moon_Trailer-720p.mp4"
              type="video/mp4"
            />
            <source src="" type="video/webm" />
          </video>
        </div>
        <!-- Course Card Start -->
        <div class="card mt-24">
          <div class="card-body">
            <div class="pb-24 flex-between gap-4 flex-wrap">
              <h5 class="mb-12 fw-bold">Questions ({{ questionCount }})</h5>
              <a
                href="#"
                class="btn btn-outline-gray text-gray-500 text-13 py-8 px-8 rounded-4"
                >See All</a
              >
            </div>

            <ul class="comment-list">
              <li v-for="(comment, index) in comments" :key="index">
                <div class="d-flex align-items-start gap-8 flex-xs-row flex-column">
                  <img
                    :src="comment.avatar"
                    alt=""
                    class="w-48 h-48 rounded-circle object-fit-cover flex-shrink-0"
                  />
                  <div class="">
                    <div class="flex-align flex-wrap gap-8">
                      <h6 class="text-15 fw-bold mb-0">{{ comment.name }}</h6>
                      <span
                        v-if="comment.isCurrentUser"
                        class="py-0 px-8 bg-main-50 text-main-600 rounded-4 text-15 fw-medium h5 mb-0 fw-bold"
                        >You</span
                      >
                      <span class="text-gray-300 text-13">{{ comment.time }}</span>
                    </div>
                    <p class="text-15 text-gray-600 mt-8">{{ comment.text }}</p>
                  </div>
                </div>
                <ul class="sub-comment-list mt-24">
                  <li v-for="(reply, replyIndex) in comment.replies" :key="replyIndex">
                    <div class="d-flex align-items-start gap-8 flex-xs-row flex-column">
                      <img
                        :src="reply.avatar"
                        alt=""
                        class="w-48 h-48 rounded-circle object-fit-cover flex-shrink-0"
                      />
                      <div class="">
                        <div class="flex-align flex-wrap gap-8">
                          <h6 class="text-15 fw-bold mb-0">{{ reply.name }}</h6>
                          <span
                            v-if="reply.role"
                            class="py-0 px-8 bg-main-50 text-main-600 rounded-4 text-15 fw-medium h5 mb-0 fw-bold"
                            >{{ reply.role }}</span
                          >
                          <span class="text-gray-300 text-13">{{ reply.time }}</span>
                        </div>
                        <p class="text-15 text-gray-600 mt-8">{{ reply.text }}</p>
                      </div>
                    </div>
                  </li>
                </ul>
              </li>
            </ul>

            <form @submit.prevent="submitQuestion" class="position-relative mt-44">
              <input
                v-model="newQuestion"
                type="text"
                class="form-control bg-main-50 border-0 py-18 pe-54"
                placeholder="Drop your questions here..."
              />
              <button
                type="submit"
                class="w-40 h-40 flex-center rounded-8 bg-white text-main-600 hover-bg-main-600 hover-text-white transition-1 position-absolute inset-inline-end-0 top-50 translate-middle-y me-8"
              >
                <iconify-icon icon="ph:paper-plane-tilt" />
              </button>
            </form>
          </div>
        </div>
        <!-- Course Card End -->
      </div>

      <div class="col-md-4">
        <div class="card">
          <div class="card-body">
            <div class="flex-between flex-wrap mb-12">
              <h5 class="mb-0 fw-bold">Your Lesson</h5>
              <span class="text-13">{{ completedLessons }}/{{ totalLessons }}</span>
            </div>
            <div class="flex-align gap-8 mb-12">
              <span class="text-main-600 flex-shrink-0 text-13 fw-medium"
                >{{ progressPercentage }}%</span
              >
              <div
                class="progress w-100 bg-main-100 rounded-pill h-4"
                role="progressbar"
                :aria-valuenow="progressPercentage"
                aria-valuemin="0"
                aria-valuemax="100"
              >
                <div
                  class="progress-bar bg-main-600 rounded-pill"
                  :style="{ width: progressPercentage + '%' }"
                ></div>
              </div>
            </div>
            <ul class="lesson-list">
              <li
                v-for="(lesson, index) in lessons"
                :key="index"
                class="lesson-list__item d-flex align-items-start gap-16"
                :class="{ active: lesson.completed }"
              >
                <span
                  class="circle w-16 h-16 flex-center rounded-circle text-main-100 text-13 flex-shrink-0"
                >
                  <iconify-icon icon="ph-fill:check-circle" />
                </span>
                <div>
                  <a
                    href="#"
                    class="text-13 text-heading d-block text-gray-600 fw-medium hover-text-main-600"
                  >
                    {{ lesson.title }}
                    <span class="text-13 text-heading d-block text-gray-600 fw-medium">{{
                      lesson.status
                    }}</span>
                  </a>
                </div>
              </li>
            </ul>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, computed } from "vue";
import Breadcrumb from "@/components/breadcrumb/Breadcrumb.vue";
// import Plyr from "plyr";
// import "plyr/dist/plyr.css";

// Data for comments and questions
const questionCount = ref(85);
const newQuestion = ref("");
const comments = ref([
  {
    name: "Amir Hamja",
    avatar: "/assets/images/thumbs/mentor-img1.png",
    isCurrentUser: true,
    time: "8:00PM",
    text:
      "Fringilla justo mauris cursus arcu sit urna. Nullam eu non bibendum quam mi dolor nisi orci?",
    replies: [
      {
        name: "Selina Eyvi",
        avatar: "/assets/images/thumbs/mentor-img2.png",
        role: "Mentor",
        time: "8:10PM",
        text:
          "Justo gravida eget id massa volutpat. Volutpat vehicula tortor fusce sed pellentesque id sagittis eu commodo. Ut ultrices neque faucibus morbi rhoncus. Volutpat vehicula tortor fusce sed pellentesque id sagittis eu commodo",
      },
    ],
  },
]);

// Data for lessons
const completedLessons = ref(3);
const totalLessons = ref(35);
const progressPercentage = computed(() =>
  Math.round((completedLessons.value / totalLessons.value) * 100)
);

const lessons = ref([
  {
    title: "Intro",
    status: "Last access: 12Jan 24. 8:00PM",
    completed: true,
  },
  {
    title: "What is Digital Marketing?",
    status: "Last access: 12Jan 24. 8:00PM",
    completed: true,
  },
  {
    title: "Digital Marketing Fundamental",
    status: "Locked",
    completed: false,
  },
  {
    title: "Digital Marketing Fundamental",
    status: "Locked",
    completed: false,
  },
  {
    title: "Digital Marketing Fundamental",
    status: "Locked",
    completed: false,
  },
  {
    title: "Digital Marketing Fundamental",
    status: "Locked",
    completed: false,
  },
  {
    title: "Digital Marketing Fundamental",
    status: "Locked",
    completed: false,
  },
]);

// Player reference
const player = ref(null);

// Initialize Plyr video player on mounted
// onMounted(() => {
//   if (player.value) {
//     new Plyr(player.value);
//   }
// });

// Submit question function
const submitQuestion = () => {
  if (newQuestion.value.trim()) {
    // Add question logic here
    console.log("Submitted question:", newQuestion.value);
    newQuestion.value = "";
  }
};
</script>

<style scoped>
.lesson-list__item.active .circle {
  color: var(--bs-primary);
}

.flex-between {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.flex-align {
  display: flex;
  align-items: center;
}

.flex-center {
  display: flex;
  align-items: center;
  justify-content: center;
}

/* Additional custom CSS to match the original design can be added here */
</style>
