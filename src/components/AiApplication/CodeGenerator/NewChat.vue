<template>
    <div class="col-xxl-9 col-lg-8">
      <div class="chat-main card overflow-hidden">
        <div class="chat-sidebar-single gap-8 justify-content-between cursor-default flex-nowrap">
          <div class="d-flex align-items-center gap-16">
            <router-link to="/code-generator-new" class="text-primary-light text-2xl line-height-1">
              <i class="ri-arrow-left-line"></i>
            </router-link>
            <h6 class="text-lg mb-0 text-line-1">Please create a 5 Column table with HTML Css and js</h6>
          </div>
  
          <div class="d-flex align-items-center gap-16 flex-shrink-0">
            <button type="button" class="text-secondary-light text-xl line-height-1 text-hover-primary-600">
              <i class="ri-edit-2-line"></i>
            </button>
            <button type="button" class="text-secondary-light text-xl line-height-1 text-hover-primary-600">
              <i class="ri-delete-bin-6-line"></i>
            </button>
          </div>
        </div>
  
        <div class="chat-message-list max-h-612-px min-h-612-px position-relative">
          <div class="d-flex align-items-center justify-content-center flex-column h-100 position-absolute top-50 start-50 translate-middle">
            <img src="@/assets/images/chatgpt/empty-message-icon2.png" alt="">
            <span class="text-secondary-light text-md mt-16">Type New Message </span>
          </div>
        </div>
  
        <form class="chat-message-box" @submit.prevent="sendMessage">
          <input type="text" v-model="chatMessage" name="chatMessage" placeholder="Message wowdash...">
          <button
            type="submit"
            class="w-44-px h-44-px d-flex justify-content-center align-items-center radius-8 bg-primary-600 text-white bg-hover-primary-700 text-xl">
            <iconify-icon icon="f7:paperplane"></iconify-icon>
          </button>
        </form>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        chatMessage: '',
      };
    },
    methods: {
      sendMessage() {
        if (this.chatMessage.trim()) {
          console.log('Message sent:', this.chatMessage);
          this.chatMessage = '';
        }
      },
    },
  };
  </script>
  