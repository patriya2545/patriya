<template>
  <div
    class="bg-purple-200 px-4 py-5 mx-auto sm:max-w-xl md:max-w-full w-full md:px-24 lg:px-8"
  >
    <div class="relative flex items-center justify-between">
      <div>
        <router-link to="/" class="inline-flex items-center">
          <img
            class="w-8 text-deep-purple-accent-400"
            src="~/assets/cat.png"
            alt=""
          />
          <span
            class="ml-2 text-xl font-bold tracking-wide text-gray-800 uppercase"
            >Mew Company</span
          >
        </router-link>
      </div>
      <div>
        <ul class="flex items-center hidden space-x-8 lg:flex">
          <li>
            <router-link
              to="/"
              class="inline-flex items-center font-medium tracking-wide text-gray-700 transition-colors duration-200 hover:text-deep-purple-accent-400"
            >
              <button>Product</button>
            </router-link>
          </li>
          <li>
            <router-link to="/profile">
              <button
                class="font-medium tracking-wide text-gray-700 transition-colors duration-200 hover:text-deep-purple-accent-400"
              >
                Profile
              </button>
            </router-link>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {};
  },
};
</script>