<script setup>
import { useRouter } from "vue-router";
import { useUserStore } from "../../stores/user";

const userStore = useUserStore();
const router = useRouter();
const props = defineProps({
  user: Object,
});

async function logout() {
  try {
    localStorage.clear();
    userStore.logout();
    router.push("/");
  } catch (error) {
    console.log(error);
  }
}
</script>

<template>
  <div class="flex items-center md:order-2">
    <div class="font-regular mr-2 ml-5 text-sm">Halo, {{ user.name }}</div>
    <div class="dropdown">
      <button
        type="button"
        class="mr-3 flex rounded-full bg-gray-800 text-sm focus:ring-4 focus:ring-gray-300 dark:focus:ring-gray-600 md:mr-0"
      >
        <span class="sr-only">Open user menu</span>
        <img
          class="h-8 w-8 rounded-full"
          :src="user.profile_photo_url"
          alt="user photo"
        />
      </button>
      <div
        class="dropdown-content right-0 z-50 my-4 list-none divide-y divide-gray-100 rounded bg-white text-base shadow-[0_8px_16px_0px_rgba(0,0,0,0.3)] dark:divide-gray-600 dark:bg-gray-700"
      >
        <div class="px-4 py-3">
          <span class="block text-sm text-gray-900 dark:text-white">{{
            user.name
          }}</span>
          <span
            class="font-regular block truncate text-sm text-gray-500 dark:text-gray-400"
            >{{ user.email }}</span
          >
        </div>
        <ul class="py-1" aria-labelledby="dropdown">
          <!-- <li>
            <a
              href="#"
              class="block px-4 py-2 text-sm text-gray-700 hover:bg-gray-100 dark:text-gray-200 dark:hover:bg-gray-600 dark:hover:text-white"
              >Subscriptions</a
            >
          </li> -->
          <!-- <li>
            <a
              href="#"
              class="block px-4 py-2 text-sm text-gray-700 hover:bg-gray-100 dark:text-gray-200 dark:hover:bg-gray-600 dark:hover:text-white"
              >Settings</a
            >
          </li> -->
          <li>
            <button
              href="#"
              @click.prevent="logout"
              class="w-full px-4 py-2 text-left text-sm text-gray-700 hover:bg-gray-100 dark:text-gray-200 dark:hover:bg-gray-600 dark:hover:text-white"
            >
              Sign out
            </button>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>
