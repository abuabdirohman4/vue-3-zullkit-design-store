<script setup>
// import { RouterLink } from "vue-router";
import Logo from "./Logo.vue";
import NavigationLinks from "./NavigationLinks.vue";
import UserInfo from "./UserInfo.vue";
import AuthButton from "./AuthButton.vue";

import { computed, onMounted } from "vue";
import { useUserStore } from "@/stores/user";

const userStore = useUserStore();
const isLoggedIn = computed(() => userStore.isLoggedIn);
const user = computed(() => userStore.user);
// const getUser = computed(() => userStore.getUser);

onMounted(() => {
  userStore.fetchUser();
});
</script>

<template>
  <!-- Navbar -->
  <nav
    class="bg-white border-gray-200 px-2 sm:px-4 py-2.5 rounded dark:bg-gray-800"
  >
    <div
      class="container flex flex-wrap items-center justify-between mx-auto my-2"
    >
      <Logo />
      <UserInfo v-if="isLoggedIn" :user="user.data" />
      <AuthButton v-else />
      <NavigationLinks />
    </div>
  </nav>
</template>
