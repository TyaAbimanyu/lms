<template>
  <div>
    <ul class="nav nav-pills common-tab gap-20 mb-24" role="tablist">
      <li v-for="tab in tabs" :key="tab.id" class="nav-item" role="presentation">
        <button
          class="nav-link"
          :class="{ active: activeTab === tab.id }"
          @click="activeTab = tab.id"
          type="button"
        >
          {{ tab.label }}
        </button>
      </li>
    </ul>

    <!-- START SECTION COURSES -->
    <div class="tab-content">
      <div v-for="tab in tabs" :key="tab.id">
        <div v-if="activeTab === tab.id" class="tab-pane fade show active">
          <div class="row g-20">
            <div
              v-for="(course, idx) in tab.content"
              :key="idx"
              class="col-xxl-3 col-lg-4 col-sm-6"
            >
              <CourseCard :course="formatCourseData(course)" />
            </div>
          </div>
        </div>
      </div>
    </div>
    <!-- END SECTION COURSES -->

    <!-- START SECTION RECOMMENDATION -->
    <div class="card mt-24">
      <div class="card-body">
        <div
          class="mb-20 d-flex justify-content-between align-items-center flex-wrap gap-8"
        >
          <h4 class="mb-0">Recommended For You</h4>
          <!-- Modified filter section -->
          <div class="d-flex align-items-center gap-8 flex-wrap">
            <div
              class="d-flex align-items-center text-gray-500 text-13 border border-gray-100 rounded-4 ps-8"
            >
              <span class="text-lg d-none d-md-block"><i class="ph ph-layout"></i></span>
              <select
                v-model="selectedCategory"
                class="form-control px-8 py-8 py-md-12 border-0 text-inherit rounded-4 text-center"
                style="min-width: 100px; font-size: 12px"
              >
                <option
                  value=""
                  label="All Categories"
                  style="text-align: center"
                ></option>
                <option v-for="cat in categories" :key="cat" :value="cat">
                  {{ cat }}
                </option>
              </select>
            </div>
            <div
              class="d-flex align-items-center text-gray-500 text-13 border border-gray-100 rounded-4 ps-8"
            >
              <span class="text-lg d-none d-md-block"
                ><i class="ph ph-funnel-simple"></i
              ></span>
              <select
                v-model="sortBy"
                class="form-control px-8 py-8 py-md-12 border-0 text-inherit rounded-4 text-center"
                style="min-width: 100px; font-size: 12px"
              >
                <option value="popular">Popular</option>
                <option value="latest">Latest</option>
                <option value="trending">Trending</option>
              </select>
            </div>
          </div>
        </div>

        <div class="row g-20">
          <div
            v-for="(course, index) in filteredAndSortedCourses"
            :key="index"
            class="col-xxl-3 col-lg-4 col-sm-6"
          >
            <CourseCardRecomendation :course="formatCourseData(course)" />
          </div>
        </div>
      </div>
    </div>
    <!-- END SECTION RECOMMENDATION -->
  </div>
</template>

<script setup>
import { computed, ref } from "vue";
import CourseCard from "@/components/courses/CourseCard.vue";
import CourseCardRecomendation from "@/components/courses/CourseCardRecomendation.vue";

const activeTab = ref("ongoing");

