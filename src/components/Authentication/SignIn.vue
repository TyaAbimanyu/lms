<template>
  <section class="auth bg-base d-flex flex-wrap">
    <div class="auth-left d-lg-block d-none">
      <div class="d-flex align-items-center flex-column h-100 justify-content-center">
        <img src="@/assets/images/auth/auth-img.png" alt="" />
      </div>
    </div>
    <div class="auth-right py-32 px-24 d-flex flex-column justify-content-center">
      <div class="max-w-464-px mx-auto w-100">
        <div>
          <router-link to="/" class="mb-40 max-w-290-px">
            <img src="@/assets/images/logo.png" alt="" />
          </router-link>
          <h4 class="mb-12">Sign In to your Account</h4>
          <p class="mb-32 text-secondary-light text-lg">
            Welcome back! please enter your detail
          </p>
        </div>
        <form @submit.prevent>
          <div class="icon-field mb-16">
            <span class="icon top-50 translate-middle-y">
              <iconify-icon icon="mage:email"></iconify-icon>
            </span>
            <input
              type="email"
              class="form-control h-56-px bg-neutral-50 radius-12"
              placeholder="Email"
              v-model="email"
            />
          </div>
          <div class="position-relative mb-20">
            <div class="icon-field">
              <span class="icon top-50 translate-middle-y">
                <iconify-icon icon="solar:lock-password-outline"></iconify-icon>
              </span>
              <input
                :type="showPassword ? 'text' : 'password'"
                class="form-control h-56-px bg-neutral-50 radius-12"
                id="your-password"
                placeholder="Password"
                v-model="password"
              />
            </div>
            <span
              class="toggle-password ri-eye-line cursor-pointer position-absolute end-0 top-50 translate-middle-y me-16 text-secondary-light"
              :class="{ 'ri-eye-off-line': showPassword }"
              @click="togglePassword"
            ></span>
          </div>

          <div class="d-flex justify-content-between gap-2">
            <div class="form-check style-check d-flex align-items-center">
              <input
                class="form-check-input border border-neutral-300"
                type="checkbox"
                id="remember"
                v-model="remember"
              />
              <label class="form-check-label" for="remember">Remember me</label>
            </div>
            <router-link to="forgot-password" class="text-primary-600 fw-medium"
              >Forgot Password?</router-link
            >
          </div>

          <button
            type="submit"
            class="btn btn-primary text-sm btn-sm px-12 py-16 w-100 radius-12 mt-32"
          >
            Sign In
          </button>
        </form>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref } from "vue";

// Define component name
const componentName = "SignIn";

// Reactive state
const email = ref("");
const password = ref("");
const showPassword = ref(false);
const remember = ref(false);

// Methods
const togglePassword = () => {
  showPassword.value = !showPassword.value;
};
</script>
