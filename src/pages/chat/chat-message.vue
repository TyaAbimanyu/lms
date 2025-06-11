<template>
  <div class="dashboard-main-body">
    <Breadcrumb title="Chat" :breadcrumbs="[
      { name: 'Chat' }
    ]" />
    <div class="chat-wrapper">
      <ChatSidebar />
      <ChatMessage />
    </div>

  </div>
</template>
<script setup>
import Breadcrumb from '@/components/breadcrumb/Breadcrumb.vue';
import { Icon } from "@iconify/vue"; 
import ChatSidebar from "@/components/chat/ChatSidebar.vue"
import ChatMessage from "@/components/chat/ChatMessage.vue"

// Define component name
const componentName = "Chat";
</script>