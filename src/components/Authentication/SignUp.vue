<template>
    <section class="auth bg-base d-flex flex-wrap">
      <div class="auth-left d-lg-block d-none">
        <div class="d-flex align-items-center flex-column h-100 justify-content-center">
          <img src="@/assets/images/auth/auth-img.png" alt="">
        </div>
      </div>
      <div class="auth-right py-32 px-24 d-flex flex-column justify-content-center">
        <div class="max-w-464-px mx-auto w-100">
          <div>
            <router-link to="/" class="mb-40 max-w-290-px">
              <img src="@/assets/images/logo.png" alt="">
            </router-link>
            <h4 class="mb-12">Sign Up to your Account</h4>
            <p class="mb-32 text-secondary-light text-lg">Welcome back! please enter your detail</p>
          </div>
          <form @submit.prevent="handleSubmit">
            <div class="icon-field mb-16">
              <span class="icon top-50 translate-middle-y">
                <iconify-icon icon="f7:person"></iconify-icon>
              </span>
              <input type="text" class="form-control h-56-px bg-neutral-50 radius-12" placeholder="Username" v-model="form.username">
            </div>
            <div class="icon-field mb-16">
              <span class="icon top-50 translate-middle-y">
                <iconify-icon icon="mage:email"></iconify-icon>
              </span>
              <input type="email" class="form-control h-56-px bg-neutral-50 radius-12" placeholder="Email" v-model="form.email">
            </div>
            <div class="mb-20">
              <div class="position-relative">
                <div class="icon-field">
                  <span class="icon top-50 translate-middle-y">
                    <iconify-icon icon="solar:lock-password-outline"></iconify-icon>
                  </span>
                  <input :type="passwordVisible ? 'text' : 'password'"
                         class="form-control h-56-px bg-neutral-50 radius-12"
                         id="your-password"
                         placeholder="Password"
                         v-model="form.password">
                </div>
                <span :class="['toggle-password', passwordVisible ? 'ri-eye-off-line' : 'ri-eye-line', 'cursor-pointer', 'position-absolute', 'end-0', 'top-50', 'translate-middle-y', 'me-16', 'text-secondary-light']"
                      @click="togglePassword">
                </span>
              </div>
              <span class="mt-12 text-sm text-secondary-light">Your password must have at least 8 characters</span>
            </div>
            <div class="">
              <div class="d-flex justify-content-between gap-2">
                <div class="form-check style-check d-flex align-items-start">
                  <input class="form-check-input border border-neutral-300 mt-4" type="checkbox" v-model="form.termsAccepted" id="condition">
                  <label class="form-check-label text-sm" for="condition">
                    By creating an account means you agree to the
                    <router-link to="javascript:void(0)" class="text-primary-600 fw-semibold">Terms & Conditions</router-link> and our
                    <router-link to="javascript:void(0)" class="text-primary-600 fw-semibold">Privacy Policy</router-link>
                  </label>
                </div>
              </div>
            </div>
  
            <button type="submit" class="btn btn-primary text-sm btn-sm px-12 py-16 w-100 radius-12 mt-32"> Sign Up</button>
  
            <div class="mt-32 center-border-horizontal text-center">
              <span class="bg-base z-1 px-4">Or sign up with</span>
            </div>
            <div class="mt-32 d-flex align-items-center gap-3">
              <button type="button"
                      class="fw-semibold text-primary-light py-16 px-24 w-50 border radius-12 text-md d-flex align-items-center justify-content-center gap-12 line-height-1 bg-hover-primary-50">
                <iconify-icon icon="ic:baseline-facebook" class="text-primary-600 text-xl line-height-1"></iconify-icon>
                Facebook
              </button>
              <button type="button"
                      class="fw-semibold text-primary-light py-16 px-24 w-50 border radius-12 text-md d-flex align-items-center justify-content-center gap-12 line-height-1 bg-hover-primary-50">
                <iconify-icon icon="logos:google-icon" class="text-primary-600 text-xl line-height-1"></iconify-icon>
                Google
              </button>
            </div>
            <div class="mt-32 text-center text-sm">
              <p class="mb-0">Already have an account? <router-link to="sign-in" class="text-primary-600 fw-semibold">Sign In</router-link></p>
            </div>
          </form>
        </div>
      </div>
    </section>
  </template>
  
  <script>
  export default {
    name: 'SignUpForm',
    data() {
      return {
        form: {
          username: '',
          email: '',
          password: '',
          termsAccepted: false
        },
        passwordVisible: false
      };
    },
    methods: {
      togglePassword() {
        this.passwordVisible = !this.passwordVisible;
      },
      handleSubmit() {
        // Example submit handler
        if (this.form.password.length < 8) {
          alert('Password must be at least 8 characters');
          return;
        }
        if (!this.form.termsAccepted) {
          alert('You must accept the terms and conditions');
          return;
        }
        alert('Form submitted!');
      }
    }
  };
  </script>
  