const tabs = [
  {
    id: "ongoing",
    label: "Ongoing (08)",
    content: [
      {
        title: "Full Stack Web Development",
        category: "Development",
        categoryBadgeClass: badgeClass("Development"),
        image: "src/assets/images/dummy/dummyCourse400x200.png",
        progress: 32,
        userImage: "src/assets/images/avatar/avatar-group1.png",
        creator: "Albert James",
        rating: 4.9,
        reviews: "12k",
      },
      {
        title: "UI/UX Design Course",
        category: "Design",
        categoryBadgeClass: badgeClass("Design"),
        image: "src/assets/images/dummy/dummyCourse400x200.png",
        progress: 20,
        userImage: "src/assets/images/avatar/avatar-group1.png",
        creator: "Albert James",
        rating: 4.9,
        reviews: "12k",
      },
      // Tambahkan course lainnya
    ],
  },
  {
    id: "completed",
    label: "Completed (10)",
    content: [
      {
        title: "Full Stack Web Development",
        category: "Design",
        categoryBadgeClass: badgeClass("Design"),
        image: "src/assets/images/dummy/dummyCourse400x200.png",
        progress: 32,
        userImage: "src/assets/images/avatar/avatar-group1.png",
        creator: "Albert James",
        rating: 4.9,
        reviews: "12k",
      },
      {
        title: "UI/UX Design Course",
        category: "Development",
        categoryBadgeClass: badgeClass("Development"),
        image: "src/assets/images/dummy/dummyCourse400x200.png",
        progress: 20,
        userImage: "src/assets/images/avatar/avatar-group1.png",
        creator: "Albert James",
        rating: 4.9,
        reviews: "12k",
      },
    ],
  },
  {
    id: "saved",
    label: "Saved (12)",
    content: [
      {
        title: "Full Stack Web Development",
        category: "Marketing",
        categoryBadgeClass: badgeClass("Marketing"),
        image: "src/assets/images/dummy/dummyCourse400x200.png",
        progress: 32,
        userImage: "src/assets/images/avatar/avatar-group1.png",
        creator: "Albert James",
        rating: 4.9,
        reviews: "12k",
      },
      {
        title: "UI/UX Design Course",
        category: "Design",
        categoryBadgeClass: badgeClass("Development"),
        image: "src/assets/images/dummy/dummyCourse400x200.png",
        progress: 20,
        userImage: "src/assets/images/avatar/avatar-group1.png",
        creator: "Albert James",
        rating: 4.9,
        reviews: "12k",
      },
    ],
  },
  {
    id: "favourite",
    label: "Favorite (25)",
    content: [
      {
        title: "Full Stack Web Marketing",
        category: "Development",
        categoryBadgeClass: badgeClass("Development"),
        image: "src/assets/images/dummy/dummyCourse400x200.png",
        progress: 32,
        userImage: "src/assets/images/avatar/avatar-group1.png",
        creator: "Albert James",
        rating: 4.9,
        reviews: "12k",
      },
      {
        title: "UI/UX Design Course",
        category: "Learning",
        categoryBadgeClass: badgeClass("Learning"),
        image: "src/assets/images/dummy/dummyCourse400x200.png",
        progress: 20,
        userImage: "src/assets/images/avatar/avatar-group1.png",
        creator: "Albert James",
        rating: 4.9,
        reviews: "12k",
      },
    ],
  },
];

function badgeClass(category) {
  switch (category) {
    case "Development":
      return "text-13 py-2 px-10 rounded-pill bg-success-50 text-success-600 mb-16";
    case "Design":
      return "text-13 py-2 px-10 rounded-pill bg-warning-50 text-warning-600 mb-16";
    case "Marketing":
      return "text-13 py-2 px-10 rounded-pill bg-info-50 text-info-600 mb-16";
    default:
      return "text-13 py-2 px-10 rounded-pill bg-secondary-50 text-secondary-600 mb-16";
  }
}

const selectedCategory = ref("");
const sortBy = ref("popular");

const categories = ["Development", "Design", "Frontend", "SEO"];

const recommendedCourses = ref([
  {
    title: "Full Stack Web Development",
    category: "Development",
    image: "src/assets/images/dummy/dummyCourse400x200.png",
    userImage: "src/assets/images/avatar/avatar-group1.png",
    creator: "Albert James",
    rating: 4.9,
    reviews: 12000,
    popularity: 95,
    latest: "2025-06-10",
    trending: 87,
  },
  {
    title: "Design System",
    category: "Design",
    image: "src/assets/images/dummy/dummyCourse400x200.png",
    userImage: "src/assets/images/avatar/avatar-group1.png",
    creator: "Albert James",
    rating: 4.8,
    reviews: 8500,
    popularity: 90,
    latest: "2025-05-01",
    trending: 90,
  },
  // Tambah course lain sesuai kebutuhan
]);

const filteredAndSortedCourses = computed(() => {
  let filtered = recommendedCourses.value;

  if (selectedCategory.value) {
    filtered = filtered.filter((c) => c.category === selectedCategory.value);
  }

  return [...filtered].sort((a, b) => {
    switch (sortBy.value) {
      case "popular":
        return b.popularity - a.popularity;
      case "latest":
        return new Date(b.latest) - new Date(a.latest);
      case "trending":
        return b.trending - a.trending;
      default:
        return 0;
    }
  });
});

// Add new helper function to format course data
function formatCourseData(course) {
  return {
    ...course,
    link: "/course-details",
    creatorImage: course.userImage,
    categoryClass: course.categoryBadgeClass || badgeClass(course.category),
  };
}
</script>

<style scoped>
.card {
  display: flex;
  flex-direction: column;
}

.card-body {
  height: 100%;
}

.fs-6 {
  font-size: 0.9rem !important;
}

.course-image-container {
  width: 100%;
  height: 200px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.course-image {
  width: 400px;
  height: 200px;
  object-fit: cover;
}
</style>
